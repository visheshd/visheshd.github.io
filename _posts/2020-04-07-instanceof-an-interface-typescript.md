---
layout: post
title: Check if an object is an instanceof an interface
type: post
published: true
excerpt: "Checking interface type at runtime"
comments: true
tags: ["typescript", "interface", "instanceof"]
---

## How do you check in typescript if variable is an instance of interface?

Since types are not available at runtime typescript allows you to define type checks that you could use at runtime like:

```javascript

interface Keyboard {
    keys: number;
}

function instanceOfKeyboard(object: any): object is Keyboard {
    return 'keys' in object;
}

const kb = { keys: 5 }
if (instanceOfKeyboard(kb)) {
    alert(kb.member);
}

```

