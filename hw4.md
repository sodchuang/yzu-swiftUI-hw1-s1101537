<h1>HW4</h1>
    
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Text("YZU 樂器行")
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
            TabView{
                Group{
                    WelcomeView()
                        .tabItem { Image(systemName: "rosette")
                            Text("Welcome")
                        }
                    
                    IntroduceView()
                        .tabItem { 
                            Image(systemName: "list.dash")
                            Text("Courses")
                        }
                    courseView()
                        .tabItem { 
                            Image(systemName: "book")
                            Text("Learn")
                        }
                }
                .toolbarBackground(Color.black, for: .tabBar)
                .toolbarBackground(.visible, for:.tabBar)
            }
            .tint(.yellow)
        }
    }
}

import SwiftUI
struct Course: Identifiable{
    var id = UUID()
    var image:String
    var courseNameUS:String
    var courseNameTW:String
    var courseHours:String
}
var courses = [
    Course(image: "Musicdisplays", courseNameUS: "Instrument teaching", courseNameTW: "初級樂器教學", courseHours: "total 64hr"),
    Course(image: "Violinview", courseNameUS: "Instrument sales", courseNameTW: "樂器販售", courseHours: "8 hr/day"),
    Course(image: "Perform", courseNameUS: "Concert", courseNameTW: "音樂會", courseHours: "不定期"),
    Course(image: "Sheet", courseNameUS: "sheet sales", courseNameTW: "樂譜販售", courseHours: "8 hr/day"),
    Course(image: "Together", courseNameUS: "tool sales", courseNameTW: "零件販售", courseHours: "8 hr/day")
]

struct courseView: View {
    var body: some View{
        ScrollView{
            ForEach(courses){
                thisCourse in 
                CardView(course: thisCourse)
            }
        }      
    }
    
}


struct CardView: View {
    var course: Course
    var body: some View {
        VStack {
            Image(course.image)
                .resizable()
                .aspectRatio(contentMode: .fit)
            
            VStack(alignment: .leading) {
                Text(course.courseNameUS)
                    .font(.headline)
                    .foregroundStyle(.secondary)
                
                Text(course.courseNameTW)
                    .font(.title)
                    .foregroundStyle(.primary)
                    .lineLimit(3)
                
                Text(course.courseHours)
                    .font(.caption)
                    .foregroundStyle(.purple)
            }
            .frame(minWidth: 0, idealWidth: 100, maxWidth: .infinity, alignment: .leading)
            .padding(.leading, 15)
            .padding(.bottom, 10)
        }
        .background(Color(red: 255/255, green: 204/255, blue: 153/255))
        .cornerRadius(20)
        .clipShape(Rectangle())
        .overlay(RoundedRectangle(cornerRadius: 20).stroke(Color.gray, lineWidth: 2))
        .padding(.all, 10)
    }
}

import SwiftUI

struct WelcomeView: View {
    var body: some View {
        VStack{
            Image("music")
                .resizable()
                .aspectRatio(contentMode: .fit)
            Text("樂器培訓\n樂譜/樂器/零件等販售")
                .fontWeight(.heavy)
                .lineSpacing(20)
                .font(.system(size: 32.0))
                .foregroundColor(.white)
                .frame(width: 350, height: 150, alignment: .center)
                .background(Color.blue)
                .cornerRadius(20.0)
                .multilineTextAlignment(.center)
            
        }
    }
}


import SwiftUI
struct Restaurant: Identifiable {
    var id = UUID()
    var name:String
    var image:String
}

var restaurants = [
    Restaurant(name: "Violin", image: "Violin"),
    Restaurant(name: "Viola", image: "Viola"),
    Restaurant(name: "Bass", image: "Bass"),
    Restaurant(name: "Trumpet", image: "Trumpet"),
    Restaurant(name: "Guitar", image: "Gita"),
    Restaurant(name: "Oboe", image: "Double"),
    Restaurant(name: "Er-hu", image: "Ergo"),
    Restaurant(name: "Tronbone", image: "Long"),
    Restaurant(name: "Piano", image: "Piano"),
    Restaurant(name: "Basson", image: "Ba"),
]
struct IntroduceView: View {
    @State var showDetailView = false
    @State var selectedRestaurant:Restaurant?
    var body: some View {
        NavigationView{
            List(restaurants){
                restaurantItem in 
                BasicImageRow(thisRestaurant: restaurantItem)
                    .onTapGesture {
                        self.showDetailView = true
                        self.selectedRestaurant = restaurantItem
                    }
            }
            .sheet(item: self.$selectedRestaurant, content: {restaurantItem in RestaurantDetailView(thisRestaurant: restaurantItem)})
            .navigationBarTitle("餐廳列表")
        }
    }
}
struct BasicImageRow: View {
    var thisRestaurant:Restaurant
    var body: some View {
        HStack{
            Image(thisRestaurant.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thisRestaurant.name)
        }
    }
}
struct RestaurantDetailView:View {
    @Environment(\.presentationMode) var presentationMode
    var thisRestaurant: Restaurant
    var body: some View {
        ScrollView{
            VStack{
                Image(thisRestaurant.image)
                    .resizable()
                    .aspectRatio(contentMode: /*@START_MENU_TOKEN@*/.fill/*@END_MENU_TOKEN@*/)
                    .clipped()
                Text(thisRestaurant.name)
                    .font(.system(.title, design: .rounded))
                    .fontWeight(.black)
                Spacer()
                
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName:"chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20)
                    .padding(.top, 40)
                    Spacer()
                }
            }
        )
    }
}
```

![](amo8w-mfwgy.gif)

