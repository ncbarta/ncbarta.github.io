---
title: "Maxing out MapKit: Optimizing map views for high performance"
description: "In this post you will learn how to save memory, CPU, and battery in iOS applications containing a map view."
slug: "maxing-out-mapkit"
date: 2022-09-20 00:00:00+0000
#image:
tags:
    - "Swift"
    - "MapKit"
    - "Performance"
    - "iOS"
keywords:
    - "MapKit"
weight: 1
---

All changes require minimal code changes and boost performance substantially. This is not a tutorial on how to use a map view.

## Dequeue

If you are looking at this blog, there is a high chance you already know the following optimization.

Map Views are set up very similarly to Table Views from an interface perspective. Developers should make sure they dequeue MKMapAnnotations.

```swift
func mapView(_ mapView: MKMapView, viewFor annotation: MKAnnotation) -> MKAnnotationView? {
    let annotationView = mapView.dequeueReusableAnnotationView(withIdentifier: nil, for: annotation) // <- important
    
    annotationView.canShowCallout = true
    annotationView.annotation = annotation
     
    return annotationView
}
```

This simple change lets the map view reuse annotation views when they move offscreen. The performance gained from this system is crucial for keeping the map scrolling smoothly when there are large quantities of annotations. As a tradeoff, this optimization will increase the memory used, but it is generally considered best practice.

## Annotation Callouts

Typically, developers choose to add callout accessory views inside mapView(viewFor:), however this is actually a critical memory mistake since accessory view creation is not `lazy`. Unless there is some special reason you need to create your accessory view inside mapView(viewFor:), you should instead create it in mapView(didSelect:).

```swift
// Performance testing results (Physical iPad pro 11inch iOS 14.6, restarted after each run):
// 10k trials: 29mb in savings
// 100k trials: 92.8mb in savings + considerably shorter launch time
func mapView(_ mapView: MKMapView, didSelect view: MKAnnotationView) {
    view.rightCalloutAccessoryView = UIButton()
}
```

## Clustering Annotation Views

Clustering annotation views is a great way of reducing the number of annotations being rendered on screen - it should be used in almost all scenarios. Benefits from this optimization greatly outweigh the previous two optimizations in most scenarios. There are many great tutorials on clustering, so I won’t dive into it in this post.

## Caching User Location

Unless you need real time updating information, you should not be using `mapView.showsUserLocation = true`, because it consumes a lot of energy (in my tests it was consuming ~10% of CPU.)

Instead, cache a pin and update it’s location manually.

```swift
private let locationManager = CLLocationManager()
private var userPin: MKPointAnnotation?

func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
	
	//...
    
   if userPin != nil {
       mapView.removeAnnotation(userPin!)
   }
   let newUserPin = MKPointAnnotation()
   newUserPin.coordinate = center
   userPin = newUserPin
   self.mapView.addAnnotation(self.userPin!)
}
```

Devices iOS 14+ are compatible with a manually placed “default” user location pin - devices bellow iOS 14 are stuck with whatever you come up with.

```swift
func mapView(_ mapView: MKMapView, viewFor annotation: MKAnnotation) -> MKAnnotationView? {
    if annotation === userPin { // note the operator here
        if #available(iOS 14.0, *) { // most devices get this nice pin
            let v = MKUserLocationView(annotation: annotation, reuseIdentifier: "upin")
            v.zPriority = .max
            v.isEnabled = false
            v.isOpaque = true
            return v
        } else {
            let v = MKMarkerAnnotationView(annotation: annotation, reuseIdentifier: "upin")
            v.glyphImage = UIImage(systemName: "person.circle.fill")
            v.isEnabled = false
            v.isOpaque = true
            return v
        }
    }
}
```

## Getting Memory to Release

The biggest problem with map views is that they never release their memory. Apps using map views will often balloon to hundreds of mb of memory within a few scrolls. This memory will then refuse to be released, damaging the performance of the rest of the app/device. Unfortunately there is no `mapView.clearCache()` function, so we will have to do it ourselves.

The solution is to create the map view programmatically, and delete/recreate when necessary. This optimization is highly application specific, so I leave it to the reader.