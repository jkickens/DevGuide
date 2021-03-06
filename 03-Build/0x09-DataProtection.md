# Data Protection

Allocated to AJV

## Background

Data protection is one of the top issues with secure development, and one of the least well developed from an API point of view. 

Various laws and regulations exist to protect user privacy. Users expect their data to be handled well as a baseline requirement, particularly when it comes to the cloud. It is no longer sufficient to protect against SQL injection and consider data protection done. Users expect more from software vendors. Organisations will not trust their data with you unless you have a strong end to end data protection architecture. 

With recent events exposing both mass surveillance of the Internet, as well as the memory scraping attacks favored by attackers, it is important for developers to include countermeasures to protect data at rest, during processing and data in transit. 

## Principles

### Encrypt all data in transit

Ten years ago, it was very common for the majority of applications to be unencrypted. There is still strong resistance to the idea of encrypting all data, but end to end encryption is essential to building trust between you and your users. 

With the collection and analysis of metadata shown to be a clear and present danger to the Internet at large, it is important to ensure that all communications to and from your services are encrypted. This doesn't prevent mass surveillence understanding the size or who connects to your services, but it does prevent basic data leakage, which is very common with older web apps and many mobile applications.

For more information, please see TBA below. 

### Encrypt sensitive data at rest 

Data stored in the cloud, or even bulk data collections require protection from interception and exfiltration. Generally, high value records should be protected, such as:

Data that could be considered a private record under privacy legistlation, which may include (but is not limited to):

* Name, phone, e-mail and address (generally taken together, but refer to your local privacy laws)
* Gender
* Political affliations
* Health records or status
* TBA (need to look at privacy legislation)

It is important to understand that simply using database engine "encryption" facilities does not protect against application level attacks against bulk data stored in the database, nor does it stop database administrators from accessing that data. Therefore, it should be up to the application to ensure that the data being encrypted cannot be viewed or decrypted without obtaining the private key held on the application server. 

This approach allows for safe storage in the cloud, as long the key is not stored with the data. If you store the key with the data, that is called "plain text equivalent" and provides no real protection. 

For more information, please see TBA below and in the cryptography chapter. 

### Protect sensitive data in processing

A common security flaw is direct object references, where a URL design, particularly in RESTful webservices:

http://example.com/webservice/member/32351/edit

But what happens when you change the URL to the following?

http://example.com/webservice/member/32352/edit

If your application does not protect against this issue, which is also the OWASP Top 10 #4 software flaw, data protection is at risk. It is important to enforce direct object reference security wherever a primary key is used to access data. 

For more information, please see TBA below. 

### Clear memory as soon as you're done with it

One of the most common modern attack tecniques is to inject malware into an application, and scrape the application's memory for sensitive data. With a large virtual memory space, this can include the memory allocator's work pages, which are often not zeroed out. This means that if you create a sensitive string in memory, such as a password or a certificate, or a special value such as account roles or balances, an attacker can scrape your memory and obtain these values. 

For more information, please see TBA below. 

## Positive controls 

### Use end to end encryption for data in transit



### Create per-installation encryption keys for data at rest




### Use secure strings


### Use prepared statements,parameterized queries, Active Record, ORMs, or data bindings

As a developer, you should be familiar with the concept of SQL injection (TBA: link to Testing Guide). You can completely avoid SQL injection via the use of prepared statements (also known as paraneterized queries), Active Record data access pattern, or Object Relational Mapping engines (ORMs). 

All major platforms have support for one or more of these safer alternatives to dynamic queries. You should be using them unless you have a very specific requirement for dynamic queries, such as report writing. 

If you have to use dynamic queries, you are responsible for escaping data provided by end users, as this data can be both hostile or accidentally damaging to your database. 

NB: it is not possible to escape table names, SQL DDL (such as "ORDER BY", or "DESC" or "ASC", etc), and so on. If your dyanmic query relies upon user supplied input for this unescapable data, you should strongly validate that data, and review if you could use another data access mechanism, such as prepared statements or an ORM. 

## Unit or Integration Test Cases

### testForEncryption()

Your integration testing should be per

### testvalidDirectObjectReference()

Test your data model to ensure that user A's records can be created, read, updated and deleted by User A. 

For example, create a setUp() that logs in as User A (Alice), and then inserts a record. 

Then for the test, login as User A (Alice), and as Alice try to create a new record, read both records, updates one or both records, and finally deletes Alice's records. 

### testinvalidDirectObjectReference()

Test your data model to ensure that trying to read an invalid data direct object reference does not work. This will prevent an attacker possibly reading the random user data. 

For example, create a setUp() that logs in as User A (Alice) and creates valid records for Alice. 

Then for the test, either don't login, or login as another valid user, such as "


### testvalidDirectObjectReference()

Test your data model to ensure that user A's records can be created, read, updated and deleted by User A. 

For example, create a setUp() that logs in as User A (Alice), and then inserts a record. 

Then for the test, login as User A (Alice), and as Alice try to create a new record, read both records, updates one or both records, and finally deletes Alice's records. 


### testsomeOneElsesDirectObjectReference()

Test your data model to ensure that user A's records cannot be accessed or manipulated by user M. 

For example, create a setUp() that logs in as User A (Alice), and inserts a record. Then for the test, login as User M (Mallory), and as Mallory try to create, read, update or delete Alice's records. 




## Abuse Cases

### Protect against direct object references

## Negative patterns

### Using dynamic queries for SQL or LDAP access



### Control that should never ever appear under pain of infinite nyan cat

e.g. shared knowledge questions or answers, or dynamic SQL queries

## References

***

## Secure strings



## Data retention


## Privacy
## Data at rest controls
## PCI DSS requirements
