---
id: 959
title: Dual Boot s Hyper-V a bez Hyper-V
date: 2015-08-04T20:44:56+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=959
permalink: /2015/08/04/dual-boot-s-hyper-v-a-bez-hyper-v/
apss_content_flag:
  - "0"
  - "0"
accesspress_mag_post_template_layout:
  - global-template
  - global-template
accesspress_mag_sidebar_layout:
  - global-sidebar
  - global-sidebar
categories:
  - Hyper-V
  - Nezařazené
---
Cože to? Proč? No je to easy &#8211; když chcete používat na kompu Hyper-V spolu s dalším virtualizačním softem, třeba s VMware Workstation, jako já, tak se to vzájemně hádá o hardware virtualizaci. Abyste teda nemuseli pořád odinstalovávat Hyper-V, resp. ten druhý soft, tak stačí si udělat dual boot, který ale neloaduje různé OS, ale ten samý, jen jednou s hypervisorem a podruhé bez něj.

Už to nějakou dobu používám (vlastně od Windows 8, kdy přišlo Client Hyper-V).

Stačí si do CMDčka hodit tyhle příkazy a je to:

1. tohle vypne na aktuálním boot záznamu Hyper-V  
_C:\WINDOWS\system32>**bcdedit /set {current} hypervisorlaunchtype off**_  
_The operation completed successfully._

2. tohle pak zkopíruje aktuální boot record a pojmenuje ho (to IDčko, které ten command vyhodí, použijete v dalším příkazu)  
_C:\WINDOWS\system32>**bcdedit /copy {current} /d &#8222;Windows 10 with Hyper-V&#8220;**_  
_The entry was successfully copied to {<span style="color: #ff0000;">6bbd723f-324f-11e5-9b0d-fd4bac592e19</span>}._

3. no a toto nakonec povolí na tom novém boot záznamu Hyper-V  
_C:\WINDOWS\system32>**bcdedit /set {<span style="color: #ff0000;">6bbd723f-324f-11e5-9b0d-fd4bac592e19</span>}** hypervisorlaunchtype auto_  
_The operation completed successfully._

That&#8217;s all 🙂
