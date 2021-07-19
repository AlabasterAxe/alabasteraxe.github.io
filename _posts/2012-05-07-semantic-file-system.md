---
id: 6
timestamp: 1336435213
author: "Matt Keller"
title: "How could I write a Semantic File System?"
excerpt: "I don't feel like tree-based file systems are expressive enough! How do we go about building a better one?"
---

If I wanted to write my own file system on Windows it seems like [Dokan](https://github.com/dokan-dev/dokany) would be the tool to use. Instead of writing a system from scratch this provides libraries for implementing a user defined file system. In addition to this I would need to write new file explorer to take advantage of the new information associated with each file.  
  
In addition to my research about generic user defined file systems I also investigated if such a file system had been created. I found a [paper](http://www.hipc.org/hipc2006/posters/semfs.pdf) that talks about implementing many of the features that I imagined would be useful in something called SemFS. In searching for SemFS I was only able to find a web app of the same name. A .war file found [here.](http://code.google.com/p/sem-fs/downloads/detail?name=semfs.war&can=2&q=) A .war file is a web archive file which is used to make deploying a web site easier but it is a Java construct and something that the Apache server that runs on our EC2 instance doesn't handle. If a web version of this was something I would be interested in working on, I would investigate the possibility of installing and forwarding requests for the web app to [Apache Tomcat](http://tomcat.apache.org/whichversion.html).  As I was writing this I decided that, before I write off the only option as installing Tomcat myself, I should investigate something that I had read on a forum that said that I should deploy using Elastic Beanstalk. At first I didn't want to spend effort learning about another Amazon tool but for some reason I changed my mind.  
  
Elastic BeanStalk is just a tool where a user can select, like PHP for example, and upload a web app. It will do all of the configuration for you. In my case, this meant that I was able to create a server and have amazon install Tomcat for me. Unfortunately, when I tried that the webapp didn't work and I never got an explanation as to why. I then installed Tomcat locally (using the installer [here](http://mirror.olnevhost.net/pub/apache/tomcat/tomcat-7/v7.0.27/bin/apache-tomcat-7.0.27.exe)) and tried to run it that way by placing the .war file from before into the webapps folder in the install location in program files. Tomcat serves its pages from there but for some reason it wouldn't recognize the directory. I think most, if not all, of my problems were coming from the fact that I was trying to deploy a web app that is over 3 years old.  
  
**In sum:**  
 - If I ever want to write my own file system, I should investigate Dokan more.  
 - Using java for web looks like it would allow very tight development cycles by using a local ApacheTomcat server.  
- Criticrania might benefit from using Elastic Beanstalk  
- Don't use random 3 year old alpha code unless you want lots of fun(read: mind-numbing) problems to solve.