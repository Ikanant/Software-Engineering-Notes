Xamarin.Android Fundamentals

 

Creating a new Android App

![•du:•s•dÅ1 1 ](003_Xamarin.Android_Fundamentals_000.png){width="5.0in" height="3.5416666666666665in"}

 

 

 

![](003_Xamarin.Android_Fundamentals_001.png){width="5.0in" height="2.6166666666666667in"}

 

 

The two most important and fundamental elements of Android development are:

 

 

**Activities**

 

 

When thinking about regular C# or Java development, we deal with the common MAIN class which can be considered t he entry point of the application. This concept is quite simple and sadly does note relate entirely to Android development.

 

Android on the other hand can be thought as a collection of Activities. Some people can think of an Activity corresponding to ONE screen... but this is not entirely true. \--\> The truth is that an Activity contains the functionality of a SINGLE screen. In most cases it doesn\'t contain the actual code to handle the Visual Part of the screen. Although is possible to do that.

 

 

![Starting an App App ](003_Xamarin.Android_Fundamentals_002.png){width="5.0in" height="2.908333333333333in"}

 

 

When doing Android development what we can do is setup a single page (Activity). that will be the entry point of our application. We do this by setting up an Attribute in one of the activities. NOTICE that if we add this attribute to multiple Activities, Android will launch this simultaneously.

 

![Activities All activities inherit from base Activity Corresponds to one screen Functionality for a single task Specific lifecycle ](003_Xamarin.Android_Fundamentals_003.png){width="5.0in" height="2.575in"}

 

 

Activities are the HEART of Android development.

 

![\[Activity(Labe1 = \"Ray\'s Hot Dogs\" MainLauncher - true, - \"@drawable/icon\")l Icon public class MainActivity Activity A Sample Activity a 3:32 Rays Hot Dogs Hello World, Click Me! ](003_Xamarin.Android_Fundamentals_004.png){width="5.0in" height="2.6666666666666665in"}

 

 

In the image above, notice how our activities has a series of Attributes.

-   Label: Will be the name of the page / activity

-   MainLauncher: Will set a page to be the first Activity to be run when launching the app

-   Icon: Icon that will display next to the Label of the page\
     

 

![Activity States Activity launched Running Paused Backgrounded Stopped Other activity launched Home or App switcher Back button ](003_Xamarin.Android_Fundamentals_005.png){width="5.0in" height="2.05in"}

 

 

 

![USER NAVIGATES BACK TO YOUR ACTIVITY Process Killed OTHER APPLICATIONS NEED MEMORY Activity Starts onCreate() onStart() onResume() Activity Running NEW ACTIVITY STARTED onFreeze() onRestart() ACTIVITY COMES TO FOREGROUND ACTIVITY COMES TO FOREGROUND ](003_Xamarin.Android_Fundamentals_006.png){width="5.0in" height="2.875in"}

 

![onPause() ACTIVITY NO LONGER VISIBLE onStop() onDestroy() Activity Shut Down ](003_Xamarin.Android_Fundamentals_007.png){width="5.0in" height="1.9916666666666667in"}

 

 

 

**Important Lifecycle Method:**

 

-   OnCreate

    -   Called on the Construction of the Activity and it\'s only called ONCE

-   OnStart

    -   Ran after the OnCreate

-   OnResume

    -   Called right before User can interact with the activity

-   OnPause

    -   Opposite method of OnResume. Called when the user can no longer interact with the Activity

-   OnStop

    -   Called when the Activity is no longer Active

 

 

The MOST common method we will use is the OnCreate method. This method is called when the Activity is CREATED and it\'s created once PER activity. Only when the Activity gets destroyed by the OS (for example when there is no more memory left) OR when the User taps the BACK button, will this method will be called again.

 

**SetContentView** is a method to use to link a VIEW to our Activity

 

![OnCreate \[Activity(Labe1 = \"RaysHotDogs\" , MainLauncher public class MainActivity : Activity = true, - \"@drawable/icon \" ) \] Icon - (Bundle bundle) protected override void OnCreate base . OnCreate(bund1e) ; // Set our view from the \"main\" layout resource SetContentView( Resource . Layout . Main) ; ](003_Xamarin.Android_Fundamentals_008.png){width="5.0in" height="2.5166666666666666in"}

 

 

 

**Views**

 

 

-   Visual part of the screen

-   Views in Xamarin.Android are wqritten in .axml pages. This pages are pretty much the same as XAML.

-   Views in Android applications are Stored in the Resources\\Layout folder

 

![Sample View Code 6:00 RaysHotDogs How many hot dogs do you want to r der? ORDER NOW! \< ?xml encoding=\"utf-8\"?\> \<LinearLayout xmlns: android=\" android : orientation= \"vertical android : android : Il_parent \> \< Text View android : many hot dogs do you want to order?\" android : textAppearance=\" ? android : attr/textAppearanceLarge \" android . layout width=\"match_parent\" android . layout_height=\"wrap content\" android / \> (Edit Text android : \" android : \"wrap_content\" android : \<Button android : android : \"fil l_parent \" android : \"wrap_content\" android : now!\" / \> \< / LinearLayout\> ](003_Xamarin.Android_Fundamentals_009.png){width="5.0in" height="2.4166666666666665in"}

 

 

 

![](003_Xamarin.Android_Fundamentals_010.png){width="5.0in" height="3.075in"}

 

 

There is something important to note about our code for the Activities and the Views....and that is the Resources designer file.

 

![](003_Xamarin.Android_Fundamentals_011.png){width="5.0in" height="2.2083333333333335in"}

 

 

Notice that the path for the View ALMOST matches the actual folder allocation designed through Visual Studio. The truth about this logic is that the value that we are passing is MORE OR LESS an INTEGER. But, how ? Well, That\'s where the Resources.Designer comes into place.

 

The Resource.Designer.cs is a file automatically created and Maintained by Xamarin. All resources that we create inside the Resources folder, will get a value in the Designer class. In my head I image it to be like the .csproj file in popular C# application.

 

![public partial class Layout // aapt resource value: ex7ft3eeee public const int Main = 213ege3e4e; static Layout() global : : Android . Runtime. ResourceIdManager . UpdateIdVa1ues ( ) ; The \"Magic\' : Resource.Designer.cs ](003_Xamarin.Android_Fundamentals_012.png){width="5.0in" height="2.325in"}

 

![Accessing Controls from Code \<Button android : \'l@+id/MyButton \" android : \" fill_parent \" android : wrap_content \" android : text: ring/He1101\' public partial class Resource public partial class Id public const int MyButton = static Id() 2131034112; global : :Android . Runtime . Resou rceIdManager . UpdateIdVa1ues() ; ](003_Xamarin.Android_Fundamentals_013.png){width="5.0in" height="3.216666666666667in"}

 

 

In this case Notice how we are setting MyButton to ALSO have an ID in the Resource values.

 

This logic is IMPORTANT in order to access a Control from an Activity.

 

![Accessing Controls from Code protected override void OnCreate(Bund1e bundle) base. OnCreate(bund1e) ; // Set our view from the \"main\" layout resource SetContentView( Resource . Layout . Main) ; // Get our button from the layout resource, // and attach an event to it Button button = .MyButton) ; button. Click delegate { button . Text = string. Format(\" {0} clicks!\' count++) ; ](003_Xamarin.Android_Fundamentals_014.png){width="5.0in" height="2.8833333333333333in"}

 

 

 

 

![Application Manifest Images \*.axml Manifest file Activities Icons Other ](003_Xamarin.Android_Fundamentals_015.png){width="5.0in" height="2.85in"}

 

 
