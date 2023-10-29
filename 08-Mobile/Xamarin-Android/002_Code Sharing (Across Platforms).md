Code Sharing (Across Platforms)

Sunday, February 12, 2017

9:40 PM

 

![Xamarin.Android app Code Sharing Xamarin.iOS app Windows Phone app UI App layer Service access layer Data layer UI App layer UI Shareable code Business layer Data access layer App layer Models ](002_Code_Sharing_(Across_Platforms)_000.png){width="5.0in" height="2.4583333333333335in"}

 

 

An average amount of code that can be shared across platform is around **60%.**

 

 

So what happens when we need to use various services, apis and class libraries across multiple platform? Well, it\'s simple we would use PCL\
\
**PCL (Portable Class Library)**

 

As the name implies, these are libraries that can be references from different various project types. It can be thought of the Lowest common denominator. Because of these, we do have the limitation that we can only use LOW LEVEL Apis in our progress.

 

![PCL (Portable Class Library) Library shared across platforms Lowest common denominator Extendable to other platforms ](002_Code_Sharing_(Across_Platforms)_001.png){width="5.0in" height="2.341666666666667in"}

 

 

**How do we create a PCL though?\
\
**In Visual Studio this is a simple option that appears under Visual C# \> Windows \> Class Library (Portable for iOS, Android and Windows)

 

PCLs can be configured to work with different project types:

 

![Change Targets largets: .NET Framework 4.5 Windows 8 Windows Phone Silverlight 8 ASP.NET core 5.0 Silverlight 5 Windows Phone 8.1 XamarinAndroid Xamarin.iOS Xamarin.iOS (Classic) Install additional targets\... OK ](002_Code_Sharing_(Across_Platforms)_002.png){width="5.0in" height="4.583333333333333in"}

Another way of sharing logic between platform is using a **Shared Project.**

 

A shared project is a different prototype we can select in VS.

 

![Summary Xamarin.Android allows us to build fully native Android applications Architecture often based on PCLs ](002_Code_Sharing_(Across_Platforms)_003.png){width="5.0in" height="2.158333333333333in"}

 
