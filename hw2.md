<h1>HW2</h1>
    
```swift
import SwiftUI

struct StartView: View {
    var body: some View {
        NavigationView {
            VStack {
                Text("猜拳遊戲")
                    .font(.largeTitle)
                    .padding()
                
                NavigationLink(destination: InstructionsView()) {
                    Text("開始遊戲")
                        .font(.headline)
                        .padding()
                }
            }
            .navigationBarTitle("歡迎", displayMode: .inline)
        }
    }
}

struct InstructionsView: View {
    var body: some View {
        VStack {
            Text("玩法說明")
                .font(.largeTitle)
                .padding()
            
            Text("在遊戲中，您需要選擇剪刀、石頭或布。規則如下：")
                .font(.headline)
                .padding()
            
            Text("剪刀 > 布")
                .padding()
            Text("石頭 > 剪刀")
                .padding()
            Text("布 > 石頭")
                .padding()
            
            NavigationLink(destination: GameView()) {
                Text("開始遊戲")
                    .font(.headline)
                    .padding()
            }
        }
        .navigationBarTitle("玩法說明", displayMode: .inline)
    }
}

struct GameView: View {
    @State private var playerChoice = 0 // 玩家手势，0代表剪刀、1代表石头、2代表布
    @State private var computerChoice = Int.random(in: 0..<3) // 随机生成计算机手势
    @State private var isShowingResult = false // 用于控制是否显示游戏结果页面
    @State private var resultMessage = "" // 存储游戏结果的消息
    
    @EnvironmentObject var gameModel: GameModel // 通过环境对象访问胜利和失败计数
    
    var gestures = ["✂️", "🪨", "🧻"] // 手势符号数组
    
    let computerWinImageNames = ["1.png", "2.png", "3.png"] // 1到3为计算机赢的图像
    let playerWinImageNames = ["4.png", "5.png", "6.png"] // 4到6为玩家赢的图像
    
    var body: some View {
        VStack {
            Text("選擇你的手勢:")
                .font(.headline)
                .padding()
            
            HStack(spacing: 30) {
                ForEach(0..<gestures.count) { index in
                    Button(action: {
                        self.playerChoice = index
                        self.playGame()
                    }) {
                        Text(gestures[index])
                            .font(.largeTitle)
                    }
                }
            }
            
            if isShowingResult {
                VStack { // 使用 VStack 包装游戏结果的文本和图像
                    if resultMessage.contains("你赢了") {
                        Image(playerWinImageNames.randomElement() ?? "4.png")
                            .resizable()
                            .scaledToFit()
                            .frame(width: 200, height: 200)
                        Text(resultMessage)
                            .font(.title)
                            .padding()
                    } else if resultMessage.contains("計算機贏了") {
                        Image(computerWinImageNames.randomElement() ?? "1.png")
                            .resizable()
                            .scaledToFit()
                            .frame(width: 200, height: 200)
                        Text(resultMessage)
                            .font(.title)
                            .padding()
                    } else {
                        Text(resultMessage)
                            .font(.title)
                            .padding()
                    }
                }
                
                Button("再玩一次") {
                    self.isShowingResult = false
                    self.computerChoice = Int.random(in: 0..<3)
                }
                .font(.headline)
                .padding()
            }
            
            Spacer()
        }
    }
    
    func playGame() {
        let playerWins = (playerChoice == 0 && computerChoice == 2) ||
        (playerChoice == 1 && computerChoice == 0) ||
        (playerChoice == 2 && computerChoice == 1)
        
        let computerWins = (computerChoice == 0 && playerChoice == 2) ||
        (computerChoice == 1 && playerChoice == 0) ||
        (computerChoice == 2 && playerChoice == 1)
        
        if playerWins {
            resultMessage = "你赢了！"
            gameModel.recordWin() // 记录胜利
        } else if computerWins {
            resultMessage = "計算機贏了！"
            gameModel.recordLoss() // 记录失败
        } else {
            resultMessage = "平局！"
        }
        
        isShowingResult = true
    }
    
}

class GameModel: ObservableObject {
    @Published var wins = 0
    @Published var losses = 0
    
    func recordWin() {
        wins += 1
    }
    
    func recordLoss() {
        losses += 1
    }
}

@main
struct YourApp: App {
    var body: some Scene {
        WindowGroup {
            StartView().environmentObject(GameModel())
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        StartView()
    }
}

    
```

<img width="40%" src="">
