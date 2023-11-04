
<h1>HW3</h1>
    
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack{
            Image("3th")
                .resizable()
                .frame(width: 700, height: 100)
            HStack {
                VStack {
                    HStack {
                        Image("new-1")
                            .resizable()
                            .frame(width: 100, height: 100)
                        Image("new-2")
                            .resizable()
                            .frame(width: 100, height: 100)
                    }
                    
                    HStack {
                        Image("1th-3")
                            .resizable()
                            .frame(width: 100, height: 100)
                        Image("1th-5")
                            .resizable()
                            .frame(width: 100, height: 100)
                    }
                }
                
                Image("1th-1")
                    .resizable()
                    .frame(width: 200, height: 200)
                VStack {
                    HStack {
                        Image("new-3")
                            .resizable()
                            .frame(width: 100, height: 100)
                        Image("new-4")
                            .resizable()
                            .frame(width: 100, height: 100)
                    }
                    
                    HStack {
                        Image("1th-2")
                            .resizable()
                            .frame(width: 100, height: 100)
                        Image("1th-4")
                            .resizable()
                            .frame(width: 100, height: 100)
                    }
                }
            }}
    }
}
      


    
```

<img width="40%" src="https://raw.githubusercontent.com/sodchuang/yzu-swiftUI-hw1-s1101537/main/1101537-hw3.jpg">
