---
layout:     post
title:      "How to keep track of current page of an UIPageViewController"
subtitle:   "Keep track of your current page"
date:       2016-03-06 13:30:00
author:     "Cedulio Cezar"
header-img: "img/posts/swift-current-page/head.jpg"
social-img: "img/posts/swift-current-page/head-social.jpg"
favicon: "img/posts/swift-current-page/favicon.png"
tags: [swift2,ios9,swift,UIPageViewController,paging]
summary: "Keep track of your current page"
comments: True
---
In order to keep track of the current page your Keep track of your UIPageViewController your controller should conform to the UIPageViewControllerDelegate protocol and implement the following methods and of course have a member var Int to store the index.

```
func pageViewController(pageViewController: UIPageViewController, willTransitionToViewControllers pendingViewControllers: [UIViewController])

func pageViewController(pageViewController: UIPageViewController, didFinishAnimating finished: Bool, previousViewControllers: [UIViewController], transitionCompleted completed: Bool) {
```

This post assume that you already have implemented UIPageViewControllerDataSource correctly.

First let's implement the the willTransitionToViewControllers that is called every time a scroll happens, even if the transition didn't complete.

```
func pageViewController(pageViewController: UIPageViewController, willTransitionToViewControllers pendingViewControllers: [UIViewController]){
    // 1
    if let viewController = pendingViewControllers[0] as? MyPageViewController {
        // 2
        self.lastPendingViewControllerIndex = viewController.index
    }
}
```

1 - We have to wrap the lastPendingViewController in case there are no pendingViewControllers.

2 - Save the last pending viewController to use after when the transition completes.

Ok, now that we have the index of the next possible current page we should implement the second method.

```
func pageViewController(pageViewController: UIPageViewController, didFinishAnimating finished: Bool, previousViewControllers: [UIViewController], transitionCompleted completed: Bool) {
    // 1
    if completed{
      // 2
        self.currentPageIndex = self.lastPendingViewControllerIndex
    }
}
```

1 - This if statement validate if the page change transition ended. Otherwise we don't have to update the currentPageIndex, because the scroll was interrupted.

2 - We attribute the index of the last pending view controller to the current.

### Credits
Header image by [Hoach Le Dinh](https://unsplash.com/photos/c8TWWQ5ZnUw)
