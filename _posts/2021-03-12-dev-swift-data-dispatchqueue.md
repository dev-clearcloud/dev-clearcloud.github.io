---
title: "Studying Swift"
excerpt: "internet"

categories:
  - swift
tags:
  - dispatchqueue
  - async
---

### Swift main thread -> UI update
```
func UpdateProgress() {
    var i = 0
    var prog : Float = 0.10
    let step : Float = (Float(1.0) / Float(tempValuesArray.count)) * 0.90
    print(step)
    DispatchQueue.global().async {
        while i < self.tempValuesArray.count {
            print(prog)             
            DispatchQueue.main.async { () -> Void in
                self.progressView.setProgress(prog, animated: true)
                self.progressLabel.text = String(prog)
            } // end of async
            prog += step
            i = i + 1
        } // end of while
    }
}
```
