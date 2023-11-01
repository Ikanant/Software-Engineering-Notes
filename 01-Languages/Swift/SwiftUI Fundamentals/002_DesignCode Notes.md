DesignCode Notes

Tuesday, May 24, 2022

9:19 PM

**CANVAS**

![// Canvas is a simple wrapper // Context: Allows us to draw // Size: Gives me the size of Canvas { context, size in context . stroke( that gives me the conte. graphics the actual canvas Path(ellipseln: CGRect(origin. • . zero, with: . color( .green), lineWidth: 4) size: s: ](002_DesignCode_Notes_000.png)

The question really is, why use a Canvas instead of just a regular VIEW? The true advantage is when we compose things as a GRAPHIC and that will give me a performance gain... SPECIALLY when I start animating things.... I should think of a whole Canvas as an Animate asset that\'s gonna be performant.

![struct BackgroundB10b: View { var body: some View { // Canvas is a simple wrapper that gives me the context and the size. // Context: Allows us to draw graphics // Size: Gives me the size of the actual canvas Canvas { context, size in context . stroke(l Path(ellipseln: CGRect(origin: . zero, size: size)), . color( .green), with: lineWidth: 4) context . fill( Path(ellipseln: CGRect(x: lee, y: 100, with: . color( .blue)) context .draw( Image( \"Blobl\"), in: CGRect(x: 200)) . frame(width: 30, height: 20) . border (Color. blue) width: 100, height: 10)), 0, y: e, width: 20, height: ](002_DesignCode_Notes_001.png)
