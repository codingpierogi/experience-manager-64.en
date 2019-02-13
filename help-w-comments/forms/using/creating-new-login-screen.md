---
title: Creating a new login screen
seo-title: Creating a new login screen
description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: 36bb0384-c990-4a20-b400-e1b6c9d3c922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 17537e8d-d158-47ec-94aa-988b39c13b61
index: y
internal: n
snippet: y
---

# Creating a new login screen{#creating-a-new-login-screen}

You can modify the login screen of all AEM Forms modules that use the AEM Forms login screen. For example, the modifications affect the login screen of, both, Forms Manager and AEM Forms workspace.

### Prerequisite {#prerequisite}

1. Log in at `/lc/crx/de` with Administrator permissions.
1. Perform the following actions:

    1. Replicate the hierarchical structure: of `/libs/livecycle/core/content` at `/apps/livecycle/core/content`. Maintain the same (node/folder) properties and access control.
    
    1. Copy the content folder: from `/libs/livecycle/core` to `/apps/livecycle/core`.  
    
    1. Delete the contents of `/apps/livecycle/core` folder.

1. Perform these actions:

    1. Replicate the hierarchical structure: of `/libs/livecycle/core/components/login` at `/apps/livecycle/core/components/login`. Maintain the same (node/folder) properties and access control.
    
    1. Copy the components folder: from `/libs/livecycle/core` to `/apps/livecycle/core`.  
    
    1. Delete the contents of the folder: `/apps/livecycle/core/components/login`.

### Adding a new locale {#adding-a-new-locale}

1. Copy the `i18n` folder:

    * from `/libs/livecycle/core/components/login`
    * to `/apps/livecycle/core/components/login`

1. Delete all the folders inside `i18n` except one, say `en`.
1. On the folder `en`, perform these actions:

    1. Rename the folder to the locale name you wish to support. For example, `ar`.
    1. Change the property `jcr:language` value to `ar`(for the `ar` folder).

   >[!NOTE]
   >
   >If locale is a language-country code combination, say, `ar-DZ`, then change the folder name and property value to `ar-DZ`.

1. Copy `login.jsp`:

    * from `/libs/livecycle/core/components/login` 
    * to `/apps/livecycle/core/components/login`

1. Modify the following snippet of code for `/apps/livecycle/core/components/login/login.jsp`:

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ```
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)
   
   To
   
   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
   ```

### Adding new text, or modifying existing text {#adding-new-text-or-modifying-existing-text}

1. Copy `i18n` folder:

    * from `/libs/livecycle/core/components/login`
    * to `/apps/livecycle/core/components/login`

1. Now modify the value of the property `sling:message` of the node (under the desired locale code folder) for which you wish to change the text. Translation is done via the key mentioned in the value of `sling:key` property of the node.
1. For adding new key-value pair, perform the following actions. Check an example in the screenshot that follows.

    1. Create a node of type `sling:MessageEntry`, or copy an existing node and rename it, under all the locale folders.
    1. Copy `login.jsp` :

        * from `/libs/livecycle/core/components/login`  
        
        * to `/apps/livecycle/core/components/login`

    1. Modify `/apps/livecycle/core/components/login/login.jsp` to incorporate the newly added text.

   ![](assets/capture.png) 

   ```
   div class="loginContent">
                       <span class="loginFlow"></span>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></span>
                       <span class="loginTitle"><%= i18n.get("Login") %></span>
                       <% if (loginFailed) {%>
   
   To
   
   div class="loginContent">
                       <span class="loginFlow"></span>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></span>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></span>
                       <span class="loginTitle"><%= i18n.get("Login") %></span>
                       <% if (loginFailed) {%>
   ```

### Adding new style, or modifying existing style {#adding-new-style-or-modifying-existing-style}

1. Copy `login` node:

    * from `/libs/livecycle/core/content` 
    * to `/apps/livecycle/core/content`

