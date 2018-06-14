---
title: "4 Weeks Developing for iOS"
date: 2018-06-13T09:53:31+08:00
author: "Julius Putra Tanu Setiaji"
tags:
  - iOS
  - UIKit
  - Swift
  - MapKit
---

A brief introduction: it is currently my summer break after I finished my freshman year in NUS -- and I was able to secure an internship at SEA Group (Garena Online) in the iOS team.

I had no experience in owning an Apple device, let alone developing for iOS, so I had to learn a lot of things.

For the first 2-3 weeks I was doing my entry tasks. First 2 days I learnt swift, and tried my best to pick up Objective-C (man, isn't objc syntax weird). Swift is really a pleasant language to work with, especially after having to deal with Java for one whole semester (NUS SoC being a Java school). I also used extensively this very useful website: https://objectivec2swift.com/ to learn the mapping between Swift and Objective-C. After a week+ I think I can say I can read Objective-C code quite well.

Using Apple documentations was a little bit frustrating at first -- it is rather example-scarce and the caveats are usually not stated explicitly -- this is in comparison with Ruby on Rails/nodeJS documentations that I have been using when I was doing web development. I also can't look at the source code, so sometimes I just cross my fingers and use `lldb` extensively to test various possibilities that are not documented clearly.

As for bugs, I found some -- not sure if those were my mistakes or not. Firstly, MapKit annotation does not show up if the coordinate is (0.00, 0.00). I know, it's in the middle of the ocean, but it should still show up. Changing it to (0.00001, 0.00) makes the annotation shows up. Sigh, Apple, why? Another bug that I found is that when changing the annotation, it would work if I either change the `title` and `subtitle` directly, or through this kind of code:

```swift
class MyAnnotation: MKPointAnnotation {
  var locationName: String {
    didSet {
      subtitle = locationName
    }
  }
}
```

However, it wouldn't work if I used setter/getter instead:

```swift
class MyAnnotation: MKPointAnnotation {
  var locationName: String {
    set(newValue) {
      subtitle = newValue
    }
    get {
      return subtitle
    }
  }
}
```

I can't be bothered to look at how MKPointAnnotation works under the hood in Objective-C but that was an annoying bug.

And now I have encountered another pecularity. For my current project, I need to create a `UITableView` with around 400,000 rows. Yes, you read that right, 4 followed by five 0's afterwards. When run in the simulator, no matter where you are, scrolling is always buttery smooth, yet whenever I try it on the real device, scrolling would be smooth on top and lags starting at row 200,000 onwards. This was really weird and tracking down my code yields nothing. I tried to run Time Profiler on the real device, but apparently since XCode 9.3, you can't run time profiler on iPhones below iOS 11.3 (wow, thanks so much Apple!)

Eventually I borrowed my colleague's iPhone X, and voila! the scrolling is as smooth as in the simulator. It was running iOS 11.4, so I immediately went to time profile for later comparison. For testing, I downloaded both XCode 9.2 (which supports my iOS 10 device), and ran time profiler on it. I was suspecting that UITableView rendering is optimised in iOS 11. It's either that, or that iPhone X is so powerful that the scrolling lag simply does not exist. My former hypothesis was correct! There's one symbol that takes up more than 60% of the time when the `UITableView` starts to lag, which does not exist in the iPhone X. It seems that the rendering logic has been changed in iOS 11. To further confirm this, I used my iOS 9 simulator, and, wow, I could not believe my eyes, it lagged even on the simulator running on the computer. Since this is something internal, I can do nothing :( except asking my future users to upgrade to iOS 11 when they finally encounter this problem.

Here's to 8 more weeks developing for iOS.
