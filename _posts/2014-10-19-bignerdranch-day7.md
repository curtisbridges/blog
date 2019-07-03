---
title: "Big Nerd Ranch, Beginning iOS - Day 7"
date: 2014-10-19
canonical: ""
description: ""
tags: [iOS, swift]
draft: false
---
Day 7 was very different from the previous days at the Ranch. It is mostly a catch-all day for miscellaneous topics that came up throughout the week as well as a discussion on tools.

<!--more-->

I was impressed by some of the built in features of both Xcode, the debugger, and instrumentation. In particular, I was shocked by all the options available for debugging with breakpoints; conditional breakpoints, computer speach of pre-defined text triggered from breakpoints, and many other options.

Next we reviewed memory leak analysis using Instrument templates. We worked through a fairly contrived (but relevant) example where the tools correctly found an ARC leak.

The rest of the day was picking up random topics of interest. Christian demonstrated some of his techniques of debugging Auto Layout constraints with Size Classes by setting the canvas in free form mode and resizing it to see how the layout behaves. I’ve used this technique for years for correctly developing desktop applications with resizable windows so I’m very glad to see it replicated in the iOS tools. While he was at it, we saw a demonstration for constraint inequalities and how they affect animation, which led perfectly into the next topic…

Animations.

I was impressed with how easy iOS makes animating interface elements. In a lot of cases, it can simply be achieved via a call to:

```swift
UIView.animateWithDuration(\_: animations: () -> ())
// with a start state before the call and the desired end state within the closure.
// There we variations on this as well such as Spring animations:

UIView.animateWithDuration(0.6, delay: 0.0, usingSpringWithDampening: 0.2, initialSpringVelocity: 0.0,
    options: UIViewAnimationOptions.something, animations: { () -> Void in
        // .. finishing code
        }, completion: nil)

// And keyframe animations:
override func touchesEnded(touches: NSSet, withEvent event: UIEVent) {
    let touch = touches.anyObject() as UITouch
    let loc = touch.locationInView(view)

    // Update constraints outside of animation closure
    topConstraint.constant = loc.y

    UIView.animateWithDuration(0.5, animations: { () -> Void in
        // Re-layout views inside animation closure
        self.view.layoutIfNeeded()

        // Update view properties inside animation closure
        self.view.backgroundColor = UIColor.redColor()
    })
}
```

Finally, we picked up a topic covered in older editions of the book, location. I’m pleased we covered this topic, as it is something almost completely unique to the platform and something I hope to become familiar with soon (I like to jog).

Our simple example in Swift:
```swift
import CoreLocation
import MapKit
import UIKit

class ViewController: UIViewController, CLLocationManagerDelegate {
    @IBOutlet weak var mapView: MKMapView!
    let locationManager = CLLocationManager()

    override func viewDidLoad() {
        super.viewDidLoad()

        locationmanager.requestWhenInUseAuthorization()

        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.distanceFilter = 10.0 // how far the user needs to move before you get updates
        locationManager.delegate = self
        locationManager.startUpdateingLocation()
    }

    func locationManager(manager: CLLOcationManager!, didUpdateLocations locations: [AnyObject]!) {
        println("\(locations)")

        // CLLocation: coordinate, altitude, horizontal and vertical accuracy
        if let currentLocation = locations.last as? CLLocation {
            // We found a location
            mapView.setCenterCoordinate(currentLocation.coordinate, animated: true)

            let span = MKCoordinateRegionMake(0.01, 0.01)
            let region = MKCoordinateRegionMake(currentLocation.coordinate, span)
            mapView.setRegion(region, animated: true)

            if currentLocation.horizontalAccuracy < 20.0 {
                manager.stopUpdatingLocation()
            }
        }
    }

    func locationManager(manager: CLLocationManager!, didFailWithError error: NSError!) {
        println("\(error)")
    }
}
```

And so ended my Big Nerd Ranch course. It was such an incredible experience and I highly recommend anyone interested in one of the course topics taught by Big Nerd Ranch to give them serious consideration; the environment is completely unique and they certainly aren’t lying when they say it is “monastic like”. The lack of external distractions of the real world certainly went a long way in helping become immersed in the material.

I hope to put it to good use soon.
