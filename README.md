# RealityKit-tap-import-models
RealityKit SwiftUI tap and Import models 
# The first part
![IMG_0142](https://github.com/S-way520/RealityKit-import-multiple-models/assets/95877651/b79359c7-15e2-4aea-aecb-d176e30455dc)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ZStack{
            ARViewContainer()
                .edgesIgnoringSafeArea(.all)
            Image(systemName: "moonphase.full.moon.inverse")
        }
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: UIViewRepresentableContext<ARViewContainer>) -> ARView {
        let arView = ARView(frame: .zero)
        arView.tapGesture()//放置物体 1/2
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {}
}
extension ARView{//放置物体 2/2
    func tapGesture() {
        let tapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(handleTap(recognizer:)))
        self.addGestureRecognizer(tapGestureRecognizer)//点击行为1/2
    }//手势
    @objc func handleTap(recognizer: UITapGestureRecognizer) {//手势内容
        let anchorEntity = AnchorEntity(plane: .horizontal)//水平类锚点
        guard let ARentity = try? ModelEntity.load(named: "tutorial") else {
            fatalError("tutorial model is not!")
        }
        anchorEntity.addChild(ARentity)
        self.scene.addAnchor(anchorEntity)//点击行为2/2
    }
}
```
