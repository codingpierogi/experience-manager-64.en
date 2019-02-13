---
title: Configuring Acrobat Reader DC extensions for data capture
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: Learn how to configure Acrobat Reader DC extensions for data capture.
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: 075d46f5-8cdd-4e11-a745-d7dbd68747a4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b1568005-9d15-4393-8c2b-405873e55579
index: y
internal: n
snippet: y
---

# Configuring Acrobat Reader DC extensions for data capture{#configuring-acrobat-reader-dc-extensions-for-data-capture}

If users of your AEM forms installation use the data capture functionality of Content Services (Deprecated), it is recommended that you create a role with read-only access for these users.

***note**: Adobe® LiveCycle® Content Services ES (Deprecated) is a content management system installed with LiveCycle. It enables users to design, manage, monitor, and optimize human-centric processes. Content Services (Deprecated) support ends on 12/31/2014. See [Adobe product lifecycle document](http://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). To know about configuring Content Services (Deprecated), see [Administering Content Services](http://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

Data capture requires that you assign a user role to access the SampleReaderExtensionsCredential. You may assign the standard Trust Administrator role, but consider that this role gives general, non-administrative users the powerful administrator privileges that control the PKI Trust settings and manage PKI Credentials, which could compromise the security of your AEM forms installation in a production environment. It is recommended that the AEM forms system administrator create a role that grants only read-only access to the Trust Store, and assign this new role to non-administrator users who use data capture.

## Create a role for data capture users {#create-a-role-for-data-capture-users}

1. In administration console, click Settings &gt; User Management &gt; Role Management, and then click New Role.
1. Enter the role name (for example, Data Capture User) and description in the appropriate fields, then click Next.
1. On the Role Permissions screen, click Find Permissions, then select Credential Read from the list of available permissions.
1. Click OK, then click Finish.

## Assign the data capture role {#assign-the-data-capture-role}

1. In administration console, click Settings &gt; User Management &gt; Role Management, and then click Find.
1. Click the data capture user role you created.
1. On the Role Users/Groups tab, click Find Users/Groups.
1. On the Find Users and Groups screen, click Find, select the users who require the data capture user role, then click OK.
1. On the Edit Role screen, click Save.
