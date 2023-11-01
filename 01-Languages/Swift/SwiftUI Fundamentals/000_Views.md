Views

Sunday, May 15, 2022

7:34 PM

**[XCODE WALKTHROUGH]**

![\' TOD0 ---t ToDo AppDelegate,swift Scene Delegate. swift ContentView.swift Assets. xcassets LaunchScreen. storyboard Info.plist Preview Content Products 1 2 3 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 TODo ) TODo ) AppDelegate.swift ) No Selection AppDe1egate . swift ToDo Created by zappycode on 2/22/20. Copyright @ 2020 Nick Walter. All rights reserved. import UlKit 1 \@UIApp1icationMain class AppDeIegate: UIResponder, UIApp1icationDe1egate { func application(\_ application: UIApp1ication, didFinishLaunchingWithOptions launchOptions: \[UIApp1ication.LaunchOptionsKey: Any J?) Bool { // Override point for customization after application launch. return true ](000_Views_000.png)

So, during this course the trainer goes into the files that we have by default when we start a SwiftUI application. What\'s interesting here is that this does NOT match what got created by default on my local machine. Is it because I am dealing with a newer version of SwiftUI?

**AppDelegate.swift**

(Do not have this file)... but essentially it is the Starting Point of the app.... We got the **didFinishLaynchingWithOptions** which means the app has launched for the first time and we pass in whatever customization we want to include... Since we are doing a SwiftUI application you can see that we are passing a **UISceneConfiguration** which means we are setting up a SCENE... which takes out to our scene delegate...

**SceneDelegate.swift**

(I also do NOT have this file)\
This seems to have been started in 2020\
<https://medium.com/swlh/bye-bye-appdelegate-swiftui-app-life-cycle-58dde4a42d0f>

\^\^\^ This link is also outdated since we don\'t even have a **LifeCycle** option to work with in Xcode today.

Hah! One thing the instructor says in the course is that if doing a pure SwiftUI project I pretty much never have to touch this files... that explains things. I guess it was rare for people do combine SwiftUI to StoryBoard work to begin with.

... BUT THEN we get to the ContentView file

**ContentView.swift**

I DO have this file. The ContentView is just the name of the View... just as a ViewController with StoryBoard ... there is nothing special about this file. We can call it whatever we want. Apple just decided to call the FIRST view the ContentView.

VIEWs are the big thing with SwiftUI. They can be as Big as the old school ViewControllers OR as small a tiny peace of text.

**Assets**

This is the folder where I will store all media for the app...

With SwiftUI I get the Automatic preview of the app... this I guess is only available when working in SwiftUI.

**[TEXT VIEWS]**

SwiftUI at is core is just formed with STRUCTS called VIEW. These Struct has been created by Apple.... The REQUIREMENT for this struct is to have a property called body that ALSO inherits from VIEW.

![struct Conter1tView: View { var body: some View { Code\" ](000_Views_001.png)

One random swift thing I didn\'t know about is that when you have a single line inside of a closure like we have here, we don\'t need to type return... though we can.. The above would be the same if I did

*Return Text(\"Hello Code\")*

BTW the file that states which is your first VIEW rendering is the Swift file that has the \@main

![10 11 Swi ftlJI_Fundamenta1sApp. swi ft Swi ftUI Fundamentals Created by Jonathan Hernandez on 5/14/22. import SwiftUI grain struct SwiftUI_Fundamenta1sApp: App { var body: some Scene { WindowGroup { ContentView() ](000_Views_002.png)

In my case \^\^\^ \@main I think it means, MAIN thread

**[Hstacks and Vstacks]**

So if I wanted to get multiple views going in my page, I could attempt to just add them to the body like so:\
![struct MyFristView: View { var body: some View { O Functiondeclares an opaque re. \' ) of \'Text\' initializer is unu lext( \"Hello Code\' World\") 1 ](000_Views_003.png)

But I immediately see errors everywhere. How come? Well, here is where Vstacks and Hstacks come into place:

![struct MyFristView: View { var body: some View { HStack { Text( \"Hello Code\" Text( \"Hello World\" ](000_Views_004.png)

The Vstack just means we can stack our views vertically and the Hstack horizontally.

Stacks can also be place inside each other!

![var body: some View { Text ( \'hello Text ( \"Hello Text ( \"Hello VStack { HStack { Text( HStack { Text ( HStack { Text ( \"#110 \"Hello \"Hello Code ) World \" Code ) World\" Code \" ) World\" ](000_Views_005.png)

Seems like writing the code is not the only way... CMD+click will yield:\
![11 13 struct MyFristView: View { Q var body: ex Actions Jump to Definition Show Quick Help Callers Edit All in Scope some View { \"Hello Code u views: s: som Show SwiftUl Inspector\... Embed in Stack Embed in VStack Embed in List Group Make Conditional Repeat Extract to Variable Extract to Method Extract All Occurrences ](000_Views_006.png)

**[SPACERS]**

The thing with SwiftUI is also that it wants to center things as much as possible...What if we want to alter? That\'s where Spaces come in inside of an Hstack or Vstack... spacers will take up as much space as it possibly can.

![HStack { Text ( \"Hello Spacer ( ) Text( \"Hello Code \" World\" Heno Code ](000_Views_007.png)

I can use this spacers as fun ways to get all my views Left or Right / Top or Bottom at any time

![import SwiftU1 struct MyFristView: View { var body: some View { VStack { HStack { Text (\"Hello Code\" Text (\"Hello World\" Spacer() Spacer ( ) 1 \*euo Code Hello World ](000_Views_008.png)

**[BUTTONS]**

Another simple VIEW provided by SwiftUI... As expected it gives me the chance to have some actions

The button consists of two simple things... the ACTION and the LABEL... pretty self explanatory. The action will require the code we want to run... just a simple function passed in... and then the label will want another VIEW... not just text... LITERALLY ANY VIEW can be the \"label\".... It says \"what do you want me to look like\"

![struct ContentView: View { var body: some View { return Button(action: label: { Circle() ](000_Views_009.png)

**[MODIFIERS]**

This are the tools we have to modify any views we have in a page... A great way to access them is by going to the + at the top right of Xcode and:\
![\'ort swiftU1 :uct ContentVie • t var body: sor @ Vociifiers return Bu print label: Circl :uct ContentVie static var pr Group { Conte te_l func content: (T) ---Y ActionSheet) Vie. \"here T Identifiable this -f\" \' with fm i uTTyp. title: ](000_Views_010.png)

Plenty of them to choose from. In order to use them we can just call them after the definition of a view.. With a DOT...

An even easier way to pull our modifiers is by pressing CMD and clicking on the View we wish to modify... show the SwiftUI Inspector... and then:\
![Rectangle() Suøer Cool Button\" . red) A-vs : PreviewProvider { some View { nterfaceorientation( Status ](000_Views_011.png)

Modifiers are all at the bottom
