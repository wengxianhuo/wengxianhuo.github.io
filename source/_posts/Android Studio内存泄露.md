---
title: Android Studio内存泄露
date: 2016-08-19 16:52:50
tags: 记录
---
　　内存泄露指的是在gc进行回收时，无法回收本应该回收的对象，造成该对象重复出现，占用内存，严重影响app性能。


　　最常见的内存泄露情况是handler作为匿名内部类直接使用，而不是使用静态内部类。这种情况，匿名内部类Handler会保持对外部类的一个引用（假设是Activity），那么Activity在本应该被回收的时候会因为保留有Handler引用，且Handler中的msg或者runnable还没运行完，那就造成Activity无法被回收了，产生泄露问题。解决的办法就是使用静态内部类，并且该静态内部类的引用在可能的情况下使用弱引用。如果非的使用Context参数，那尽量多用ApplicationContext吧。

　　