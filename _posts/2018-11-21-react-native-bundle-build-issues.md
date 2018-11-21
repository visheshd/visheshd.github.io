---
layout: post
title: ReactNative bundling and build issues on a new machine
type: post
published: true
excerpt: "I started to setup a ReactNative project that we have been working on for a while now on my machine. The generated iOS native code was version controlled but the build was still not functioning on my machine."
comments: true
tags: [reactnative, cocoapods, ios]
---

I started to setup a ReactNative project that we have been working on for a while now on my machine. The generated iOS native code was version controlled but the build was still not functioning on my machine.

Followed the setup instructions and I got the following 

> Can't build on iOS - "Podfile.lock: No such file or directory"

Turned out I didn’t have cocoapods installed which were needed!

## Installing CocoaPods 
`sudo gem install cocoapods`

Once I fixed that, started seeing 
> ”:CFBundleIdentifier", Does Not Exist

1. Close Xcode
2. Delete node_modules and reinstall fresh
3. Open the project in Xcode

On step three I opened .xcodeproj  which gave me something to the effect of

> directory not found DerivedData

I had to instead open .xcworkspace. Did a product clean and build and it worked!

When you use CocoaPods, it creates a workspace file that needs to be opened in order for the builds to compile properly.

https://github.com/auth0/react-native-lock/issues/151#issuecomment-295566616

Have you come across other quirky react-native issues? :) ... Would love to hear about them.

Original blog post at https://causecode.com/reactnative-bundling-and-build-issues-on-a-new-machine/