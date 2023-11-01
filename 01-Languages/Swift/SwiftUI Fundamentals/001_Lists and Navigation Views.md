Lists and Navigation Views

Sunday, May 15, 2022

10:37 PM

A List in View is a container that presents rows of data arranged in a single column, optionally providing the ability to select one or more members.

![10 12 13 struct ToDoList: View { var body: some View List { do I ) 2\") do do 3 ) ](001_Lists_and_Navigation_Views_000.png)

The real important thing to remember when dealing with SwiftUI and a List of items.. Is that we ALWAYS need to provide some sort of unique identifier. Which means the list that we are providing NEEDS to follow the **identifiable protocol.** In order to do this we can create a new Struct.... IF we follow the identifiable protocol it only says that we need a variable named id:

![10.15, ios 13.0, watchos 6.e, tvos 13.e public protocol Identifiable { / / Il A type representing the stable dentity of the entity associated with /// an instance. associatedtype ID : Hashable I\' / The stable identity of the entity associated with this instance. var id: Self. ID { get ](001_Lists_and_Navigation_Views_001.png)
