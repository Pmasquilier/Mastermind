---
kindle-sync:
  bookId: '25999'
  title: 'Refactoring UI (Steve Schoger, Adam Wathan) (z-lib.org)'
  author: Unknown
  highlightsCount: 40
---
# Refactoring UI
## Metadata
* Author: [[Unknown]]

## Highlights
If you want an elegant or classic look, you might want to incorporate a serif typeface in your design: For a playful look, you could use a rounded sans serif: — location: [161]() ^ref-35217

---
If you’re going for a plainer look, or want to rely on other elements to provide the personality, a neutral sans serif works great: — location: [165]() ^ref-59357

---
As small of a detail as it sounds, if and how much you round the corners in your design can have a big impact on the overall feel. A small border radius is pretty neutral, and doesn’t really communicate much of a personality on its own: A large border radius starts to feel more playful: — location: [177]() ^ref-11187

---
…while no border radius at all feels a lot more serious — location: [182]() ^ref-50147

---
To pick the best option, start by taking a guess at which one will look best, maybe 16px. Then try the values on either side (12px and 24px) for comparison. Chances are, two of those options will seem like obviously bad choices. If it’s the options on the outside, you’re done — the middle option is the only good choice. — location: [221]() ^ref-26223

---
• A dark color for primary content (like the headline of an article) • A grey for secondary content (like the date an article was published) • A lighter grey for tertiary content (maybe the copyright notice in a footer) — location: [263]() ^ref-25556

Hiérarchiser Avec des couleurs

---
• A normal font weight (400 or 500 depending on the font) for most text • A heavier font weight (600 or 700) for text you want to emphasize Stay away from font weights under 400 for UI work — — location: [265]() ^ref-64284

Hierarchiser avec des fonts

---
Don’t use grey text on colored backgrounds — location: [276]() ^ref-9634

---
A better approach is to hand-pick a new color, based on the background color. Choose a color with the same hue, and adjust the saturation and lightness until it looks right to you: Hand-picking a color this way makes it easy to — location: [283]() ^ref-42806

---
For example, if you need to display inventory in an e-commerce interface, instead of “In stock: 12”, try something like “12 left in stock”. — location: [314]() ^ref-62697

---
De-emphasize the label by making it smaller, reducing the contrast, using a lighter font weight, or some combination of all three. — location: [325]() ^ref-28544

Quand on est obligé d'avoir label:value

---
If you’re designing an interface where you know the user will be looking for the label, it might make sense to the emphasize the label instead of the data. This is often the case on information-dense pages, like the technical specifications of a product. — location: [327]() ^ref-58182

---
Don’t de-emphasize the data too much in these scenarios; it’s still important information. Simply using a darker color for the label and a slightly lighter color for the value is often enough. — location: [331]() ^ref-42031

---
Unlike text, there’s no way to change the “weight” of an icon, so to create balance it needs to be de-emphasized in some other way. A simple and effective way to do this is to lower the contrast of the icon by giving it a softer color. — location: [359]() ^ref-26128

---
Primary actions should be obvious. Solid, high contrast background colors work great here. — location: [377]() ^ref-50128

---
Semantics are secondary • Secondary actions should be clear but not — location: [379]() ^ref-21207

---
prominent. Outline styles or lower contrast background colors are great options. • Tertiary actions should be discoverable but unobtrusive. Styling these actions like links is usually the best approach. — location: [380]() ^ref-23884

---
One of the easiest ways to clean up a design is to simply give every element a little more room to breathe. — location: [392]() ^ref-27358

Commencer par dnner bcp trop despace au debut et en supprimer pti a pti

---
If you want your system to make sizing decisions easy, make sure no two values in your scale are ever closer than about 25%. — location: [429]() ^ref-3550

---
When you’re building a type scale, don’t use em units to define your sizes. Because em units are relative to the current font size, the computed font size of nested elements is often not actually a value in your scale. — location: [606]() ^ref-15413

---
For the best reading experience, make your paragraphs wide enough to fit between 45 and 75 characters per line. The easiest way to do this on the web is using em units, which are relative to the current font size. A width of 20-35em will get you in the right ballpark. — location: [654]() ^ref-33833

