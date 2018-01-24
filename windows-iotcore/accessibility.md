---
title: Accessibility for Windows IoT
author: saraclay
ms.author: saclayt
ms.date: 01/23/2017
ms.topic: article
description: Learn about accessibility and how to apply these learnings to your next application or device.
keywords: Windows 10 IoT Core, Windows 10 IoT Enterprise, accessibility, color contrast
---

# An Overview of Accessibility for Windows IoT

## Introduction
In addition to development, design, and testing, accessibility is another concept to take into account when publishing
applications or manufacturing devices. Accessibility enables all people to leverage all of the functionalities your applications or devices offer, regardless of a user's abilities.

To ensure that applications and devices leveraging Windows IoT products offer accessibility-ready features and experiences,
we've put together an overview on best practices and important considerations.

## Common Accessibility Bugs
When it comes to designing and developing with accessibility in mind, successful execution requires awareness and preparation.
Accessibility should be considered initially when technical specifications are decided on. It's also helpful to keep in mind common accessibility bugs that often make a big difference when implemented.

* Colors and contrast: Don't convey important information through the use of color alone.

![Image of color contrast do's and dont's](media/Accessibility/accessibility1.png)

* Colors and contrast: Provide a minimum default contrast of 4.5:1. You can find this ratio using a color contrast analyzer ([download here](https://developer.paciellogroup.com/resources/contrastanalyser/))
or any other color contrast tool available online.

![Image of color contrast example](media/Accessibility/accessibility2.gif)

* Keyboard accessibility: Keyboard focus needs to be clearly visible, with required contrast and colors. The tab/arrow path through the UI must be intuitive.

![Image of keyboard focus example](media/Accessibility/accessibility3.gif)

* Programmatic accessibility: Use Windows desktop tools to learn about programmatic representation. 

![Image of programmatic accessibility example](media/Accessibility/accessibility4.png)

## Accessibility in UWP apps
The UWP team at Microsoft has put together a comprehensive guide on accessiblity for UWP app design and development. For your convenience, we've included the list below, but you can also learn more by reading their [Usability in UWP apps documentation](https://docs.microsoft.com/en-us/windows/uwp/design/usability/).

| Article | Description |
|---------|-------------|
| [Accessibility overview](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-overview) | This article is an overview of the concepts and technologies related to accessibility scenarios for UWP apps. |
| [Designing inclusive software](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/designing-inclusive-software) | Learn about evolving inclusive design with UWP apps for Windows 10.  Design and build inclusive software with accessibility in mind. |
| [Developing inclusive Windows apps](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/developing-inclusive-windows-apps) | This article is a roadmap for developing accessible UWP apps. |
| [Accessibility testing](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-testing) | Testing procedures to follow to ensure that your UWP app is accessible. |
| [Accessibility in the Store](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-in-the-store) | Describes the requirements for declaring your UWP app as accessible in the Microsoft Store. |
| [Accessibility checklist](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessibility-checklist) | Provides a checklist to help you ensure that your UWP app is accessible. |
| [Expose basic accessibility information](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/basic-accessibility-information) | Basic accessibility info is often categorized into name, role, and value. This topic describes code to help your app expose the basic information that assistive technologies need. |
| [Keyboard accessibility](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/keyboard-accessibility) | If your app does not provide good keyboard access, users who are blind or have mobility issues can have difficulty using your app or may not be able to use it at all. |
| [High-contrast themes](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/high-contrast-themes) | Describes the steps needed to ensure your UWP app is usable when a high-contrast theme is active. |
| [Accessible text requirements](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/accessible-text-requirements) | This topic describes best practices for accessibility of text in an app, by assuring that colors and backgrounds satisfy the necessary contrast ratio. This topic also discusses the Microsoft UI Automation roles that text elements in a UWP app can have, and best practices for text in graphics. |
| [Accessibility practices to avoid](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/practices-to-avoid) | Lists the practices to avoid if you want to create an accessible UWP app. |
| [Custom automation peers](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/custom-automation-peers) | Describes the concept of automation peers for UI Automation, and how you can provide automation support for your own custom UI class. |
| [Control patterns and interfaces](https://docs.microsoft.com/en-us/windows/uwp/design/accessibility/control-patterns-and-interfaces) | Lists the Microsoft UI Automation control patterns, the classes that clients use to access them, and the interfaces providers use to implement them. |
