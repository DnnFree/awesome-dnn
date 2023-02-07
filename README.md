## Awesome DNN (DotNetNuke) [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated list of awesome things related to DNN

### v9.11.0 Notes
Telerik removal automatically happen in 9.11, it's not require to run all process below.
But due some Resources issue, it's better wait until v9.11.1 is out.

### Noteworthy Changes in v9.8.0 - Optional Telerik Removal
The major highlight for this release is that we removed all our dependencies on the Telerik library. In oder to not make this a breaking change, we do leave Telerik removal as a manual option until v10. The main component that still relied on Telerik where Site Assets and Global assets which used Digital Assets Manager. We ship with v9.8.0 a new file manager that has no dependencies on Telerik but it is not installed by default to not break existing sites upon upgrades. Please note that it will be automatically replaced in v10, so please test and plan accordingly.

To help you try to identify if you have any other 3rd party extension that depends on Telerik, our very own @mitchelsellers has published the [Dnn Telerik Identitier](https://github.com/IowaComputerGurus/DnnTelerikIdentifier) module which you can download and install to to find assemblies that reference Telerik. Carefully review the results from this module to determine if your website is ready for full removal of Telerik. For any third-party modules that depend on Telerik, you should contact the module vendor/developer before following the steps below.

If you would like to remove Telerik in DNN 9.8.0 following are the steps to do so. Again, proceed with caution based on your findings using the ```DNN Telerik Identifier module``` above, as performing these steps may also break third-party extensions that depend on Telerik. We recommend you contact the developer/vendor in these cases for further guidance.

1. Create a full backup of the site and database.
2. Install the new ```Resource Manager``` module via ```Extensions > Available Extensions (Modules)```.
3. Navigate to ```Manage > Site Assets``` via the ```Persona Bar``` and remove the ```Digital Assets Management``` module from the page.
4. Add an instance of the ```Resource Manager``` module to the ```Site Assets``` page
5. Navigate to ```Manage > Global Assets``` via the ```Persona Bar``` and repeat ```Steps 3 & 4``` for that page.
6. Navigate to ```Manage > SQL Console``` via the ```Persona Bar``` and run the following script:
	
```
UPDATE {databaseOwner}{objectQualifier}Packages
SET IsSystemPackage = 0
WHERE Name IN ('DigitalAssetsManagement', 'DotNetNuke.Telerik.Web', 'DotNetNuke.Web.Deprecated', 'DotNetNuke.Website.Deprecated')
GO

DELETE FROM {databaseOwner}{objectQualifier}PackageDependencies
WHERE (PackageName = 'DotNetNuke.Web.Deprecated')
GO

UPDATE {databaseOwner}[{objectQualifier}Lists] SET Text = 'DotNetNuke.Web.UI.WebControls.Internal.PropertyEditorControls.DateEditControl, DotNetNuke.Web'
WHERE ListName = 'DataType' AND Value = 'Date'
GO

UPDATE {databaseOwner}[{objectQualifier}Lists] SET Text = 'DotNetNuke.Web.UI.WebControls.Internal.PropertyEditorControls.DateTimeEditControl, DotNetNuke.Web'
WHERE ListName = 'DataType' AND Value = 'DateTime'
GO
```

7. Navigate to ```Settings > Servers``` in the ```Persona Bar``` and click the ```Clear Cache``` button in the top-right corner.
8. Navigate to ```Settings > Extensions (Modules)``` in the ```Persona Bar``` and uninstall the ```Digital Assets Management``` extension. Be sure to check the ```Delete Files``` checkbox.
9. Navigate to ```Settings > Extensions (Libraries)``` in the ```Persona Bar``` and uninstall the ```DotNetNuke Telerik Web Components``` extension. Be sure to check the ```Delete Files``` checkbox.
10. Navigate to ```Settings > Extensions (Libraries)``` in the ```Persona Bar``` and uninstall the ```DNN Deprecated Web Controls Library``` extension. Be sure to check the ```Delete Files``` checkbox.
11. Navigate to ```Settings > Extensions (Libraries)``` in the ```Persona Bar``` and uninstall the ```DotNetNuke Deprecated Website Codebehind files``` extension. Be sure to check the ```Delete Files``` checkbox.
12. Open the ```web.config``` file within the site root and search for "Telerik". Delete any lines that reference it.
13. Test all third-party modules to make sure they still work without Telerik. If any do not work properly, please contact the developer/vendor for further guidance.

### [Upgrade Path](https://github.com/DnnFree/awesome-dnn/blob/master/UPGRADE-PATH.md)
[05.06.08](https://github.com/dnnsoftware/Dnn.Releases.Archive.5x) - [06.02.08](https://github.com/dnnsoftware/Dnn.Releases.Archive.6x) - [07.04.02](https://github.com/dnnsoftware/Dnn.Releases.Archive.7x) - [08.00.04](https://github.com/dnnsoftware/Dnn.Releases.Archive.8x) - 09.01.01 - 09.03.02 - 09.08.00 - 09.10.02 (Recommended due some minor issue on 9.11)

notes:
- make sure all module run smooth on 09.03.02 before upgrade to 9.8.0

### Official Resources
- [DNN Platform](https://github.com/dnnsoftware/Dnn.Platform) - [Latest release](https://github.com/dnnsoftware/Dnn.Platform/releases)
	- [v9.11.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.11.0)
	- [v9.10.2](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.10.2)
	- [v9.9.1](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.9.1)
	- [v9.9.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.9.0)
	- [v9.8.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.8.0)
	- [v9.7.2](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.7.2)
	- [v9.6.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.6.0)
	- [v9.5.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.5.0)
	- [v9.4.0](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.4.0)
	- [v9.3.2](https://github.com/dnnsoftware/Dnn.Platform/releases/tag/v9.3.2)
- [DNN wiki](http://www.dnnsoftware.com/wiki)
- [DNN Docs](http://www.dnnsoftware.com/docs/index.html)
- [DNN Videos](http://www.dnnsoftware.com/videos)
- [DNN Core Modules](https://github.com/dnnsoftware/Dnn.Platform/tree/master/DNN%20Platform/Modules)
	- CoreMessaging
	- DDRMenu
	- DigitalAssets
	- DnnExportImport
	- DnnExportImportLibrary
	- Groups
	- Html
	- HtmlEditorManager
	- Journal
	- MemberDirectory
	- RazorHost

### Community Site
- [dnncommunity.org](https://dnncommunity.org/) Official community site
- [DnnDocs.com](https://www.dnndocs.com/) Documentation created for the community, by the community

### Tutorial
- [DNN Token](https://github.com/DnnFree/awesome-dnn/blob/master/DNN-TOKEN.md)
- [DNN Suggested Upgrade Path](https://github.com/DnnFree/awesome-dnn/blob/master/UPGRADE-PATH.md)
- [DNNTemplates - Using the new Module Development Templates for DotNetNuke](http://www.chrishammond.com/Blog/itemid/2616/using-the-new-module-development-templates-for-dot)
- [DnnPackager - Getting Started](http://darrelltunnell.net/blog/2015/12/01/dnnpackager-getting-started/)
- DNN 9 Persona Bar
	1. [Persona Bar Architecture](https://www.dnnsoftware.com/community-blog/cid/155381/dnn-9-persona-bar-architecture)
	2. [Extending the Persona Bar](https://www.dnnsoftware.com/community-blog/cid/155384/dnn-9-extending-the-persona-bar)
	3. [Adding a ReactJS App to Persona Bar](https://www.dnnsoftware.com/community-blog/cid/155391/dnn9-adding-a-reactjs-app-to-persona-bar)
	4. [Diving in a ReactJS Persona Bar Extension](https://www.dnnsoftware.com/community-blog/cid/155393/dnn9-diving-in-a-reactjs-persona-bar-extension)
	5. [Calling an existing Web API from the Persona Bar](https://www.dnnsoftware.com/community-blog/cid/155404/dnn9-calling-an-existing-web-api-from-the-persona-bar)
	6. [Working with Common Components in the Persona Bar](https://www.dnnsoftware.com/community-blog/cid/155405/dnn9-working-with-common-components-in-the-personabar)
	7. [Using Common Components outside of the Persona Bar](https://www.dnnsoftware.com/community-blog/cid/155407/dnn9-using-common-components-outside-of-the-persona-bar)
- [DNN 9.4.0: DNN Dependency Injection: .NET Core](https://www.andrewhoefling.com/Blog/Post/dnn-dependency-injection)
	- [sample](https://github.com/DnnFree/DNN.DependencyInjection.Samples)

### Development Tools
- [Generator-Upendodnn](https://github.com/UpendoVentures/generator-upendodnn) A yeoman generator that scaffolds DNN extensions, including Modules (Webforms, SPA, and MVC), Persona Bar, Skin Object, Library, Scheduler, and Hotcakes Commerce projects
- [DnnFree React](https://github.com/DnnFree/DnnFree.Modules.SPA.React) a starter DNN SPA Module with API, create using latest React & Webpack
- [DnnFree Angular](https://github.com/DnnFree/DnnFree.Modules.SPA.Angular) a starter DNN SPA Module create using Angular 5 (with Angular-CLI)
- [DNNTemplates](https://github.com/ChrisHammond/DNNTemplates) DNN Module and Theme Development Template for DNN 7/8/9
- [TopMenu](https://github.com/jbrinkman/TopMenu) Sample Razor Templates for DDRMenu
- [DNN8Templates](https://github.com/dnnsoftware/DNN.Templates) Module and Theme Development templates for DNN 8
- [DnnPackager](https://github.com/dazinator/DnnPackager) Module Development
- [nvQuickSite](https://github.com/nvisionative/nvQuickSite) is a desktop installation app for DNN
- [nvQuickTheme](https://github.com/nvisionative/nvQuickTheme) is a DNN theme framework / development workflow
- [nvQuickComponents](https://github.com/nvisionative/nvQuickComponents) is a collection of Web Components for DNN extension development (and beyond)
- [DnnC.DBAnalyzer](https://github.com/dnnconsulting/DnnC.DBAnalyzer) a tool that will give you a visualization of your Dnn database
- [DnnUserAccess-Mobile](https://github.com/DNN-Connect/DnnUserAccess-Mobile) Mobile app that pairs with the DNN User Access personabar extension. This app is made in React Native.
- [R7.Dnn.Extensions](https://github.com/roman-yagodin/R7.Dnn.Extensions) A library to simplify extensions development for DNN Platform
- [R7.Dnn.Extensions.React](https://github.com/roman-yagodin/R7.Dnn.Extensions.React) Library for DNN Platform web CMS extensions development with ReactJS.NET
- [R7.Dnn.Extensions.EFCore](https://github.com/roman-yagodin/R7.Dnn.Extensions.EFCore) A library for DNN Platform web CMS extensions development with Entity Framework Core
- [R7.Dnn.Templates](https://github.com/roman-yagodin/R7.Dnn.Templates) DNN Platform project templates and helper addin for MonoDevelop / Xamarin Studio
- [R7.Webmaster](https://github.com/roman-yagodin/R7.Webmaster) Webmaster's desktop productivity tools

### Open Source Modules
- [DnnFree Module SPA React](https://github.com/DnnFree/DnnFree.Modules.SPA.React) a starter DNN SPA Module with API, create using latest React & Webpack
- [DnnFree Module SPA Angular](https://github.com/DnnFree/DnnFree.Modules.SPA.Angular) a starter DNN SPA Module create using Angular 5
- DNNCommunity module collection to extend DNN features
  - [Dnn.SiteLog](https://github.com/DNNCommunity/Dnn.SiteLog) which replaces the feature from DNN Platform which was removed as part of DNN 8
  - [DNN.Feedback](https://github.com/DNNCommunity/DNN.Feedback) a basic module used for accepting user inquiries
  - [DNN.Vendors](https://github.com/DNNCommunity/DNN.Vendors) allows admins to manage Vendor relationships and add Advertising banners
  - [DNN.ActiveDirectory](https://github.com/DNNCommunity/DNN.ActiveDirectory) Active Directory authentication for DNN
  - [DNN.FormAndList](https://github.com/DNNCommunity/DNN.FormAndList) Design your own table complete with field types, validation and custom user permissions.
  - [DNN.Faq](https://github.com/DNNCommunity/DNN.Faq) a basic module used for displaying frequently asked questions
  - [Dnn.Newsletter](https://github.com/DNNCommunity/Dnn.Newsletter)
  - [DNN.IFrame](https://github.com/DNNCommunity/DNN.IFrame) a module used for embedding an internal/external URL
  - [DNN.XML](https://github.com/DNNCommunity/DNN.XML) a module used for displaying XML transformations
  - [DNN.Links](https://github.com/DNNCommunity/DNN.Links) a basic module used for displaying navigational links
  - [DNN.Wiki](https://github.com/DNNCommunity/DNN.Wiki) a module that combines a wiki engine with your favourite html editor
  - [DNN.NewsFeeds](https://github.com/DNNCommunity/DNN.NewsFeeds) a module used for displaying aggregated news feeds
  - [DNN.Forum](https://github.com/DNNCommunity/DNN.Forum) used for managing forums and email notification of posts
  - [DNNUserGroups](https://github.com/DNNCommunity/DNNUserGroups)
  - [DNN.Announcements](https://github.com/DNNCommunity/DNN.Announcements) a basic module used for displaying news items
  - [SecurityAnalyzer](https://github.com/DNNCommunity/SecurityAnalyzer) is a module aimed at helping you to improve the security on your DNN website
  - [DNN.Events](https://github.com/DNNCommunity/DNN.Events) manages display of upcoming events as a list in chronological order or in calendar format
  - [DNN.Reports](https://github.com/DNNCommunity/DNN.Reports) provides a simple, flexible, view on your database
  - [CaptainHook](https://github.com/DNNCommunity/CaptainHook) a simple GitHub Bot for processing Pull Requests
  - [DNN.Gallery](https://github.com/DNNCommunity/DNN.Gallery)
  - [DNN.Help](https://github.com/DNNCommunity/DNN.Help)
  - [DNN.Map](https://github.com/DNNCommunity/DNN.Map)
  - [DNN.Repository](https://github.com/DNNCommunity/DNN.Repository) can be used to store a collection of files, images, links or text
  - [DNN.Survey](https://github.com/DNNCommunity/DNN.Survey)
  - [NavigationProviders](https://github.com/DNNCommunity/NavigationProviders) This is a group of Navigation Providers which used to be part of the core DNN Platform
- [DnnBulkUserDelete](https://github.com/brucerchapman/DnnBulkUserDelete) - (by: @brucerchapman)
- [dnnGlimpse](https://github.com/jbrinkman/dnnGlimpse) module that aids in troubleshooting server-side - (by: @jbrinkman)
- [dnnCHAT](https://github.com/ChrisHammond/dnnCHAT) Chat module for DNN - (by: @ChrisHammond)
- [dnnsimplearticle](https://github.com/ChrisHammond/dnnsimplearticle) A simple DNN articles module - (by: @ChrisHammond)
- [Message of the Day](https://github.com/ChrisHammond/MessageOfTheDay) A simple MVC module - (by: @ChrisHammond)
- @sachatrauwaen Module collection
  - [Open Url Rewriter](https://github.com/sachatrauwaen/OpenUrlRewriter) improve SEO and overall Site quality
    - [PropertyAgent_OpenUrlRewriter](https://github.com/sachatrauwaen/PropertyAgent_OpenUrlRewriter) Open Url Rewriter provider for Ventrian Property Agent
	- [SQL_OpenUrlRewriter](https://github.com/sachatrauwaen/SQL_OpenUrlRewriter) Generic SQL provider for Open Url Rewriter for DNN
  - [NBStore_OpenUrlRewriter](https://github.com/sachatrauwaen/NBStore_OpenUrlRewriter) NBStore Provider for OpenUrlRewriter
  - [Open Content](https://github.com/sachatrauwaen/OpenContent) Structured Content editing
    - [Open Content Template](https://github.com/sachatrauwaen/OpenContent-Templates) Template for Open Content
    - [OpenContent_OpenUrlRewriter](https://github.com/sachatrauwaen/OpenContent_OpenUrlRewriter) DNN OpenUrlRewriter for OpenContent module
  - [Open Form](https://github.com/sachatrauwaen/openform) Create end users forms like contact, register, etc
  - [OpenImageProcessor](https://github.com/sachatrauwaen/OpenImageProcessor) DNN wrapper library around ImageProcessor Library For On-The-Fly Processing Of Images
  - [OpenOutputCache](https://github.com/sachatrauwaen/OpenOutputCache) 
  - [Content Localization Tools](https://github.com/sachatrauwaen/CLTools)
- @IowaComputerGurus Module Collection
  - [**DNN Telerik Identifier**](https://github.com/IowaComputerGurus/DnnTelerikIdentifier)
  - [Database Exporter](https://github.com/IowaComputerGurus/dnn.dbexporter)
  - [Secure Password Recovery](https://github.com/IowaComputerGurus/dnn.SecurePasswordRecovery)
  - [DNN Log Cleaner](https://github.com/IowaComputerGurus/DnnLogCleaner)
  - [DNN Secure My Install](https://github.com/IowaComputerGurus/dnn.secureMyInstall)
  - [DNN Simple Bootstrap Accordion](https://github.com/IowaComputerGurus/dnn.simpleBootstrapAccordion)
  - [DNN Simple Bootstrap Tabs](https://github.com/IowaComputerGurus/dnn.simpleBootstrapTabs)
  - [DNN News Articles URL Provider](https://github.com/IowaComputerGurus/dnn.newsArticlesUrlProvider)
  - [Quiz Module](https://github.com/IowaComputerGurus/icg.dnn.quiz)
  - [Scheduled SQL Jobs](https://github.com/IowaComputerGurus/dnn.scheduledjobs)
  - [Simple File List](https://github.com/IowaComputerGurus/dnn.SimpleFileList) Showing files in a particular folder
  - [Expandable Text HTML](https://github.com/IowaComputerGurus/DNN-ExpandableText) Quickly display multiple pieces of content in a compressed area
- [dnnWeather](http://dnnweather.codeplex.com/releases) Weather module for DNN. - (by: @davidCarpinteiro)
- [Handy Tips - Tooltips](https://github.com/bogdan-litescu/DnNSharp-HandyTips) - Skin Object replaces Dnn Labels with nice tooltips. (by: @dnnsharp)
- [DNN Redirects](https://github.com/bogdan-litescu/DnnRedirect) - set up redirects by user roles. (by: @dnnsharp)
- [Fast Shot - Slideshows and Galleries](https://github.com/bogdan-litescu/DnnSharp-FastShot) - Display images as galleries/slideshows (by: @dnnsharp)
- @fordnn Collection
  - [Universal Autosave](https://github.com/fordnn/universal-autosave/) - Configure autosave for any form/control.
  - [Data Exporter](https://github.com/fordnn/dataexport) - Export Data from database.
  - [User Import & Export](https://github.com/fordnn/usersexportimport) - Export/import users.
  - [User Friendly Registration ](https://github.com/fordnn/ufregistrationplugin)
  - [Reverse SiteUrls](https://github.com/fordnn/reversesiteurls)
- [Active Forum](https://github.com/activeforums/ActiveForums) - (by: @activeforums)
- DNN-Connect Modules collection (by: @DNN-Connect)
  - [DNN-Blog](https://github.com/DNN-Connect/DNN-Blog)
  - [DNN Connect Conference module](https://github.com/DNN-Connect/Conference) is used to create and manage our yearly conferences
	- [Conference.Mobile](https://github.com/DNN-Connect/Conference.Mobile) Xamarin mobile app for conference module
  - [Connect.Map](https://github.com/DNN-Connect/Map) Google maps module for DNN 8+
  - [DNN.Events](https://github.com/DNN-Connect/DNN.Events)
  - [DNN QA](https://github.com/DNN-Connect/DNNQA)
  - [DNN-Translator](https://github.com/DNN-Connect/DNN-Translator) helps you translate resource files in DNN
  - [RoleManager](https://github.com/DNN-Connect/RoleManager) Module to manage user role memberships
  - [CKEditorProvider](https://github.com/DNN-Connect/CKEditorProvider)
  - [Connect-Projects](https://github.com/DNN-Connect/Connect-Projects) Project gallery module
  - [Connect.UserAccess](https://github.com/DNN-Connect/Connect.UserAccess) Personabar extension to manage users' access to a site
  - [DNNConnect-2016-Demo-ReactJs](https://github.com/DNN-Connect/DNNConnect-2016-Demo-ReactJs) React JS 101 session demo
  - [Dnn-Powershell](https://github.com/DNN-Connect/Dnn-Powershell) module which allows you to run commands remotely for DNN Platform
  - [FlickrGallery](https://github.com/DNN-Connect/FlickrGallery) module to show group photos sorted by date taken
  - [IdentitySwitcher](https://github.com/DNN-Connect/IdentitySwitcher) Allows you to switch between users, without knowing their passwords
  - [LPManager](https://github.com/DNN-Connect/LPManager) Language Pack Manager, formerly known as DNN Europe LocalizationEditor
  - [SiteNews](https://github.com/DNN-Connect/SiteNews) Display new or modified contents from a web site.
  - [SkinControls](https://github.com/DNN-Connect/SkinControls) DNN Connect skin controls suite
- [dnnDocuments](https://github.com/mitchelsellers/dnnDocuments) - (by: @mitchelsellers)
- [AppInsights module](https://github.com/davidjrh/dnn.appinsights) - A module to use Visual Studio Application Insights with the DNN (by: @davidjrh)
- [Redis Caching Provider for DNN](https://github.com/davidjrh/dnn.rediscachingprovider) - (by: @davidjrh)
- [DNN Azure Active Directory Provider](https://github.com/davidjrh/dnn.azureadprovider) is an Authentication provider for DNN - (by: @davidjrh)
- [surveybox](https://github.com/surveyproject/surveybox) - (by: @surveyproject)
- [HotCakes Commerce Core](https://github.com/HotcakesCommerce/core) - (by: @HotcakesCommerce)
  - [HotCakes Commerce CMS](https://github.com/HotcakesCommerce/cms)
  - [HotcakesCartItemCount](https://github.com/nvisionative/HotcakesCartItemCount) - (by: @nvisionative)
- [All in one DNN Extensions](https://github.com/hismightiness/dnnextensions) - (by: @hismightiness - Will Strohl)
  - [Disqus Module](https://github.com/hismightiness/dnnextensions/releases/tag/Disqus-02.01.01)
  - [Code Camp Module](https://github.com/hismightiness/dnnextensions/releases/tag/CodeCamp-01.00.03)
  - [Content Injection](https://github.com/hismightiness/dnnextensions/releases/tag/ContentInjection-02.00.02)
  - [Lightbox Gallery Module](https://github.com/hismightiness/dnnextensions/releases/tag/Lightbox-01.12.00)
  - [Content Slider](https://github.com/hismightiness/dnnextensions/releases/tag/ContentSlider-01.03.01)
  - oEmbed Wrapper for .Net
  - DNN Google Hangout Module
  - DNN Media Module
  - User Group Labs: Meta Data Module
  - User Group Labs: My Groups Module
  - User Group Labs: Group Data Module
  - Contact Collector Module
  - Content Slider Module
  - Content Injection Module
  - Lightbox Gallery Module
  - Open Graph Protocol Module
  - DNN Demo Skin Objects
  - PrismJS Skin Object
  - DNN Parallax Skin
  - Future Gravity Skin
  - DNN Widget Suite
- [YAF.NET - Yet Another Forum.Net](https://github.com/YAFNET/YAFNET-DNN) - (by: @YAFNET)
  - [Active Forums to YAF.Net Migration](https://github.com/sleupold/AF_YAF.Net_Migration) - (by: @sleupold)
- [DNNVideoCourseModule](https://github.com/ralphwilliams/DNNVideoCourseModule) - (by: @ralphwilliams)
- [DNNQuickSurvey](https://github.com/ralphwilliams/DNNQuickSurvey) - (by: @ralphwilliams)
- [dnnTurbo Scripts](https://github.com/dnnwerk/dnnScript/) improving your DNN Database - (by: @dnnwerk)
- [Ventrian Modules](https://github.com/ventrian) great modules to extend DNN features - (by: @ventrian)
  - [News Articles](https://github.com/ventrian/News-Articles) News Articles for DotNetNuke has been helping DotNetNuke administrators to publish articles and blogs to their DotNetNuke portals since 2004
  - [Property Agent](https://github.com/ventrian/Property-Agent) Property Agent for DotNetNuke is a templated property module that allows you to manage and display all kinds of properties from cars to boats to real estate
  - [Simple Gallery](https://github.com/ventrian/Simple-Gallery) Simple Gallery for DotNetNuke has been helping DotNetNuke administrators to publish photos and albums to their DotNetNuke portals since 2005
  - [Child-Links](https://github.com/ventrian/Child-Links) is a navigation utility for helping administrators build their DNN sites.
  - [Feedback-Center](https://github.com/ventrian/Feedback-Center) is a module for collecting and organising feedback on any particular suite of products.
  - [File-Links](https://github.com/ventrian/File-Links) is a navigation utility for helping administrators displays lists of files.
  - [Subscriptions](https://github.com/ventrian/Subscriptions) Subscription management
  - [Subscription-Tools](https://github.com/ventrian/Subscription-Tools) is a module for managing subscription payments within DotNetNuke.
- [NB-Store](https://github.com/nbrightproject/NBrightBuy) E-Commerce for DNN - (by: @nbrightproject)
  - [MolliePaymentProvider](https://github.com/dnnconsulting/MolliePaymentProvider) Mollie Payment Provider for NBrightBuy (by: @dnnconsulting)
- [Aricie.PortalKeeper](https://github.com/Aricie/Aricie.PortalKeeper) is a DNN module to build agents - (by: @aricie)
- [BBImageStory](https://github.com/weggetor/BBImageStory) is DNN Module for creating image stories - (by: @weggetor)
- [DnnJobBoard](https://github.com/INNO-Software/DnnJobBoard) a job listing and application module - (by: @INNO-Software)
- [MyDnn.LiveChat](https://github.com/mydnn/LiveChat) is a powerfull module for Chat with visitors in real-time - (by: @mydnn)
- [UManage](https://github.com/OPSI-srl/UManage) is Simple and Fast User Management for DNN 8.0 - (by: @OPSI-srl)
- [CallTrackerLite](https://github.com/dmcdonald11/CallTrackerLite) is to replace an Access Database application utilizing DNN 8 - (by: @dmcdonald11)
- [DNN-GitHub-Authentication](https://github.com/cathalconnolly/DNN-GitHub-Authentication) - (by: @cathalconnolly)
- [X3.DnnUrlManagement](https://github.com/mathisjay/X3.DnnUrlManagement) UX for manage settings of DNN's Adv.Url Management - (by: @mathisjay)
- [DNN Dev Tools](https://github.com/weweave/DnnDevTools) The Swiss army knife for DNN developers and host admins - (by: @weweave)
- [DNN 8 Shoutbox SPA Module](https://github.com/markmcavoy/ShoutboxSPA) - (by: @markmcavoy)
- [DnnLogAnalyzer](https://github.com/DotNetNuclear/DnnLogAnalyzer) - (by: @DotNetNuclear)
- DNNSpot Modules (@DNNSpot)
  - [DNNSpot - Store](https://github.com/DNNspot/DNNspot.Store) an eCommerce Module for DNN
  - [DNNSpot - Quiz](https://github.com/DNNspot/DNNspot-Quiz)
  - [DNNSpot - Maps](https://github.com/DNNspot/DNNspot-Maps)
  - [DNNSpot - Tags](https://github.com/DNNspot/DNNspot.Tags)
- DNNStuff modules
  - [Aggregator](https://github.com/redtempo/dnnstuff.aggregator) - tabbed modules or content module.
  - [Inject Anything](https://github.com/redtempo/dnnstuff.injectanything) - html or script injection module.
  - [SQLViewPro](https://github.com/redtempo/dnnstuff.sqlviewpro) - present your data in grid, template or chart.
  - [Favorites](https://github.com/redtempo/dnnstuff.favorites) - allows a user to manage a list of favorite pages.
  - [Module Rotator](https://github.com/redtempo/dnnstuff.modulerotator) - rotate modules on page change or timer.
  - [Welcome](https://github.com/redtempo/dnnstuff.welcome) - show a welcome where visibility can be controlled by the site visitor
- [Engage Modules](https://github.com/EngageSoftware) - great module to extend DNN - (by: @Engage)
  - [DNN-JavaScript-Libraries](https://github.com/EngageSoftware/DNN-JavaScript-Libraries) Common JavaScript libraries packaged as DNN JavaScript Library extensions
  - [safe-dnn-minification](https://github.com/EngageSoftware/safe-dnn-minification) A replacement for the JS and CSS minification with the Client Dependency Framework that DNN uses
  - [Engage-Jackrabbit](https://github.com/EngageSoftware/Engage-Jackrabbit) is a utility module which allows an administrator to add scripts to a page
  - [Engage-Application-Insights](https://github.com/EngageSoftware/Engage-Application-Insights) is an extension for the DNN Platform to integrate Application Insights monitoring
  - [Engage-Booking](https://github.com/EngageSoftware/Engage-Booking) is an appointment management tool
  - [Engage-F3](https://github.com/EngageSoftware/Engage-F3) allows you to quickly and easily search for a string in the Text/HTML modules
  - [Engage-Employment](https://github.com/EngageSoftware/Engage-Employment) is a job listing and applicant management tool
  - [Engage-Survey](https://github.com/EngageSoftware/Engage-Survey) is a survey and form building tool
  - [Engage-Publish](https://github.com/EngageSoftware/Engage-Publish) is an article management system/workflow engine
  - [Engage-Take-Out](https://github.com/EngageSoftware/Engage-Take-Out) for importing and exporting site settings which aren't typically included in site templates
  - [Engage-Rotator](https://github.com/EngageSoftware/Engage-Rotator) is a slider/rotator tool
  - [Engage-Locator](https://github.com/EngageSoftware/Engage-Locator) is a location management tool
  - [Engage-Events](https://github.com/EngageSoftware/Engage-Events) is a calendar and event management system
  - [Engage-Dashboard](https://github.com/EngageSoftware/Engage-Dashboard) is an administrative tool for the DNN
  - [Engage-Tell-a-Friend](https://github.com/EngageSoftware/Engage-Tell-a-Friend) gives your website visitors the ability to share links to your site with friends
- [Dnn.IdentitySwitcher](https://github.com/erikvb/Dnn.IdentitySwitcher) switch between users without knowing their passwords. - (by: @erikvb)
- R7 Modules - (by: @roman-yagodin)
  - [R7.University](https://github.com/roman-yagodin/R7.University) designed to present and manage high school educational organization assets (divisions, employees, courses, etc.)
  - [R7.Documents](https://github.com/roman-yagodin/R7.Documents) Redesigned version of DNN Documents module
  - [R7.News](https://github.com/roman-yagodin/R7.News) Taxonomy-driven news subsystem
  - [R7.ImageHandler](https://github.com/roman-yagodin/R7.ImageHandler)
  - [R7.MiniGallery](https://github.com/roman-yagodin/R7.MiniGallery) Simple image gallery module
- BitBoxx modules - (by: @weggetor)
  - [BBImageHandler](https://github.com/weggetor/BBImageHandler) DNN 6/7 Image handler to display, resize, watermarks, thumbnails
  - [BBImageHandler-8](https://github.com/weggetor/BBImageHandler-8) DNN 8 Image handler to display, resize, watermarks, thumbnails
  - [BBImageStory](https://github.com/weggetor/BBImageStory) create image stories, step-by-step guides or image galleries with subtexts
  - [BBBooking](https://github.com/weggetor/BBBooking) Simple DNN module for renting an object on a daily basis
  - [BBContact](https://github.com/weggetor/BBContact) Simple configurable contact form, easy setup & email notification
  - [BBNews](https://github.com/weggetor/BBNews) collecting and providing news, able to collect from RSS/Atom feeds or twitter
- [**2sxc**](https://github.com/2sic/2sxc) helps web designers and developers prepare great looking, animated and sexy content templates in DNN (by: @2sic)
- [DNN-SEORedirect](https://github.com/40fingers/DNN-SEORedirect) allow monitor and manage 404's - (by: @40fingers)
- [DNN-Filecuumcleaner](https://github.com/40fingers/DNN-Filecuumcleaner) utility module, to create jobs to delete files from a specific folder on your website - (by: @40fingers)
- [dnnsearchandreplace](https://github.com/horacioj/dnnsearchandreplace) DNN Text Search and Replace
- [PolyDeploy](https://github.com/cantarus/PolyDeploy) A Bulk Deployment tool for the DNN CMS. PolyDeploy is focussed on security, reliability and auditability. (by: @cantarus)
- [Ventrian Property Agent](https://scippy.github.io/Property-Agent/) - Updated module of originale Ventrian Property Agent (by: @scippy)
- [40fingers DNN-SEORedirect](https://github.com/40fingers/DNN-SEORedirect) allow you to monitor and manage the 404's your DNN site is receiving and redirect (301) them

### Provider
- [CKEditor](https://github.com/w8tcha/dnnckeditor) An WYSIWYG HTML Editor Provider for DNN® 9.3.2 or above

### Skin Object
- [DnnC.CookieConsent](https://github.com/dnnconsulting/DnnC.CookieConsent) - (by: @dnnconsulting)
- [DnnThemeEditor](https://github.com/dnnconsulting/DnnC.DnnThemeEditor) Theme Editor SkinObject - (by: @dnnconsulting)
- [R7.FeedbackButton](https://github.com/roman-yagodin/R7.FeedbackButton) Feedback skinobject extension - (by: @roman-yagodin)
- [StyleHelper](https://github.com/40fingers/StyleHelper-Sko) The 40FINGERS Style Helper Skin object allows you to manipulate the CSS, Javascript links and meta tags DNN loads by default. You can remove them, change them and add your own.

### Free Skins/Theme
- [DNN Contra](https://github.com/dnnconsulting/DnnC.Contra) Dnn 8/9 responsive theme using Bootstrap 4 - (by: @dnnconsulting)
- [DNN Bootster](https://github.com/dnnconsulting/DnnC.BootsterV2) responsive skin\theme using Bootstrap 4.0.0.beta - (by: @dnnconsulting)
- [dnnmdesign](https://github.com/dnnconsulting/DnnC.MDesign) Bootstrap 3.3.6 Theme - (by: @dnnconsulting)
- [DnnC.Minimalist](https://github.com/dnnconsulting/DnnC.Minimalist) Bootstrap 3 Theme - (by: @dnnconsulting)
- [DnnC.Dnn-Connect-2017-Sass-Theme](https://github.com/dnnconsulting/DnnC.Dnn-Connect-2017-Sass-Theme) Demo of a Dnn Skeleton theme using Sass - (by: @dnnconsulting)
- [HammerFlex](https://github.com/ChrisHammond/HammerFlex) Bootstrap 3 Theme - (by: @ChrisHammond)
- [HammerHead](https://github.com/ChrisHammond/HammerHead) theme for DNN9 using BootStrap 4 - (by: @ChrisHammond)
- [R7.Epsilon](https://github.com/roman-yagodin/R7.Epsilon) Bootstrap 3 - (by: @roman-yagodin)
- [Bootstrap3 Instant](https://github.com/2sic/dnn-theme-bootstrap3-instant) - (by: @2sxc)
- [nvQuickTheme: DNN 9 + Bootstrap 4](https://github.com/nvisionative/nvQuickTheme) great minimalist DNN theme- (by: @nvisionative)
- [aarsysmetro7skin](https://github.com/aarsys/aarsysmetro7skin) Metro style 4 color skin package - (by: @aarsys)

### Sample Code/Project
- [DNN-SignalR](https://github.com/ChrisHammond/DNN-SignalR) Sample code for DNN modules using SignalR - (by: @ChrisHammond)
- [Dnn.Platform.Samples.Mvc](https://github.com/ChrisHammond/Dnn.Platform.Samples.Mvc) Sample projects to create MVC and SPA modules using DNN Platform 8.0 - (by: @ChrisHammond)
- [Module injection filters sample](https://github.com/jbrinkman/Dnn.InjectionFilter.Sample) - (by: @jbrinkman)
- [Sample Mobile Apps to access DNN Platform Web APIs](https://github.com/dnnsoftware/Dnn.Platform.Samples.Mobile) - (by: @dnnsoftware)
- [Sample projects to create MVC & SPA module using DNN 8.0](https://github.com/dnnsoftware/Dnn.Platform.Samples.Mvc) - (by: @dnnsoftware)
- [Liquid Content Code Samples](https://github.com/dnnsoftware/Dnn.Evoq.LiquidContent.Samples.Public) - (by: @dnnsoftware)
- [Restaurant Menu](https://github.com/DotNetNuclear/DnnRestaurantMenu) is written in 3 different installable types: an MVC module, a SPA module, and a Webforms module - (by: @DotNetNuclear)

### Showcase

...
