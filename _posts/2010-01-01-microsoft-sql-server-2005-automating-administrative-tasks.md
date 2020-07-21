---
id: 35
title: Microsoft SQL Server 2005 – automating administrative tasks
date: 2010-01-01T09:32:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/01/01/microsoft-sql-server-2005-%e2%80%93-automating-administrative-tasks'
permalink: /2010/01/01/microsoft-sql-server-2005-automating-administrative-tasks/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!320')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!320')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SQL Server
---
<div id="msgcns!6E7B9216726D07B8!320" class="bvMsg">
  <p>
    <a href="/wp-content/uploads/2010/10/sqlserver20055b55d.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 15px 0 0;" title="sqlserver2005" border="0" alt="sqlserver2005" align="left" src="/wp-content/uploads/2010/10/sqlserver20055b55d.png?w=290" width="240" height="66" /></a>
  </p>
  
  <li>
    <p>
      <u>SQL Server Agent (~ job server)</u>
    </p>
    
    <p>
      &#8211; po instalaci ma manual start, takze je dobre ho dat na automatic
    </p>
    
    <p>
      &#8211; zodpovedny za veskerou automatizaci v SQL serveru
    </p>
    
    <p>
      &#8211; veskere joby, notifikace a alerty jsou pak v db msdb, takze je dobry ji zalohovat (pokud se poskodi, tak Agent nanastartuje)
    </p>
    
    <p>
      &#8211; configurace agenta:
    </p>
    
    <ul>
      <li>
        <p>
          mail &#8211; konfigurace komponenty databasemail &#8211; zapnout pres Surface Area Configuration, nebo pres SSMS &#8211; Management &#8211; Database Mail &#8211; Configure:
        </p>
        
        <ul>
          <li>
            <p>
              protoze SMTP umi jen odesilat, tak aby mi lidi neodepisovali na ten mail tak nastavim replymail
            </p>
            
            <li>
              <p>
                pocet opakovani odeslani mailu je jako vychozi 1, takze zvysit min. na 3
              </p>
            </li>
          </li>
        </ul>
        
        <li>
          <p>
            zalozka Alert System &#8211; nastavim mnou vytvoreny mail
          </p>
          
          <ul>
            <li>
              <p>
                ucet pod kterym se ale posta odesila je ucet agenta a ten nema na to prava (bug) &#8211; vyresim pres msdb &#8211; security &#8211; role &#8211; database role &#8211; DatabaseMailUserRole &#8211; sem pridat ucet SQL agenta
              </p>
            </li>
          </ul>
          
          <li>
            <p>
              pod SQL server agentem je folder Operators &#8211; New Operator &#8211; vytvorim operatora. Best practice je mit jeste jednoho zalozniho "Fail Safe Operator" a toho nastavim pres Properties SQL agenta v Alert System jako "Enable fail safe operator"
            </p>
          </li>
        </li>
      </li>
    </ul>
    
    <p>
      <u>Job</u>
    </p>
    
    <p>
      &#8211; obsahuje Job Steps, coz jsou jednotlive ulohy Jobu / funguje to tak, ze testuje uspesnost jednotliveho kroku a na zaklade toho jde na dalsi step
    </p>
    
    <p>
      &#8211; pokud nektery krok potrebuje vyssi prava nez ma SQL agent, tak ho spustim jako Proxy account (ten vyrobim pres Proxies v SQL Agentovi)
    </p>
    
    <p>
      &#8211; Job Activity Monitor &#8211; jako vychozi obsahuje 1000 jobu history zpet
    </p>
    
    <p>
      &#8211; mohu ho spustit kdyz je CPU idle, co je CPU idle nastavim v SQL Agentovi
    </p>
    
    <p>
      &#8211; mohu ho spustit i na vice serveru pres Targets &#8211; musim ale nakonfigurovat "Multi Server Administration" v SQL Agentovi
    </p>
    
    <p>
      &#8211; nastavim Schedule
    </p>
    
    <p>
      &#8211; cela konfigurace je v db msdb v tabulce sysjobs (hlavicka jobu) a v tabulce sysjobssteps (telo jobu ~ steps)
    </p>
    
    <p>
      <u>Alerts</u>
    </p>
    
    <p>
      &#8211; 3 typy alertu
    </p>
    
    <p>
      &#8211; na zaklade vzniku alertu mohu spustit Job (execute job)
    </p>
    
    <p>
      <u>Multiserver Administration</u>
    </p>
    
    <p>
      &#8211; MXSOperator
    </p>
    
    <p>
      &#8211; da se spravovat nekolik sql serveru z jednoho
    </p>
    
    <p>
      &#8211; Master Server Wizard +
    </p>
    
    <p>
      &#8211; posilat events na jeden sql ze vsech (event forwarder) ~ SQL agent properties -> Advanced
    </p></p> </p> </p>
  </li>
</div>
