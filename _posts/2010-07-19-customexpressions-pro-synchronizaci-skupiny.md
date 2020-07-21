---
id: 1219
title: CustomExpressions pro synchronizaci skupiny
date: 2010-07-19T11:38:19+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/07/19/customexpressions-for-group-synchronization
permalink: /2010/07/19/customexpressions-pro-synchronizaci-skupiny/
categories:
  - Nezařazené
  - Uncategorized
---
<div id="msgcns!6E7B9216726D07B8!365" class="bvMsg">
  <p>
    <a href="https://qocjma.blu.livefilestore.com/y1mDmQd2pwmO7Ivaq76V3sF26-uf3qjGEsmyCUiPKPyCP6HlTw5t0S6HzxwfYX9lzIxk7tCLcIHe_dOg8NCCYt60XvhXdyE0GkdvX2VyzOGTd0D7vpma_prpmw3gD9IztXoPh5gFnMjju58AqVeRWsVpw/fim[5].png?download&psid=1"><img title="FIM" src="https://qocjma.blu.livefilestore.com/y1mNPkECBxuPHcTTogcCWqvh8cMYMEr0f69yX_r7Vx_LoFL0GdOEqNZC1fA0TL9mmG6F_ZgRCGjuAJf0k9h7ZGQiQ7HkpoAsjQYpxbITvOxYZUYEv-kh-Bj9q-Ej0JxQ3P8Lal-14p01D140_99meYl9Q/fim_thumb[3].png?download&psid=1" alt="FIM" width="240" height="77" align="left" border="0" /></a>
  </p>
  
  <p>
    Našla jsem chyby v jedné příručce Microsoft "Jak udělat I vodítka" FIM 2010. Tam jsou chyby v synchro<strong>nizaci pravidlo pr</strong>o skupinu synchronizac<strong>e v vstupní atribut t</strong>ok v vl<strong>astního výrazu t</strong>ýkající se <strong>rozsa</strong>hu a<strong> typu</strong> atributu. Doprava vlastní výrazy jsou následující:
  </p>
  
  <p>
    CustomExpression pro atribut SCOPE:
  </p>
  
  <p>
    <strong>IIF(EQ(BitAnd(2,groupType),2),"Global",IIF(EQ(BitAnd(4,groupType),4),"DomainLocal","Universal"))</strong>
  </p>
  
  <p>
    Microsoft má 3 držáky na konci, ale musí existovat pouze 2 <img style="border-style: none;" src="http://janmarek.eu/wp-content/uploads/2010/10/wlemoticon-winkingsmile5b25d.png?w=19" alt="Mrkající Veselý obličej" />
  </p>
  
  <p>
    CustomExpression pro typ atributu:
  </p>
  
  <p>
    <strong>IIF(EQ(BitOr(14,groupType),14),"Distribution","Security")</strong>
  </p>
  
  <p>
    Microsoft má 2 držáky na konci, ale musí existovat pouze 1 <img style="border-style: none;" src="http://janmarek.eu/wp-content/uploads/2010/10/wlemoticon-winkingsmile5b25d.png?w=19" alt="Mrkající Veselý obličej" />
  </p>
</div>