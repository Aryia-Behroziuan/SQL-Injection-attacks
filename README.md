# SQL-Injection-attacks
SQL Injection attack is the most common website hacking technique. Most websites use Structured Query Language (SQL) to interact with databases. SQL allows the website to create, retrieve, update, and delete database records. It used for everything from logging a user into the website to storing details of an eCommerce transaction.  An SQL injection attack places SQL into a web form in an attempt to get the application to run it. For example, instead of typing plain text into a username or password field, a hacker may type in ‘ OR 1=1.  If the application appends this string directly to an SQL command that is designed to check if a user exists in the database, it will always return true. This can allow a hacker to gain access to a restricted section of a website. Other SQL injection attacks can be used to delete data from the database or insert new data.  Hackers sometimes use automated tools to perform SQL injections on remote websites. They will scan thousands of websites, testing many types of injection attacks until they are successful.  SQL injection attacks can be prevented by correctly filtering user input. Most programming languages have special functions to safely handle user input that is going to be used in an SQL query.


<div class="col-12 col-lg-7">
                    <div class="post-title">
                        <h1>SQL (Structured query language) Injection</h1>
                        <div class="post-stats">
                                                                                        <span class="view-count">324.3k views</span>
                                                        <div class="holder">
                                <span class="hero-tags">
                                    <a class="" target="_self" href="https://www.imperva.com/learn/application-security/">App Security</a><span>Threats</span>                                </span>
                                <div class="share-icon-bar"><!-- Facebook -->
                            <div class="fl-fl float-fb transition-active">
                                <a href="http://www.facebook.com/sharer.php?u=https%3A%2F%2Fwww.imperva.com%2Flearn%2Fapplication-security%2Fsql-injection-sqli%2F" target="_blank" event-action="Click" event-label="SQL (Structured query language) Injection" gtm-track=""><i class="fa fa-facebook"></i></a>
                            </div><!-- Twitter -->
                            <div class="fl-fl float-tw transition-active">
                                <a href="https://twitter.com/share?url=https%3A%2F%2Fwww.imperva.com%2Flearn%2Fapplication-security%2Fsql-injection-sqli%2F&amp;text=SQL (Structured query language) Injection&amp;hashtags=ImpervaResources" target="_blank" event-action="Click" event-label="SQL (Structured query language) Injection" gtm-track=""><i class="fa fa-twitter"></i></a>
                            </div><!-- LinkedIn -->
                            <div class="fl-fl float-li transition-active">
                                <a href="http://www.linkedin.com/shareArticle?mini=true&amp;url=https%3A%2F%2Fwww.imperva.com%2Flearn%2Fapplication-security%2Fsql-injection-sqli%2F" target="_blank" event-action="Click" event-label="SQL (Structured query language) Injection" gtm-track=""><i class="fa fa-linkedin"></i></a>
                            </div></div>                            </div>
                        </div>
                    </div>
                    <div class="article-content">
                        <h2 id="what-is-sql-injection" class="section-active">What is SQL injection</h2>
