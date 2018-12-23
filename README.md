# RxSwift 4시간에 끝내기

![](docs/rxswift_in_4_hours_logo.png)

<br/>

## Contents

### 1. 기본
#### 공식 사이트 둘러보기
- [http://reactivex.io/](http://reactivex.io/)
- [RxSwift](https://github.com/ReactiveX/RxSwift)

#### 동기/비동기
- 동기
```swift
@IBAction func onLoadSync(_ sender: Any) {
    guard let url = URL(string: imageUrl1) else { return }
    guard let data = try? Data(contentsOf: url) else { return }
    
    let image = UIImage(data: data)
    imageView.image = image
}
```
- 비동기
```swift
@IBAction func onLoadAsync(_ sender: Any) {
    DispatchQueue.global().async {
        guard let url = URL(string: self.imageUrl1) else { return }
        guard let data = try? Data(contentsOf: url) else { return }
        
        let image = UIImage(data: data)
        
        DispatchQueue.main.async {
            self.imageView.image = image
        }
    }
}
```

#### 라이브러리 (PromiseKit)
```swift
promiseLoadImage(from: loadingImageUrl)
    .done { image in
        self.imageView.image = image
    }.catch { error in
        print(error.localizedDescription)
}
```

#### RxSwift
```swift
_ = rxswiftLoadImage(from: loadingImageUrl)
    .observeOn(MainScheduler.instance)
    .subscribe({ result in
        switch result {
        case let .next(image):
            self.imageView.image = image

        case let .error(err):
            print(err.localizedDescription)

        case .completed:
            break
        }
    })
```

#### Disposable/DisposeBag
```swift
var disposable: Disposable?
disposable?.dispose()
```
```swift
var disposeBag = DisposeBag()
```

<br/>

### 2. 사용법
- just, from
- map, flatMap
- filter
- operators
  - 생성
  - 변환
  - 필터링
  - 결합
  - 오류처리
  - 조건과 불린 연산자
  - 수학과 집계 연산자
  - 역압 연산자
  - 연결
  - Observable 변환
  - [A Decision Tree of Observable Operators](http://reactivex.io/documentation/ko/operators.html)
- scheduler
- next, error, completed
- marbles
  - [http://rxmarbles.com/](http://rxmarbles.com/)
  - [http://reactivex.io/documentation/operators.html](http://reactivex.io/documentation/operators.html)
- side-effect
- RxCocoa
  - Driver
  - binding

<br/>

### 3. 응용
- Subject, Relay
- Unfinished Observable
- Memory Leak

<br/>

### 4. 확장
- [RxViewController](https://github.com/devxoul/RxViewController)
- [RxOptional](https://github.com/RxSwiftCommunity/RxOptional)
- [RxExtension](https://github.com/tokijh/RxSwiftExtensions)
- [RxSwift Community Projects](https://community.rxswift.org/)

<br/>

## 세미나 영상보기
- [RxSwift 4시간에 끝내기](https://www.youtube.com/watch?v=2uumx7Vzidc&list=PL03rJBlpwTaAh5zfc8KWALc3ADgugJwjq)

<br/>

## License

![](docs/cc_license.png)
<br />이 저작물은 <a rel="license" href="http://creativecommons.org/licenses/by/2.0/kr/">크리에이티브 커먼즈 저작자표시 2.0 대한민국 라이선스</a>에 따라 이용할 수 있습니다.
