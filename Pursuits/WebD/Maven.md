- it is a build tool and do bundling for you.
manifest file, .jar file, main class, all these files you have to organize and create a zip file is automatically handled by Maven.
- It creates pom file has build instructions in xml format , which can be used to decide which profile to use in it.
- dependency version control can be specified.

![[Pasted image 20260206205058.png|300]]
.m2 file has settings.xml

New Jar required info
<com.spring.xyz>
<.spring>
<1.2>  // version

Repository -> com -> sp2 -> xyz  -> version 1.2
automatically works on lib folder
![[Pasted image 20260206205313.png|300]]
- Do not download jar file again if it is in directory.

It does:
- Versioning
- dependency management
- build tool
- test tool
- profile management

