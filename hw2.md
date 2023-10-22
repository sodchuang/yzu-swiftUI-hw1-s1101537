<h1>HW1</h1>
    
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        ZStack {
            Image("Image Asset")
                .resizable()
                .aspectRatio(contentMode: .fill)
                .background(Color.mint) 
                .offset(y:40)
                .overlay(Text("自我介紹")
                    .fontWeight(.bold)
                    .font(.system(size:40))
                    .padding()
                    .offset(x: -90,y:-270))
                .overlay(
                    Text("姓名：莊博宇      \n學號：1101537")
                        .fontWeight(.heavy)
                        .lineSpacing(20)
                        .offset(x: -100, y:-200)
                )
                .overlay(
                    ZStack {
                        Text("沒人知道下一秒會發生什麼, \n每一刻只要活著盡興最重要")
                            .fontWeight(.heavy)
                            .lineSpacing(20)
                            .font(.system(size: 20))
                            .foregroundColor(.black)
                            .frame(width: 350, height: 150, alignment: .center)
                            .background(Color.white)
                            .cornerRadius(30.0)
                            .opacity(0.8)
                        
                        Image(systemName: "globe.europe.africa.fill")
                            .font(.largeTitle)
                            .foregroundColor(.blue)
                            .offset(y:55) 
                    },
                    alignment: .bottom
                )


        }
    }
}
      


    
```

<img width="40%" src="https://raw.githubusercontent.com/sodchuang/yzu-swiftUI-hw1-s1101537/main/1101537-hw1.jpg">
