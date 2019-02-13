---
title: Importing and exporting the configuration file
seo-title: Importing and exporting the configuration file
description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 75b4db85-5da3-4f22-a1a5-23112766522b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a1bfbc5c-03c7-4860-a751-e80c5c6ca9c0
index: y
internal: n
snippet: y
---

# Importing and exporting the configuration file{#importing-and-exporting-the-configuration-file}

Use the Manual Configuration page to download a copy of the configuration settings in XML format. The settings in this file control all server preferences. You can then edit the file and upload it back to the server. You can also use the file to configure another AEM forms product instance.

To avoid security risks, the bind password value for the directory server is not included in an exported configuration file. Update the password in the XML file before you import the file to a new system.

>[!NOTE]
>
>Importing the configuration file reconfigures AEM forms based on the information in the file. Only a system administrator or a professional services consultant who is familiar with the AEM forms product and XML should consider modifying the configuration file. They may need to edit the configuration file, for example, to reconfigure a corrupted setting.

**Export the configuration information**

1. In Administration Console, click Settings &gt; User Management &gt; Configuration &gt; Import And Export Configuration Files.
1. Click Export. If you are using Microsoft Internet Explorer, you are prompted to specify a location to save the file. If you are using Firefox, the file is saved on your desktop.

**Import the configuration information**

1. In Administration Console, click Settings &gt; User Management &gt; Configuration &gt; Import And Export Configuration Files.
1. Click Browse to find the configuration file, click Import, and then click OK.
