---
title: 用Java来监测文件夹变化并自动部署hexo
urlname: hexo_permalink
tags:
  - hexo
abbrlink: de90c921
date: 2018-11-01 11:11:22
---
## 为什么要做这个自动部署脚本
在前不久使用了Hexo作为blog框架，Hexo直接将markdown生成静态页面，并用命令就可以直接部署在github page或个人服务器上，使得网站浏览高效，写作过程简单。
但是在使用过程中，每次写作完成都要重新部署`hexo clean && hexo d -g`或者每次更改了博客设置，预览都需要先敲一个`hexo s`让人不爽，作为一名~~又懒又笨的程序员~~，本着可以自动化绝不多敲一行代码的精神，在搜集了多方hexo自动化资料之后终于决定，自己动手(其实是看不懂网上自动化一些工具的教程)。 
## 开始操作
因为前期已经改好博客设置，特别是在`hexo clean && hexo d -g`这一步，已经不需要每次都输入一次密码，所以这次工作流程其实可以简化成:**监听文件夹状态->从文件夹更改状态决定部署博客还是预览博客**，如下图
<img src="https://ws1.sinaimg.cn/large/006tNbRwgy1fwsperk51yj30kk0me75h.jpg" width=70% height=70% align="center"/>
很简单的需求，直接开搞
## 具体代码
在网上搜集资料后，发现使用apache中的common-io包是比较方便的。common-io 2.0以后出的新工具类FileAlteration，其中带listener、observer、monitor。我使用了三个类分别为Watch(继承FileAterationListenerAdaptor)、Exec(使用Runtime.getRuntime().exec实现调用命令)、MainCmd(主函数入口)我这里直接贴代码，有空了再把详解或者注释补上。也可在[Github地址](https://github.com/Ryziii/HexoShell)查看最新代码。

```java
//MainCmd类
package core;

import org.apache.commons.io.monitor.FileAlterationMonitor;
import org.apache.commons.io.monitor.FileAlterationObserver;

import java.io.File;
import java.util.concurrent.TimeUnit;

public class MainCmd {
    static long DeployInterval = TimeUnit.MINUTES.toMillis(10);

    public static void main(String[] args) {
        long ObserverInterval = TimeUnit.SECONDS.toMillis(5);
        String rootDir = "/Users/ryziii/Hexo/";
        Watch watch = new Watch();
        FileAlterationObserver observer = new FileAlterationObserver(new File(rootDir));
        observer.addListener(watch);
        FileAlterationMonitor monitor = new FileAlterationMonitor(ObserverInterval,observer);
        try {
            monitor.start();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```java
//Exec类
package core;

import java.io.IOException;
import java.io.InputStreamReader;
import java.io.LineNumberReader;

public class Exec{

    public Object start(String cmd){
        String[] cmdA = {"zsh","-c",cmd};
        try {
            Process process = Runtime.getRuntime().exec(cmdA);
            if(!cmd.equals("cd ~/hexo\nhexo s")) {
                LineNumberReader br = new LineNumberReader(new InputStreamReader(process.getInputStream()));
                StringBuffer sb = new StringBuffer();
                String line;
                while ((line = br.readLine()) != null) {
//                System.out.println(line);
                    sb.append(line).append("\n");
                }
                if (process != null)
                    process.destroy();
                return sb.toString();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

```java
//Watch类
package core;

import org.apache.commons.io.monitor.FileAlterationListenerAdaptor;

import java.io.File;
import java.util.Date;

public class Watch extends FileAlterationListenerAdaptor {

    private String hexodg = "cd ~/hexo\nhexo clean && hexo d -g";
    private String hexos = "cd ~/hexo\nhexo s";
    private String ki = "lsof -i :4000|grep -v \"PID\"|grep \"node\"|awk '{print \"kill -9\",$2}'|sh";
    private static boolean flag = false;
    private long baseTime;
    private long curTime;

    public Watch() {
        this.baseTime = new Date().getTime();
        this.curTime = new Date().getTime();
    }

    @Override
    public void onFileChange(File file) {
        curTime = new Date().getTime();
        long dif = (curTime - baseTime);
        System.out.printf("%.0fs\n",dif*1.0/1000);

        if (dif >= MainCmd.DeployInterval) {
            flag = false;
            String str = new Exec().start(ki).toString();
            System.out.println(str);
            System.out.println("##################################################################");
            System.out.println("#        File Change more than 10min....Starting Hexo work       #");
            System.out.println("##################################################################");
            baseTime = curTime;
            String str1 = new Exec().start(hexodg).toString();
            System.out.println(str1);
        }else{
            if(flag == false) {
                System.out.println("##################################################################");
                System.out.println("#          未达10min，开启预览，请进入http://localhost:4000      #");
                System.out.println("##################################################################");
                flag = true;
                new Exec().start(hexos);
            }
        }

    }
}
```




