Custom Themes
A Theme is a set of files allowing to change the visual style of a presentation.
iA Presenter comes with a set of built-in themes ready to use with a responsive design, all available in two versions: Light or Dark.
Each theme has been named after a famous city: Tokyo, Paris, New York, Copenhagen…
Easy to remember, fun and playing with the image people have of certain locations: the color palette, the typography, the atmosphere… cities have strong design characteristics that you will hopefully find right away in our themes.

Users comfortable with HTML and CSS who want to get hands-on with making changes, keep reading.
You can change the style of a presentation at different levels:
Using a specific Theme and its CSS
Using presets
Depending on your slide content (auto-layout)
By defining CSS variables in the Style Inspector.
Theme structure

Themes assets.
Presets (Predefined sets of CSS variables)
Custom fonts
Theme CSS definitions
Theme thumbnail
Theme definition
Slides HTML structures
A presentation has a collection of slide containers and a collection of slides backgrounds.
Each slide generates a slide container and a slide background DIVs.
the slide background has the same layout CSS class as the slide container
If there are no footnotes, the footnotes DIV has a 0 height.
If there are no header and footer, the slide content occupies all the available space.
You can choose to hide headers/footers on a per layout basis (see below for list of classes): .cover-container .header{ display:none;} for instance.

Layouts
Cover
Container CSS Class: .cover-container
Slide Content CSS Class: .layout-cover

Title
Container CSS Class: .title-container
Slide Content CSS Class: .layout-title

Section
Container CSS Class: .section-container
Slide Content CSS Class: .layout-section

Split
Container CSS Class: .v-split-container
Slide Content CSS Class: .layout-v-split

Grid
Container CSS Class: .grid-container
Slide Content CSS Class: .layout-grid

The Grid layout also has a CSS class indicating the number of grid cells at the slide content DIV level: grid-items-2 , grid-items-3 , grid-items-4 , etc…
Caption
Container CSS Class: .caption-container
Slide Content CSS Class: .layout-caption

Image Title
Container CSS Class: .title-image-container
Slide Content CSS Class: .layout-title-image

Default (text)
Container CSS Class: .default-container
Slide Content CSS Class: .layout-default

Custom fonts
You need to follow these steps to add a custom font to your theme:
1. Add the font files to your theme folder
Roboto-Slab-Regular.woff2
Roboto-Slab-Bold.woff2
2. Reference these fonts at the beginning of your CSS
@font-face {
  font-family: 'Roboto Slab';
  font-style: normal;
  font-weight: 400;
  src: url(Roboto-Slab-Regular.woff2) format('woff2');
}
@font-face {
  font-family: 'Roboto Slab';
  font-style: normal;
  font-weight: 700;
  src: url(roboto-slab-Bold.woff2) format('woff2');
}
3. Inform metadata
A. In template.json
  "TitleFont": "New York",
  "BodyFont": "New York",
Here you need to inform the display name of your custom fonts. That's the name that will appear in the Style Inspector. Above is an example for the New York font.
B. In presets.json
"TitleFont": "-apple-system-ui-serif, ui-serif",
"BodyFont": "-apple-system-ui-serif, ui-serif",
Here you need to inform the CSS name of your custom font. Above is an example for the New York font. You will notice the name is different than the display name.
NOTE: You could directly set your custom font in CSS but you would lose the ability to override it using the Style Inspector.
Using images from your Theme in CSS
When your custom Theme is installed, iA Presenter preserves the directories structure.
You can then reference an image using the url(...) function. Example:
.backgrounds .default-container{
  background-image: url("image1.jpg");
  background-size: cover;
  background-position: center;
}
Alignments
You need to target the inner div of each layout (see table above).
Example:
.layout-cover > div {
    justify-content: flex-end; /* vertical alignment */
    align-items: flex-start; /* horizontal alignment */
}
Horizontal alignment
Property: align-items
Alignment	Value
Left	flex-start
Center	center
Right	flex-end
Vertical alignment
Property: justify-content
Alignment	Value
Top	flex-start
Center	center
Bottom	flex-end
Backgrounds
You can use regular bitmap images (.jpg, .png) but Presenter also supports SVG backgrounds.
Background images can also be inlined directly in the CSS as shown below.
You can target a specific layout:
.backgrounds .v-split-container{
  background-image: url('data:image/svg+xml;utf8,<svg viewBox="0 0 1024 600" xmlns="http://www.w3.org/2000/svg" xml:space="preserve" fill-rule="evenodd" clip-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="2"><path fill="red" d="m541.526-57.455 584.065 49.14-56.35 669.755-584.065-49.14z"/></svg>');
  background-size: cover;
  background-position: center;
}
If you use inline SVG as url, directly in your CSS files, you need to take care of how you declare colors. Colors in hexadecimal format (like #FFFFFF) will break your CSS. You will need to use instead of the rgb(0,0,0) format.
If you want to target all backgrounds, whatever is the layout, target the .slide-background class.
Gradient background
You need to define 2 different gradients: one per appearance (Light/Dark)
These gradients are defined in the presets.json file
Example:
{
  "Presets": [
    {
      "Name": "Default",
      "TitleFont": "system-ui",
      "BodyFont": "system-ui",
      "Appearance" : "dark",
      "DarkBodyTextColor": "#000000",
      "LightBodyTextColor": "#ffffff",
      "DarkTitleTextColor": "#000000",
      "LightTitleTextColor": "#ffffff",
      "DarkBackgroundColor": "transparent",
      "LightBackgroundColor": "transparent",
      "Accent1": "#f94144",
      "Accent2": "#43aa8b",
      "Accent3": "#f9c74f",
      "Accent4": "#90be6d",
      "Accent5": "#f8961e",
      "Accent6": "#577590",
      "LightBgGradient":[
          "#c7e7ff",
          "#f0c8ff",
          "#ffdada",
          "#ffebb2"
      ],
      "DarkBgGradient":[
          "#15354c",
          "#3e154c",
          "#4c2828",
          "#4c3900"
      ],
    },...
Appearances
iA Presenter uses the .dark and .light CSS classes.
These classes are set per layout.
You can force the appearance for a specific layout in a custom Theme, in the template.json file
Example: { "Name": "New York", "Version": 0.1, "Author": "iA", "ShortDescription": "Stylish, bold, classy.", "LongDescription": "Stylish, bold, classy\n- Different sizes for headlines\n- Simple color background\n- Default white on black\n- Default font: New York", "Css": "newyork.css", "TitleFont": "New York", "BodyFont": "New York", "Layouts":[ { "Name": "Cover", "Classes": "invert", }, { "Name": "Title", "Classes": "invert", } ] }
Responsiveness
The themes are responsive. By default, CSS applies to mobile devices. If you want to target non-mobile devices:
@media (min-width: 768px) {
...
}
You can add additional breakpoints if, for instance, you want to provide different font-size/margins depending on the viewport size. However, iA Presenter already has its logic, and defaults should be enough.
Developing custom themes
Create a new Theme: Go to Preferences → Themes. Click on Create New and enter a name.
Navigate to the new Theme files: Click on the Reveal Themes folder in Finder button. Navigate then to the folder of the newly created Theme.
Use your new Theme: Open a presentation, go to the Style Inspector, and set the newly created Theme.
Bring your modification: Open your Theme.css in your preferred editor and add your custom CSS.
iA Presenter monitors the used Theme and will reload the Preview each time you change it.
