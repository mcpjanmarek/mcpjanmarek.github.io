---
id: 36
title: 'Microsoft SQL Server 2005 &#8211; monitoring'
date: 2010-01-01T09:25:00+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/01/01/microsoft-sql-server-2005-monitoring
permalink: /2010/01/01/microsoft-sql-server-2005-monitoring/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!317')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!317')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SQL Server
---
<div id="msgcns!6E7B9216726D07B8!317" class="bvMsg">
  <p>
    <a href="http://janmarek.eu/wp-content/uploads/2010/10/sqlserver20055b45d12724ffc.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 20px 0 0;" title="sqlserver2005" border="0" alt="sqlserver2005" align="left" src="/wp-content/uploads/2010/10/sqlserver20055b45d12724ffc.png?w=290" width="240" height="66" /></a>
  </p>
  
  <ul>
    <li>
      SSMS SQL Server2005 -> Maintenance -> Activity Monitor <li>
        pri vytvareni dotazu se delaji zamky nad db <li>
          pohledy v db &#8211; sys.neco jsou staticke pohledy a sys.dm_neco jsou dynamicke pohledy (jsou v db ->views->system views) <li>
            zjistit fragmentaci indexu pomoci sys.dm_db_index_physical_stats, ktera je ve vsech db <li>
              moje vlastni dotazy si pak mohu dat do vlastniho reportu, ktery si udelam pomoci nastroje SQL Server Business Intelligence Development Studio, ktery je soucasti instalace SQL server2005 SP2 <li>
                merice v OS Performance pro SQL pouzivat <li>
                  monitorujeme tedy CPU, RAM a HDD (navaznosti napr. pokud je malo RAM, tak o to vic se musi zapisovat na HDD a ten muze prestat stihat) <li>
                    <b>SQL Profiler</b> <ul>
                      <li>
                        graf. utilita, instalovat vzdy na PC a ne na srv, vzdy delat vystupy do txt a ne do table (kdyz do table, tak se strasne vytezuje ta db), da se udelat ze zachycenych logu (trace) pak replay na jinem serveru a na nem se pak podivat co se delo; taky se da s timto tracem pustit Tuning Advisor a zjistit workload <li>
                          spustim ho pres Tools &#8211; SQL Profiler; dulezite je vybrat sloupce starttime a endtime (da se pak pouzit i vuci perf logu) &#8211; to udelam tak, ze v trace properties dam SHOW ALL COLUMNS a vyberu ty sloupce; vyberu i db, kterou chci monitorovat &#8211; to udelam v TRace properties pres Filter <li>
                            spustim OS Performance a udelam v perf.logach counterlog na performance &#8211; ten pak mohu po otevreni trace v Profileru, dat v Profileru import perf.logu a dostanu vukon vuci dotazum &#8211; SKVELA VEC!!!
                          </li>
                        </li></ul>
                      </li></li>
                    </ul>
                    
                    <p>
                      <u>Triggers</u>
                    </p>
                    
                    <ul>
                      <li>
                        SQL se deli na <ul>
                          <li>
                            DDL &#8211; Data Definition Language &#8211; prikazy CREATE/ALTER/DROP <li>
                              DML &#8211; Data Manipulation Language &#8211; prikazy SELECT/INSERT/UPDATE/DELETE <li>
                                DCL &#8211; Data Control Language &#8211; prikazy GRANT/DENY/REVOKE
                              </li></ul> 
                              <li>
                                vse se konfiguruje pres TSQL -bez grafickeho rozhrani <li>
                                  nalezaji se v sys.tabulce db sys.triggers <li>
                                    jsou fakticky sp, ale je spousteny systemem <li>
                                      vznikne po udalosti, ktera ho odpali (je reaktivni), ale je soucasti transakce, takze muze pak na konci pouzit napr. rollback, aby operaci vratil <li>
                                        DML trigger (startovan prikazy INSERT/UPDATE/DELETE) &#8211; vztahuje se k table/view <li>
                                          DDL trigger (startovan prikazy CREATE/ALTER/DROP) &#8211; vztahuje se k server/db &#8211; je to udelane takto &#8211; protoze, napr. kdyz udelam create login, tak tento DDL trigger je vlastne DML triggerem nad systemovou tabulkou (v tomto pripade nad db master nad syslogins), (na co se da vsechno delat je v sql books online v DDL triggers v event groups used for firing) <li>
                                            akce, na ktere je povesen trigger, generuje EventData &#8211; na ktere se mohu pak dotazovat v tele triggeru <li>
                                              pokud zakazu v triggeru i DROP, tak ovsem samotny trigger dropnout mohu &#8211; to je vyjimka <li>
                                                prikaz triggeru:
                                              </li>
                                            </li>
                                          </li>
                                        </li>
                                      </li>
                                    </li></ul> 
                                    <p>
                                      <em>USE UserDB </em>
                                    </p>
                                    
                                    <p>
                                      <em>GO </em>
                                    </p>
                                    
                                    <p>
                                      <em>CREATE TRIGGER UserDB_Safety </em>
                                    </p>
                                    
                                    <p>
                                      <em>ON DATABASE </em>
                                    </p>
                                    
                                    <p>
                                      <em>FOR DDL_DATABASE_LEVEL_EVENTS </em>
                                    </p>
                                    
                                    <p>
                                      <em>AS </em>
                                    </p>
                                    
                                    <p>
                                      <em>DECLARE @TSQLCommand nvarchar(max) </em>
                                    </p>
                                    
                                    <p>
                                      <em>SELECT EVENTDATA().value(&#8218;(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]&#8216;,&#8217;nvarchar(max)&#8216;) </em>
                                    </p>
                                    
                                    <p>
                                      <em>WHERE EVENTDATA().value(&#8218;(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]&#8216;,&#8217;nvarchar(max)&#8216;) LIKE &#8218;%STATISTICS%&#8216; </em>
                                    </p>
                                    
                                    <p>
                                      <em>IF @@rowcount = 0 ROLLBACK </em>
                                    </p>
                                    
                                    <p>
                                      <em>GO </em>
                                    </p>
                                    
                                    <p>
                                      <em>CREATE TABLE dbo.myTable (Id INT IDENTITY PRIMARY KEY, eventDetail xml NULL); </em>
                                    </p>
                                    
                                    <p>
                                      <em>UPDATE STATISTICS dbo.UsageLog </em>
                                    </p>
                                    
                                    <p>
                                      <em>&#8211;SELECT * FROM sys.triggers WHERE is_disabled = 0 </em>
                                    </p>
                                    
                                    <p>
                                      <em>ENABLE TRIGGER UserDB_Safety </em>
                                    </p>
                                    
                                    <p>
                                      <em>ON DATABASE</em>
                                    </p>
                                    
                                    <p>
                                      <u>Event Notifications</u>
                                    </p>
                                    
                                    <ul>
                                      <li>
                                        vse se konfiguruje pres TSQL -bez grafickeho rozhrani <li>
                                          vlastne alternativa k SQL profileru <li>
                                            vytvori se na zaklade na nejake udalosti <li>
                                              vyzaduje sluzbu ServiceBroker <li>
                                                ServiceBroker &#8211; soucasti SOA &#8211; Service Orientated Architecture <ul>
                                                  <li>
                                                    aplikace obsahuje svoje casti &#8211; bloky &#8211; a mezi nimi jsou interfaces, ktere umoznuji si vymenovat data, ktere reprezentuji to reseni &#8211; jsou to vlastne zpravy, ktere si mezi sebou posilaji ty sluzby tech bloku <li>
                                                      napr. bloky A a B &#8211; A posle zpravu B a B ji musi ulozit do nejake fronty na sobe (~ buffer => async system) <li>
                                                        B odpovi A a A tuto odpoved ulozi do sve fronty <li>
                                                          ServiceBroker resi sifrovani teto komunikace a jeste to, ze tyto fronty mohou byt na vice serverech <li>
                                                            mohu pak tedy do techto front "strkat" EventData z triggeru, ale to je xml, ktere musim umet <li>
                                                              takovato fronta je pouzita i pri mailovani z SQL &#8211; maily se tam hromadi a pokud se treba do 3h neodeslou tak se smazou
                                                            </li>
                                                          </li>
                                                        </li>
                                                      </li>
                                                    </li></ul> 
                                                    <li>
                                                      postup vyuziti event notif a servicebrokeru <ul>
                                                        <li>
                                                          1. vytvorim schemu <li>
                                                            2. vytvorim frontu (CREATE QUEUE) <li>
                                                              3. vytvorim sluzbu servicebrokeru (CREATE SERVICE) na frontu <li>
                                                                4. vytvorim route (CREATE ROUTE), aby sluzba fungovala mistne <li>
                                                                  5. vytvorim notifikaci <li>
                                                                    cely skript: <li>
                                                                      &#8212; Prepare Database for using with Service Broker service instance
                                                                    </li>
                                                                  </li>
                                                                </li>
                                                              </li>
                                                            </li>
                                                          </li></ul> 
                                                          <p>
                                                            <em>USE userDB </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;Create a queue to receive messages. </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>CREATE QUEUE NotifyQueue ; </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;Create a service on the queue that references </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;the event notifications contract. </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>CREATE SERVICE NotifyService </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ON QUEUE NotifyQueue </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>([http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]); </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;Create a route on the service to define the address </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;to which Service Broker sends messages for the service. </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>CREATE ROUTE NotifyRoute </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>WITH SERVICE_NAME = &#8218;NotifyService&#8216;, </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ADDRESS = &#8218;LOCAL&#8216;; </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;Create the event notification. </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>CREATE EVENT NOTIFICATION myDemoEventNotification </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ON SERVER </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>FOR Audit_Login, Audit_Logout, Audit_Login_Failed </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>TO SERVICE &#8218;NotifyService&#8216;, </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8218;current database&#8216; ;</em>
                                                          </p>
                                                          
                                                          <ul>
                                                            <li>
                                                              v tuto chvili se udeje neco, vygeneruje se zprava a da se do servicebrokerove fronty, z ni to ale potrebuji cist a zapsat do nejake tabulky, takze: <li>
                                                                udela se to tak, ze nad zapisovanim do fronty (coz je vlastne tabulka &#8211; mohu nad ni delat SELECT, jenze zpravy jsou zasifrovane, proto mi SELECT nestaci) se udela trigger a na zaklade neho se to presune do tabulky <li>
                                                                  1. spustim servicebroker na sql serveru (na masterdb) (pozor nesmi byt session k db) <li>
                                                                    2. nactu zpravy z fronty (RECEIVE TOP(1) @msg&#8230;&#8230; ) a toto zacyklim pomoci WHILE (donekonecna &#8230; 1=1), abych nacetl vsechny zpravy fronty az do vyprazdneni a teprve za obdrzenim udelam BREAK (vyskok z WHILE) az bude vse precteno <li>
                                                                      3. po nacteni radky ji zapisuji do tabulky (INSERT INTO &#8230;) <li>
                                                                        4. protoze INSERT muze selhat, bude vlozen do BEGIN TRY a BEGIN TRAN, pricemz COMMIT udelam a bude nasledovat odchyceni chyby pomoci BEGIN CATCH kde pouziji ROLLBACK (a mohu pouzit zobrazeni erroru RAISERROR) <li>
                                                                          5. cele to ulozim jako ulozenou proceduru (sp) (CREATE PROCEDURE) <li>
                                                                            6. nastavim frontu tak, aby spoustela tuto proceduru (ALTER QUEUE WITH ACTIVATION &#8230;) <li>
                                                                              cely skript:
                                                                            </li>
                                                                          </li>
                                                                        </li>
                                                                      </li>
                                                                    </li>
                                                                  </li>
                                                                </li></ul>
                                                              </li>
                                                            </li></li> </li> </li>
                                                          </ul>
                                                          
                                                          <p>
                                                            <em>USE Master </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ALTER DATABASE UserDB SET ENABLE_BROKER </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>USE UserDB </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>CREATE PROCEDURE dbo.usp_ParseLog </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>AS </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>DECLARE @msg_body XML </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em></em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>WHILE (1=1) </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>BEGIN </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>RECEIVE TOP(1) @msg_body = message_body </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>FROM dbo.NotifyQueue </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>IF @@rowcount = 0 BREAK </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>BEGIN TRY </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>BEGIN TRAN </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>INSERT INTO dbo.UsageLog (detail) VALUES (@msg_body) </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>COMMIT TRAN </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>END TRY </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>BEGIN CATCH </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8211;RAISERROR () </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ROLLBACK </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>END CATCH </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>END &#8212; END WHILE </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>GO </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8212; SELECT * FROM dbo.NotifyQueue </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>&#8212; EXEC dbo.usp_ParseLog </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>ALTER QUEUE dbo.NotifyQueue </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>WITH ACTIVATION ( </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>PROCEDURE_NAME = dbo.usp_ParseLog, </em>
                                                          </p>
                                                          
                                                          <p>
                                                            <em>EXECUTE AS SELF) ;</em>
                                                          </p>
                                                          
                                                          <ul>
                                                            <li>
                                                              pokud bych chtel logovat audit vseho na celem serveru, pak v options na serveru zapnu ENABLE C2 AUDIT TRACING
                                                            </li>
                                                          </ul></div>

