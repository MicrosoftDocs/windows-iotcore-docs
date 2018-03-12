--- 
title: Accessibility for Windows 10 IoT 
author: saraclay 
ms.author: saclayt 
ms.date: 03/8/2018 
ms.topic: article 
description: Learn about accessibility and how to apply these learnings to your next application or device. 
keywords: Windows 10 IoT Core, Windows 10 IoT Enterprise, accessibility, color contrast 
--- 
 
# An Overview of Accessibility for Windows IoT 
 
## Introduction 
Accessibility enables people of all abilities to intuitively and efficiently leverage all the functionalities that your applications or devices offer, regardless of a person interacts with your application or device. 
 
It is essential that accessibility is considered during the design phase of the product as this will avoid many potential accessibility-related bugs. For example, during the design phase, consideration around the colors used and the size of text, (and how those might be customized by the user,) can help a great many customers. And for devices with a keyboard, during the design phase, consideration around how the keyboard can be used to leverage all the functionality in the product, and also how to access the most frequently-accessed functionality with the fewest number of keystrokes.  
 
For the developer, from an implementation perspective the good news is that Windows as a platform already does a lot of work to provide some level of accessibility by default. For example, standard controls are programmatically accessible by default through the UI Automation (UIA) API. If you choose not to use a standard control and instead build custom UI, the work required to make the UI accessibility can be much more time-consuming than simply building apps using standard controls provided by the platform. 

## Accessibility testing
Below are tools we recommend to use while building your application. While these tools will help when it comes to auditing your own designs, please note that you will still need to account for features such as high contrast and text requirements.

### AccScope
The [AccScope](https://msdn.microsoft.com/library/windows/desktop/Dn433239) tool enables developers and testers to evaluate the accessibility of their app during the app's development and design, potentially in earlier prototype phases, rather than in the late testing phases of an app's development cycle. It's particularly intended for testing Narrator accessibility scenarios with your app.

### Inspect
[Inspect](https://msdn.microsoft.com/library/windows/desktop/Dd318521) enables you to select any UI element and view its accessibility data. You can view Microsoft UI Automation properties and control patterns and test the navigational structure of the automation elements in the UI Automation tree. Use Inspect as you develop the UI to verify how accessibility attributes are exposed in UI Automation. In some cases the attributes come from the UI Automation support that is already implemented for default XAML controls. In other cases the attributes come from specific values that you have set in your XAML markup, as AutomationProperties attached properties.

Want to learn more about accessibility testing? Read the [Accessibility testing article](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-testing#inspect) for the full list.
 
 
## Accessibility in UWP apps 
The UWP team at Microsoft has put together a comprehensive guide on accessibility for UWP app design and development. For your convenience, we've included the list below, but you can also learn more by reading our [overview on accessibility](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-overview). 
 
In addition, an introduction to the UI Automation API and some tools available to help you learn about the programmatic representation of your UI, is available below. 
 
> [!VIDEO https://www.youtube.com/embed/6b0K2883rXA]

 
| Article | Description | 
|---------|-------------| 
| [Designing inclusive software](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/designing-inclusive-software) | Learn about evolving inclusive design with UWP apps for Windows 10.  Design and build inclusive software with accessibility in mind. | 
| [Developing inclusive Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/developing-inclusive-windows-apps) | This article is a roadmap for developing accessible UWP apps. | 
| [Accessibility checklist](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-checklist) | Provides a checklist to help you ensure that your UWP app is accessible. | 
| [Expose basic accessibility information](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/basic-accessibility-information) | Basic accessibility info is often categorized into name, role, and value. This topic describes code to help your app expose the basic information that assistive technologies need. | 
| [Keyboard accessibility](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/keyboard-accessibility) | If your app does not provide good keyboard access, users who are blind or have mobility issues can have difficulty using your app or may not be able to use it at all. | 
| [High-contrast themes](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/high-contrast-themes) | Describes the steps needed to ensure your UWP app is usable when a high-contrast theme is active. | 
| [Accessible text requirements](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessible-text-requirements) | This topic describes best practices for accessibility of text in an app, by assuring that colors and backgrounds satisfy the necessary contrast ratio. This topic also discusses the Microsoft UI Automation roles that text elements in a UWP app can have, and best practices for text in graphics. | 
| [Accessibility practices to avoid](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/practices-to-avoid) | Lists the practices to avoid if you want to create an accessible UWP app. | 
| [Custom automation peers](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/custom-automation-peers) | Describes the concept of automation peers for Microsoft UI Automation, and how you can provide automation support for your own custom UI class. | 
 
