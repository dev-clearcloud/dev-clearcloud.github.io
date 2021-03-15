---
title: "Studying Swift"
excerpt: "internet"

categories:
  - swift
tags:
  - dispatchqueue
  - async
  - animate
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

### Swift animate
```
UIView.animate(withDuration: 0.25, animations: {
    myButton.transform = CGAffineTransform(rotationAngle: CGFloat.pi)
})

// myView : 2초 동안 회색으로 배경색 변경, 2배 커짐, 180도 회전 하면서 200, 200 좌표로 이동
UIView.animate(withDuration: 2.0, animations: {
    myView.backgroundColor = .gray

    let scale = CGAffineTransform(scaleX: 2.0, y: 2.0)
    let rotate = CGAffineTransform(rotationAngle: .pi)
    let move = CGAffineTransform(translationX: 200, y: 200)

    let combine = scale.concatenating(rotate).concatenating(move)
    
    myView.transform = combine
}) { (_) in
        UIView.animate(withDuration: 2.0) {
            // 적용된 모든 변환을 제거 함.
            myView.transform = CGAffineTransform.identity
        }
}
```