---
Baseline, not center 120 When you align mixed font sizes by their baseline, you’re taking advantage of an alignment reference that your eyes already perceive. — location: [676]() ^ref-22414

---
-height and paragraph width should be proportional — narrow content can use a shorter line-height like 1.5, but wide content might need a line-height as tall as 2. — location: [692]() ^ref-23797

---
This means that for large headline text you might not need any extra line spacing, and a line-height of 1 is perfectly fine. — location: [698]() ^ref-41892

---
Line-height and font size are inversely proportional — use a taller line-height for small text and a shorter line-height for large text. — location: [700]() ^ref-15825

---
Don’t center long form text Center-alignment can look great for headlines or short, independent blocks of text. — location: [718]() ^ref-2800

---
But if something is longer than two or three lines, it will almost always look better left-aligned. If you’ve got a few blocks of text you want to center but one of them is a bit too long, the easiest fix is to rewrite the content and make it shorter: Not only will it fix the alignment issue, it will make your design feel more consistent, too. — location: [722]() ^ref-13244

---
If you’re designing a table that includes numbers, right-align them. When the decimal in a list of numbers is always in the same place, they’re a lot easier to compare at a glance. — location: [728]() ^ref-46324

---
Justified text looks great in print and can work well on the web when you’re going for a more formal look, but without special care, it can create a lot of awkward gaps between words: 131 Align with readability in mind To avoid this, whenever you justify text, you should also enable hyphenation: — location: [730]() ^ref-44162

---
You’ll need more greys than you think, too — three or four shades might sound like plenty but it won’t be long before you wish you had something a little darker than shade #2 but a little lighter than shade #3. In practice, you want 8-10 shades to choose from (more on this in “Define your shades up front”). Not so many that you waste time deciding between shade #77 and shade #78, but enough to make sure you don’t have to compromise too much. True black tends to look pretty unnatural, so start with a really dark grey and work your way up to white in steady increments. — location: [797]() ^ref-23274

---
Primary color(s) Most sites need one, maybe two colors that are used for primary actions, active navigation elements, etc. These are the colors that determine the overall look of a site — the ones that make you think of Facebook as “blue”. Just like with greys, you need a variety (5-10) of lighter and darker shades to choose from. — location: [805]() ^ref-47652

---
Accent colors On top of primary colors, every site needs a few accent colors for communicating different things to the user. For example, you might want to use an eye-grabbing color like yellow, pink, or teal to highlight a new feature: — location: [810]() ^ref-12880

---
All in, it’s not uncommon to need as many as ten different colors with 5-10 shades each for a complex UI. — location: [821]() ^ref-42122

---
There’s no real scientific way to do this, but for primary and accent colors, a good rule of thumb is to pick a shade that would work well as a button background. It’s important to note that there are no real rules here like “start at 50% — location: [833]() ^ref-38746

---
Next, pick your darkest shade and your lightest shade. There’s no real science to this either, but it helps to think about where they will be used and choose them using that context. The darkest shade of a color is usually reserved for text, while the lightest shade might be used to tint the background of an element. — location: [837]() ^ref-53403

---
Once you’ve got your base, darkest, and lightest shades, you just need to fill in the gaps in between them. For most projects, you’ll need at least 5 shades per color, and probably closer to 10 if you don’t want to feel too constrained. Nine is a great number because it’s easy to divide and makes filling in the gaps a little more straightforward. Let’s call our darkest shade 900, our base shade 500, and our lightest shade 100 — location: [845]() ^ref-39574

---
Small shadows with a tight blur radius make an element feel only slightly raised off of the background, while larger shadows with a higher blur radius make an element feel much closer to the user: The closer something feels to the user, the more it will — location: [1020]() ^ref-62885

---
attract their focus. — location: [1021]() ^ref-39588

---
Using shadows in a meaningful way like this is a great way to hack the process of choosing what sort of shadow an element should have. Don’t think about the shadow itself, think about where you want the element to sit on the z-axis and assign it a shadow accordingly. — location: [1042]() ^ref-60680

---
Add an overlay One way to increase the overall text contrast is to add a semi-transparent overlay to the background image. — location: [1117]() ^ref-42269

Quand Il y a un problème de lisibilité entre le texte et l'image

---
