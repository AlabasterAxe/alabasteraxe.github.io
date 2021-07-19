---
id: 17
timestamp: 1337391038
author: "Matt Keller"
title: "How can I recover the data on my EC2 if I've lost the key?"
---

All you need to do is stop(do not terminate!) the messed up instance. From the side panel you should be able to select the EBS(Elastic Block Store) Volumes menu item. Once it has stopped you can detach the drive by right clicking and selecting detach drive.  
  
Now you can create a new EC2 instance(make sure you give it a key that you actually have access to). You need to make sure that in is in the same zone as the last one, otherwise you won't be able to mount the old drive to it. Go back to the EBS Volumes menu. Once the new instance is up and running you'll be able to right click the old drive and select attach this will bring up a dialog box from which you can choose either the original instance or the new instance. If you only see the old instance you probably started the new on in the wrong zone. If you only see the new instance you might have terminated the old instance in which case you might be fucked. Any who. Select the new instance and root it wherever.  
  
Now you should be able to SSH into the new instance if you added a key that you have access to. then you can run  
  
`mount /dev/sdf /whatever/you/named/your/directory`   
  
now you can root around(get it?) this and fix whatever you messed up like authorized_keys or what have you.  
  
### In Sum  
We now have new "OH FUCK" recovery tools for ec2 incase we screw something up when the server is in a state that we really don't want to lose.