# swiftui_custom_tabview


### Core

```swift
        TabView(selection: self.$tabSelection) {
            Text("Tab Content 1")
                .tag(1)
            
            Text("Tab Content 2")
                .tag(2)
            
            Text("Tab Content 3")
                .tag(3)
            
            Text("Tab Content 4")
                .tag(4)
            
            Text("Tab Content 5")
                .tag(5)
        } //: TABVIEW
        .overlay(
            CustomTabView(tabSelection: self.$tabSelection)
            ,alignment: .bottom
        )
```

### Entire Code 

```swift

//
//  ContentView.swift
//  CustomTabViewWithButton
//
//  Created by paige shin on 2023/04/15.
//

import SwiftUI

struct ContentView: View {
    
    @State private var tabSelection = 1
    
    var body: some View {
        TabView(selection: self.$tabSelection) {
            Text("Tab Content 1")
                .tag(1)
            
            Text("Tab Content 2")
                .tag(2)
            
            Text("Tab Content 3")
                .tag(3)
            
            Text("Tab Content 4")
                .tag(4)
            
            Text("Tab Content 5")
                .tag(5)
        } //: TABVIEW
        .overlay(
            CustomTabView(tabSelection: self.$tabSelection)
            ,alignment: .bottom
        )
    }
}

struct CustomTabView: View {
    
    @Binding var tabSelection: Int
    @Namespace private var animationNamespace
    
    let tabBarItems: [(image: String, title: String)] = [
        ("house", "Home"),
        ("magnifyingglass", "Search"),
        ("heart", "Favorites"),
        ("person", "Profile"),
        ("gear", "Settings"),
    ]
    
    var body: some View {
        ZStack {
            Capsule()
                .foregroundColor(Color(.secondarySystemBackground))
                .shadow(radius: 2)
            
            HStack {
                ForEach(0..<5, id: \.self) { index in
                    Button {
                        self.tabSelection = index + 1
                    } label: {
                        VStack(spacing: 8) {
                            Spacer()
                            Image(systemName: self.tabBarItems[index].image)
                            
                            Text(self.tabBarItems[index].title)
                                .font(.caption)
                            
                            if index + 1 == self.tabSelection {
                                Capsule()
                                    .frame(height: 8)
                                    .foregroundColor(.blue)
                                    .matchedGeometryEffect(id: "SelectedTabId", in: self.animationNamespace)
                                    .offset(y: -2)
                            } else {
                                Capsule()
                                    .frame(height: 8)
                                    .foregroundColor(.clear)
                                    .offset(y: -2)
                            }
                        } //: VSTACK
                        .foregroundColor(index + 1 == self.tabSelection ? .blue : .gray)
                        .clipShape(Capsule())
                    }

                } //: FOREACH
                
            } //: HSTACK
     
            
        } //: ZSTACK
        .animation(.default, value: self.tabSelection)
        .frame(height: 80)
        .padding(.horizontal)
    }
    
}


struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}


```
