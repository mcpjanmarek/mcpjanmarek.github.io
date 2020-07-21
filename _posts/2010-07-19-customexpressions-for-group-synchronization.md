---
id: 1207
title: CustomExpressions for Group Synchronization
date: 2010-07-19T11:38:19+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/07/19/customexpressions-for-group-synchronization
permalink: /2010/07/19/customexpressions-for-group-synchronization/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!365')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!365')?authkey=EpZNAU0huAk%24"
categories:
  - Identity Manager
  - Nezařazené
tags:
  - FIM
---
<div id="msgcns!6E7B9216726D07B8!365" class="bvMsg">
  <p>
    <a href="https://qocjma.blu.livefilestore.com/y1mDmQd2pwmO7Ivaq76V3sF26-uf3qjGEsmyCUiPKPyCP6HlTw5t0S6HzxwfYX9lzIxk7tCLcIHe_dOg8NCCYt60XvhXdyE0GkdvX2VyzOGTd0D7vpma_prpmw3gD9IztXoPh5gFnMjju58AqVeRWsVpw/fim[5].png?download&psid=1"><img title="fim" src="https://qocjma.blu.livefilestore.com/y1mNPkECBxuPHcTTogcCWqvh8cMYMEr0f69yX_r7Vx_LoFL0GdOEqNZC1fA0TL9mmG6F_ZgRCGjuAJf0k9h7ZGQiQ7HkpoAsjQYpxbITvOxYZUYEv-kh-Bj9q-Ej0JxQ3P8Lal-14p01D140_99meYl9Q/fim_thumb[3].png?download&psid=1" alt="fim" width="240" height="77" align="left" border="0" /></a>
  </p>
  
  <p>
    I found mistakes in one guide of Microsoft “How Do I Guides” for FIM 2010. There are mistakes in the <strong>Synchronization Rule</strong> for Group sync in the <strong>Inbound Attribute Flow</strong> in the <strong>custom expression</strong> related to <strong>scope</strong> and <strong>type </strong>attribute. The right custom expressions are as follows:
  </p>
  
  <p>
    CustomExpression for SCOPE Attribute:
  </p>
  
  <p>
    <strong>IIF(Eq(BitAnd(2,groupType),2),&#8220;Global&#8220;,IIF(Eq(BitAnd(4,groupType),4),&#8220;DomainLocal&#8220;,&#8220;Universal&#8220;))</strong>
  </p>
  
  <p>
    Microsoft has 3 brackets in the end, but there must be only 2 <img style="border-style: none;" src="/wp-content/uploads/2010/10/wlemoticon-winkingsmile5b25d.png?w=19" alt="Winking smile" />
  </p>
  
  <p>
    CustomExpression for TYPE Attribute:
  </p>
  
  <p>
    <strong>IIF(Eq(BitOr(14,groupType),14),&#8220;Distribution&#8220;,&#8220;Security&#8220;)</strong>
  </p>
  
  <p>
    Microsoft has 2 brackets in the end, but there must be only 1 <img style="border-style: none;" src="/wp-content/uploads/2010/10/wlemoticon-winkingsmile5b25d.png?w=19" alt="Winking smile" />
  </p>
</div>
