#Introduction
---

This document describes the NSKeyValueCoding informal protocol, which defines a mechanism allowing applications to access the properties of an object indirectly by name (or key), rather than directly through invocation of an accessor method or as instance variables.

這份文件描述了一個非正式的protocol(`NSKeyValueCoding`)，此份文件定義了一種機制，且這個機制允許應用程式透過name/key去間接地存取物件的屬性，而不是直接調用存取方法或實體變數

You should read this document to gain an understanding of how to use key-value coding in your applications and how to make your classes key-value coding compliant for interacting with other technologies. Key-value coding is a fundamental technology when working with key-value observing, Cocoa bindings, Core Data, and making your application AppleScript-able. You are expected to be familiar with the basics of Cocoa development and theObjective-C language.

你應該詳讀這份文件，來增進你對KVC的認識，如何使用KVC在你的應用程式，如何讓你的類別具有KVC兼容並與其他技術互動，KVC是一個基礎的技術working with KVO, Cocoa bindins, Core Data,且讓你的應用程式AppleScript-able(蘋果腳本化),You are expected to be familiar with the basics of Cocoa development and theObjective-C language.
