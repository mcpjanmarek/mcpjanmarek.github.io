---
id: 1205
title: How to increase size of differencing disk
date: 2010-07-30T12:44:57+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/07/30/how-to-increase-size-of-differencing-disk
permalink: /2010/07/30/how-to-increase-size-of-differencing-disk/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!374')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!374')?authkey=EpZNAU0huAk%24"
categories:
  - Hyper-V
  - Nezařazené
tags:
  - Hyper-V
  - VHD(X)
---
<div id="msgcns!6E7B9216726D07B8!374" class="bvMsg">
  <div>
    &#8211; shutdown virtual machine
  </div>
  
  <div>
    &#8211; start Hyper-V Manager and modify virtual machine&#8217;s properties
  </div>
  
  <div>
    &#8211; select virtual differencing disk to increasing
  </div>
  
  <div>
    &#8211; click on Edit button and select Merge
  </div>
  
  <div>
    &#8211; in the Merge action wizard select Merge to new virtual harddisk and put in the the name of the new virtual harddisk
  </div>
  
  <div>
    &#8211; then you can select whether it will be fixed or dynamically expanding disk
  </div>
  
  <div>
    &#8211; finish the Merge wizard
  </div>
  
  <div>
  </div>
  
  <div>
    &#8211; now you have a new virtual harddisk
  </div>
  
  <div>
  </div>
  
  <div>
    &#8211; modify virtual machine&#8217;s properties and change the path for the virtual harddisk to a newly created virtual harddisk
  </div>
  
  <div>
    &#8211; confirm changes
  </div>
  
  <div>
  </div>
  
  <div>
    &#8211; now the virtual machine has a new fixed/dynamically expanding disk
  </div>
  
  <div>
  </div>
  
  <div>
    &#8211; modify virtual machine&#8217;s properties and select virtual disk and click on Edit button
  </div>
  
  <div>
    &#8211; select Expand action and finish the wizard with your values
  </div>
  
  <div>
  </div>
  
  <div>
    &#8211; start operating system and go to Storage &#8211; Disk Management in the Server Manager
  </div>
  
  <div>
    &#8211; you should see a unallocated freespace in there, so select the existing partition and select Expand disk action
  </div>
  
  <div>
  </div>
  
  <div>
    How simple! 🙂
  </div>
</div>