1. Delete files `login.js` and `jquery-1.8.0.min.js`, from the node `/apps/livecycle/core/content/login.`
1. Modify the styles in the CSS file.
1. To add new styles:

    1. Add new styles to `/apps/livecycle/core/content/login/login.css`
    1. Copy `login.jsp`

        * from `/libs/livecycle/core/components/login`  
        
        * to `/apps/livecycle/core/components/login`

    1. Modify `/apps/livecycle/core/components/login/login.jsp` to incorporate the newly added styles.

1. For example:

    * Add the following to `/apps/livecycle/core/content/login/login.css`.

   ```css
   
   .newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }

   ```

    * Modify following in /apps/livecycle/core/components/login.jsp.

   ```
   <div class="loginContentArea">
   
   To
   
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>If the existing images in `/apps/livecycle/core/content/login` (copied from `/libs/livecycle/core/content/login`) are removed, then remove the corresponding references in CSS.

### Add new images {#add-new-images}

1. Follow the steps of Adding new style, or modifying existing style (documented above).
1. Add new images in `/apps/livecycle/core/content/login`. To add image:

    1. Install WebDAV client.
    1. Navigate to `/apps/livecycle/core/content/login` folder, using webDAV client. For more information, see: [http://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](http://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).
    
    1. Add new images.

1. Add new styles in `/apps/livecycle/core/content/login/login.css,` corresponding to new images added in `/apps/livecycle/core/content/login`.
1. Use the new styles in `login.jsp` at `/apps/livecycle/core/components`.
1. For Example:

    * Add the following to `/apps/livecycle/core/content/login/login.css`

   ```css
   .newLoginContainerBkg {
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```

    * Modify following in /apps/livecycle/core/components/login.jsp.

   ```
   <div class="loginContainerBkg">
   
   To
   
   <div class="newLginContainerBkg">
   ```

[**Contact Support**](https://www.adobe.com/account/sign-in.supportportal.html)

>[!MORE_LIKE_THIS]
>
>* [Introduction to Customizing AEM Forms workspace](../../forms/using/introduction-customizing-html-workspace.md)
>* [Generic steps for AEM Forms workspace customization](../../forms/using/generic-steps-html-workspace-customization.md)
>* [Managing tasks in an organizational hierarchy using Manager View](../../forms/using/tasks-organizational-hierarchy-using-manager.md)
>* [Integrating Correspondence Management in AEM Forms workspace](../../forms/using/integrating-correspondence-management-html-workspace.md)
>* [Single Sign On and timeout handlers](../../forms/using/single-sign-timeout-handlers.md)
>* [Displaying the user avatar](../../forms/using/displaying-user-avatar.md)
>* [Displaying information in the Task Summary pane](../../forms/using/displaying-information-task-summary-pane.md)
>* [Changing the organization logo](../../forms/using/changing-organization-logo-branding.md)
>* [Changing the color scheme of the interface](../../forms/using/changing-color-scheme-interface.md)
>* [Changing the font on the interface](../../forms/using/changing-font-interface.md)
>* [Changing the locale of the user interface](../../forms/using/changing-locale-user-interface.md)
>* [Customizing error dialogs](../../forms/using/customizing-error-dialogs.md)
>* [Customizing tabs for a task](../../forms/using/customizing-tabs-task.md)
>* [Customizing Task Actions](../../forms/using/customizing-task-actions.md)
>* [Customizing the listing of process instances](../../forms/using/customizing-listing-process-instances.md)
>* [Customizing the task Details page](../../forms/using/customizing-task-details-page.md)
>* [Displaying additional data in ToDo list](../../forms/using/display-additional-data-in-todo-list.md)
>* [Getting Task Variables in Summary URL](../../forms/using/getting-task-variables-summary-url.md)
>* [Images for Route Actions](../../forms/using/images-route-actions.md)
>* [Creating a new login screen](../../forms/using/creating-new-login-screen.md)
>* [Minification of the JavaScript files](../../forms/using/minification-javascript-files.md)
>* [Sorting of Tracking tables and adding more columns](../../forms/using/sorting-tracking-tables-add-columns.md)
>* [Updating the link to the documentation](../../forms/using/updating-link-help-documentation.md)
>* [Hosting two AEM Forms workspace instances on one server](../../forms/using/two-html-workspace-instances-one.md)