<p>SQL injection, also known as SQLI, is a common attack vector that uses malicious SQL code for backend database manipulation to access information that was not intended to be displayed. This information may include any number of items, including sensitive company data, user lists or private customer details.</p>
<p>The impact SQL injection can have on a business is far-reaching. A successful attack may result in the unauthorized viewing of user lists, the deletion of entire tables and, in certain cases, the <a class="inlinks" href="https://www.imperva.com/learn/application-security/ethical-hacking/">attacker</a> gaining administrative rights to a database, all of which are highly detrimental to a business.</p>
<p>When calculating the potential cost of an SQLi, it’s important to consider the loss of customer trust should personal information such as phone numbers, addresses, and credit card details be stolen.</p>
<p>While this vector can be used to attack any SQL database, websites are the most frequent targets.</p>
<h2 id="what-are-sql-queries" class="">What are SQL queries</h2>
<p>SQL is a standardized language used to access and manipulate databases to build customizable data views for each user. SQL queries are used to execute commands, such as data retrieval, updates, and record removal. Different SQL elements implement these tasks, e.g., queries using the SELECT statement to retrieve data, based on user-provided parameters.</p>
<p>A typical eStore’s SQL database query may look like the following:</p>
<pre>SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = ItemNumber</pre>
<p>From this, the web application builds a string query that is sent to the database as a single SQL statement:</p>
<pre>sql_query= "
SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = " &amp; Request.QueryString("ItemID")</pre>
<p>A user-provided input&nbsp;<span class="url-example">http://www.estore.com/items/items.asp?itemid=999</span>&nbsp;can then generates the following SQL query:</p>
<pre>SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = 999</pre>
<p>As you can gather from the syntax, this query provides the name and description for item number 999.</p>
<h2 id="types-of-sql-injections">Types of SQL Injections</h2>
<p>SQL injections typically fall under three categories: In-band SQLi (Classic), Inferential SQLi (Blind) and Out-of-band SQLi. You can classify SQL injections types based on the methods they use to access backend data and their damage potential.</p>
<h3><strong>In-band SQLi</strong></h3>
<p>The attacker uses the same channel of communication to launch their attacks and to gather their results. In-band SQLi’s simplicity and efficiency make it one of the most common types of SQLi attack. There are two sub-variations of this method:</p>
<ul>
<li><strong>Error-based SQLi</strong>—the attacker performs actions that cause the database to produce error messages. The attacker can potentially use the data provided by these error messages to gather information about the structure of the database.</li>
<li><strong>Union-based SQLi</strong>—this technique takes advantage of the UNION SQL operator, which fuses multiple select statements generated by the database to get a single HTTP response. This response may contain data that can be leveraged by the attacker.</li>
</ul>
<h3><strong>Inferential (Blind) SQLi</strong></h3>
<p>The attacker sends data payloads to the server and observes the response and behavior of the server to learn more about its structure. This method is called blind SQLi because the data is not transferred from the website database to the attacker, thus the attacker cannot see information about the attack in-band.</p>
<p>Blind SQL injections rely on the response and behavioral patterns of the server so they are typically slower to execute but may be just as harmful. Blind SQL injections can be classified as follows:</p>
<ul>
<li><strong>Boolean</strong>—that attacker sends a SQL query to the database prompting the application to return a result. The result will vary depending on whether the query is true or false. Based on the result, the information within the HTTP response will modify or stay unchanged. The attacker can then work out if the message generated a true or false result.</li>
<li><strong>Time-based</strong>—attacker sends a SQL query to the database, which makes the database wait (for a period in seconds) before it can react. The attacker can see from the time the database takes to respond, whether a query is true or false. Based on the result, an HTTP response will be generated instantly or after a waiting period. The attacker can thus work out if the message they used returned true or false, without relying on data from the database.</li>
</ul>
<h3><strong>Out-of-band SQLi</strong></h3>
<p>The attacker can only carry out this form of attack when certain features are enabled on the database server used by the web application. This form of attack is primarily used as an alternative to the in-band and inferential SQLi techniques.</p>
<p>Out-of-band SQLi is performed when the attacker can’t use the same channel to launch the attack and gather information, or when a server is too slow or unstable for these actions to be performed. These techniques count on the capacity of the server to create DNS or HTTP requests to transfer data to an attacker.</p>
<h2 id="sql-injection-example">SQL injection example</h2>
<p>An attacker wishing to execute SQL injection manipulates a standard SQL query to exploit non-validated input <a class="inlinks" href="https://www.imperva.com/learn/application-security/vulnerability-management/">vulnerabilities</a> in a database. There are many ways that this attack vector can be executed, several of which will be shown here to provide you with a general idea about how SQLI works.</p>
<p>For example, the above-mentioned input, which pulls information for a specific product, can be altered to read&nbsp;<span class="url-example">http://www.estore.com/items/items.asp?itemid=999 or 1=1</span>.</p>
<p>As a result, the corresponding SQL query looks like this:</p>
<pre>SELECT ItemName, ItemDescription
FROM Items
WHERE ItemNumber = 999 OR 1=1</pre>
<p>And since the statement 1 = 1 is always true, the query returns all of the product names and descriptions in the database, even those that you may not be eligible to access.</p>
<p>Attackers are also able to take advantage of incorrectly filtered characters to alter SQL commands, including using a semicolon to separate two fields.</p>
<p>For example, this input&nbsp;<span class="url-example">http://www.estore.com/items/iteams.asp?itemid=999; DROP TABLE Users</span>&nbsp;would generate the following SQL query:</p>
<pre>SELECT ItemName, ItemDescription
FROM Items
WHERE ItemNumber = 999; DROP TABLE USERS</pre>
<p>As a result, the entire user database could be deleted.</p>
<p>Another way SQL queries can be manipulated is with a UNION SELECT statement. This combines two unrelated SELECT queries to retrieve data from different database tables.</p>
<p>For example, the input&nbsp;<span class="url-example">http://www.estore.com/items/items.asp?itemid=999 UNION SELECT user-name, password FROM USERS</span>&nbsp;produces the following SQL query:</p>
<pre>SELECT ItemName, ItemDescription
FROM Items
WHERE ItemID = '999' UNION SELECT Username, Password FROM Users;</pre>
<p>Using the UNION SELECT statement, this query combines the request for item 999’s name and description with another that pulls names and passwords for every user in the database.</p>
<h2 id="sql-injection-combined-with-os-command-execution-the-accellion-attack">SQL injection combined with OS Command Execution: The Accellion Attack</h2>
<p>Accellion, maker of File Transfer Appliance (FTA), a network device widely deployed in organizations around the world, and used to move large, sensitive files. The product is over 20 years old and is now at end of life.</p>
<p>FTA was the subject of a unique, highly sophisticated attack combining SQL injection with operating system command execution. Experts speculate the Accellion attack was carried out by hackers with connections to the <a href="https://www.imperva.com/blog/dont-be-a-victim-of-cyber-extortion/">financial crimes group</a> FIN11, and ransomware group Clop.</p>
<p>The attack demonstrates that SQL injection is not just an attack that affects web applications or web services, but can also be used to compromise back-end systems and <a href="https://www.imperva.com/blog/the-latest-multistage-attacks-demonstrate-the-need-to-secure-the-data-layer/">exfiltrate data</a>.</p>
<h3>Who was affected by the attack?</h3>
<p>The Accellion exploit is a <a href="https://www.imperva.com/learn/application-security/supply-chain-attack/">supply chain attack</a>, affecting numerous organizations that had deployed the FTA device. These included the Reserve Bank of New Zealand, the State of Washington, the Australian Securities and Investments Commission, telecommunication giant Singtel, and security software maker Qualys, as well as numerous others.</p>
<h3>Accelion Attack flow</h3>
<p>According to a report commissioned by Accellion, the combination SQLi and command execution attack worked as follows:</p>
<ol>
<li aria-level="1">Attackers performed SQL Injection to gain access to document_root.html, and retrieved encryption keys from the Accellion FTA database.</li>
<li aria-level="1">Attackers used the keys to generate valid tokens, and used these tokens to gain access to additional files</li>
<li aria-level="1">Attackers exploited an operating system command execution flaw in the sftp_account_edit.php file, allowing them to execute their own commands</li>
<li aria-level="1">Attackers created a web shell in the server path /home/seos/courier/oauth.api</li>
<li aria-level="1">Using this web shell, they uploaded a custom, full-featured web shell to disk, which included highly customized tooling for exfiltration of data from the Accellion system. The researchers named this shell DEWMODE.</li>
<li aria-level="1">Using DEWMODE, the attackers extracted a list of available files from a MySQL database on the Accellion FTA system, and listed files and their metadata on an HTML page</li>
<li aria-level="1">The attackers performed file download requests, which contained requests to the DEWMODE component, with encrypted and encoded URL parameters.</li>
<li aria-level="1">DEWMODE is able to accept these requests and then delete the download requests from the FTA web logs.</li>
</ol>
<p>This raises the profile of SQL injection attacks, showing how they can be used as a gateway for a much more damaging attack on critical corporate infrastructure.</p>
<h2 id="sqli-prevention-and-mitigation">SQLI prevention and mitigation</h2>
<p>There are several effective ways to prevent SQLI attacks from taking place, as well as protecting against them, should they occur.</p>
<p>The first step is input validation (a.k.a. sanitization), which is the practice of writing code that can identify illegitimate user inputs.</p>
<p>While input validation should always be considered best practice, it is rarely a foolproof solution. The reality is that, in most cases, it is simply not feasible to map out all legal and illegal inputs—at least not without causing a large number of false positives, which interfere with user experience and an application’s functionality.</p>
<p>For this reason, a web application firewall (WAF) is commonly employed to filter out SQLI, as well as other online threats. To do so, a WAF typically relies on a large, and constantly updated, list of meticulously crafted signatures that allow it to surgically weed out malicious SQL queries. Usually, such a list holds signatures to address specific attack vectors and is regularly patched to introduce blocking rules for newly discovered vulnerabilities.</p>
<p>Modern web application firewalls are also often integrated with other security solutions. From these, a <a href="/products/web-application-firewall-waf/">WAF</a> can receive additional information that further augments its security capabilities.</p>
<p>For example, a web application firewall that encounters a suspicious, but not outright malicious input may cross-verify it with IP data before deciding to block the request. It only blocks the input if the IP itself has a bad reputational history.</p>
<p>Imperva&nbsp;<a href="/products/cloud-waf/" target="_blank" rel="noopener noreferrer">cloud-based WAF</a> uses signature recognition, IP reputation, and other security methodologies to identify and block SQL injections, with a minimal amount of false positives. The WAF’s capabilities are augmented by <a href="https://www.imperva.com/blog/incaprules-optimized-application-security" target="_blank" rel="noopener noreferrer">IncapRules</a>—a custom security rule engine that enables granular customization of default security settings and the creation of additional case-specific security policies.</p>
<p>Our WAF also employs crowdsourcing techniques that ensure that new threats targeting any user are immediately propagated across the entire user-base. This enables rapid response to newly disclosed vulnerability and <a href="/learn/application-security/zero-day-exploit/">zero-day threats</a>.</p>
<div class="ddos-banner"><div class="wrap"><p>See how Imperva <a class="inlinks" href="https://www.imperva.com/learn/application-security/what-is-web-application-firewall-waf/">Web Application Firewall can help you with SQL injections</a>.</p>
<div class="cta-container">
                                                    <a class="impv-yellow-btn" event-action="Click" event-category="LC Banner" event-label="Request demo" gtm-track="" target="_self" href="javascript:openModal('modalid3533', '/learn/banner/virtual/request-demo/', 'Personal Demo Request | Imperva');">Request demo</a>
                                                    <a class="gst-yellow-dark-text-btn" event-action="Click" event-category="LC Banner" event-label="Learn more" gtm-track="" target="_self" href="https://www.imperva.com/products/web-application-firewall-waf/">Learn more</a>
                                                </div></div></div><h2 id="adding-datacentric-protection-for-defense-in-depth">Adding Data-Centric Protection for Defense in Depth</h2>
<p>The optimal defense is a layered approach that includes <a href="https://www.imperva.com/resources/resource-library/datasheets/defending-against-complex-data-centric-attacks/">data-centric strategies</a> that focus on protecting the data itself, as well as the network and applications around it. Imperva <a href="https://www.imperva.com/products/database-security/">Database Security</a> continuously discovers and classifies sensitive data to identify how much sensitive data there is, where it is stored, and whether it’s protected.</p>
<p>In addition, Imperva Database Security <a href="https://www.imperva.com/products/data-risk-analytics/">actively monitors data access activity</a> to identify any data access behavior that is a risk or violates policy, regardless of whether it originates with a network SQL query, a compromised user account, or a malicious insider. Receive automatic notification of a security event so you can respond quickly with security analytics that provides a clear explanation of the threat and enables immediate initiation of the response process, all from a single platform.</p>
<p>Database security is a critical last line of defense to preventing hacks like SQLi. Imperva’s unique approach to protecting data encompasses a complete view of both the web application and data layer.</p>
                    </div>
                </div>


