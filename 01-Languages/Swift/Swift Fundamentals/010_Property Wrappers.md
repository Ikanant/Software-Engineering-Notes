Property Wrappers

Monday, May 16, 2022

6:38 PM

So in SwiftUI, by changing the property \@State, you can trigger UI reloads... this is something cool for making things interactive in live iOS application. We can do something like:\
![Created by Brian Advent on 14.06. 19. Copyright s 2e19 Brian Advent. All rights reserved. Swi ContentView View \@State var favsOnIy = false \@State displayAIert = - \@EnuironmentObject dataStore:DataStore ](010_Property_Wrappers_000.png)

This is very efficient because SwiftUI uses a diffing algorithm to understand changes and updates ONLY to corresponding views. These properties marked with **\@State** in a special separated memory where only corresponding views can access them.

\@State is an example of a Property Wrapper

<https://www.swiftbysundell.com/articles/property-wrappers-in-swift/>

**[PROPERTY WRAPPERS]**

Make a generic type usable as an attribute.

| **Content Type**                                    | **Price** |
|-----------------------------------------------------|-----------|
| Individual Photo (including 6 months digital rights | \$100     |
| Individual Video (including 6 months digital rights | \$300     |
| Instagram Story                                     | \$125     |
| Instagram Photo                                     | \$300     |
| Instagram Reel / TikTok                             | \$600     |

Based on your deliverables:\
| **Content Type**                        | **Price** | **Quantity** | **Total**     |
|-------------------------------------|----------|------------|--------------|
| Instagram Photo                         | \$300     | 2            | \$600         |
| Instagram Story                         | \$125     | 5            | \$625         |
| Instagram Reel                          | \$600     | 1            | \$600         |
| TikTok (Assuming I can re-use the Reel) | \$600     | 2            | \$600         |
| Individual Photo                        | \$100     | 7-10         | \$700-\$1,000 |

\$200 - Individual Photograph (including 6 months digital rights)

\$300 - Individual Short video (including 6 months digital rights)

\$125-\$250 - Story

\$310-\$500 - Instagram Photo

\$500-\$550 - Carousel

\$700-1000 - Video

**What they want:**

[7-10 Images: \$2000]

2 Instagram Photos: \$620

5 Stories: \$625

Adding Stories to Highlight

1 Instagram reel: \$700

2 TikToks: \$1,400

\$2645
