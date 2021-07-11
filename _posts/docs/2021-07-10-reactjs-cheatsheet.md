---
layout: post
date: 2021-07-10 16:19
title: "ReactJS cheatsheet"
category: docs
tags:
- documentation 
comments: true

---

If you already know react, but wanted to brush up your knowledge on React or looking for quick reactjs references and best practices, 
this is the right place. This post can be used as a cheatsheet and is intended to keep up with latest and best practices.

<!--more-->

# Hooks

## useEffect

**1. Run an effect and clean it up only once**

```javascript
useEffect(
    () => {
        const hobbits = api.getHobbits('get me list of Hobbits');
        setHobbits(hobbits);
        const subscription = props.lordOfTheRings.subscribe();
        return () => {
            subscription.unsubscribe();
        };
    },
    []
)

```
**2. Run effect every time some property changes**

```javascript
useEffect(
    () => {
        const hobbit = api.getHobbitByName('props.hobbitName');
        setHobbit(hobbit);
    },
    [props.hobbitName]
)
```
**3. Run effect after every completed render**

```javascript
useEffect(
    () => {
        api.load('misty mountain song!!!')
    }
)
```

