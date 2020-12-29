---
title: 'RxSwift Quick Guide'
date: 2020-07-19T17:18:05+01:00
draft: false
---

# 

# RxSwift Quick Guide

RxSwift :- is a library for making our code asynchronous + re-active in nature. Swift based varibales or model does not have these bahaviuor by default. We need to write extra code to get these bahaviour



# Main concept in RxSwift

`Observable<Element>` :- think it as a magic box. Any thing inside it becomes re-active. its emites 3 events alogn with some data (element or error or completed message)

`Operators` :- transform/ process data emitted by Observable

Observer/ subscriber :- received event/ data from Observable



# How to create Observables?

```swift
Observable.just(...)
.range()
.of()
.from()
.create{}
.never()  // does not emit enything and never terminated
.empty()  // it will only emit a completed event and terminated
.deferred() // brand new observable for each subscribers
```



# Traits

Traits are also Observable but with limited power

There are three kinds of traits in RxSwift: `Single`, `Maybe` and `Completable`

```swift
Single :- Observable that emits either success with value or an error event eg . Use its to get notified about an operation (file reading)
Completable :- emits either completed or error event
Maybe :- either sucess with value or completed or error event
```



# Subject

Observable with ability to add new elements any time. Observable are read only like `let`. Subjects are read and write like `varibale`

```swift
PublishSubject :- starts empty..add new value using .send('newValue').. subscriber will get 
only newly added value after subscription. 

BehaviorSubject :- starts with an initial value.. subscriber will get most recent element

ReplaySubject :- subscribe will get last specied elements and all newly added elements
```



# Relay - Subject

`PublishRelay and BehaviourRelay`

Subjects with limited power. unlike Subject relay only accepts new value using `.accept()` method

PublishRelay and BehaviourRelay does not emit error or completed event



