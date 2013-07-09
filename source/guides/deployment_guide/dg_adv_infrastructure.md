---
layout: default
title: "PE Deployment Guide"
subtitle: "Puppetize Your Infrastructure: Advanced Automation"
---

Writing Your Own Modules
-----

[pe_dl]: http://info.puppetlabs.com/download-pe.html


Judy now has most everything in the marketing department under Puppet Enterprise (PE) management, with one exception: the SugarCRM server. Because there is no pre-existing Forge module for SugarCRM, Judy will have to write her own. 

When managing an application, one of the first things to consider is how it gets installed, and what's required for that installation. This understanding will help you write a module that can fully automate every aspect of that application, including ensuring that it is actually present on a given machine. That way, when you need to create a new server for that application, the whole process can be under PE's control and you won't have to repeat steps or go hunting for tarballs on the internet. Bringing up a new application server will become as simple as installing a PE agent and starting a puppet run.

So step one in module writing involves doing some research to get familiar with an application: its prerequisites and dependencies, the download location of the software itself, its installation and configuration processes, etc. To that end, Judy spends a little time on the SugarCRM website reading tech docs. Then she downloads the software and does a test installation, keeping careful notes about the process. With that knowledge in hand, she's ready to start writing her module.

[TODO place in text box] Writing a module means getting to know and understand Puppet's configuration language. There are many resources available to help you with that task. One of the best is to sign up for a Puppet Fundamentals class [TODO link] where you can get hands-on experience and support. But there are many other options. There are numerous resources in Puppet Labs' documentation, including:
[TODO: link list].
You can also get feedback, help, and advice from the Puppet community. [TODO: list of examples]



__________________________________________________
[TODO: move to chapter 3]

Windows MS-SQL
-----

In order to get the marketing department's mailing list server under automation, Judy needs to get PE control of their Windows MS-SQL server. The procedure for doing this is nearly identical to the process we used for the other modules. In this case, however, Judy is going to take the opportunity to replace the old, Windows 2003 machine with a modern, Windows 2008 r2 server. She sets up the box, installs the OS and a puppet agent, and connects it to the master. This is all old hat now. Next, she's going to use a module to install and manage MD-SQL Server. To that end, she'll need the MS installation disc. Thankfully, all the media in the marketing department have been neatly organized and cataloged (this is why you hire interns from liberal arts colleges). She mounts the disc on the Winbox and goes back to her laptop to complete the procedure, much as before.

    * Judy has chosen a Puppet Labs module, which she installs on her master with `puppet module install puppetlabs/mssql`. 
    * Next, she adds the new `mssql` class in the console, and adds it to the node's definition.
    * Then, she uses orchestration's runonce action to kick off a puppet run on the Winbox and get the new class applied, which in turn will install MS-SQL and start it up. She can now migrate the data from the old 2003 machine using the MS-SQL native tools (i.e. the Import and Export Wizard). 
    
With that done, the next step will be to get the CRM machine under PE control. Since there is no Forge module for managing SugarCRM, Judy will have to write her own module. We'll cover that in the next chapter.

Next Steps
-----
Judy now has a basic deployment that is managing some simple services in the marketing department's infrastructure.  Following Judy's example, after [downloading](pe_dl) and setting up PE, you should now be able to find and install Forge modules for basic services, classify nodes using the classes defined by the modules, and use PE to apply configurations to nodes. Some other easy things you might consider managing early on include:

   * sudo 
   * rsyslog
   * vmware tools
   * yumrepo (already defined in PE's core types, no module needed)
 
You should be able to find Forge modules for most of these things. The workflow for installing the modules and adding nodes is essentially the same as we describe above. 
__________________________________________________
