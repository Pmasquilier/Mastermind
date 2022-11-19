---
deck: Mastermind my memory::Javascript
---

<!-- basicblock-start oid="ObsViT5CimXUK4szOFW6CKEd" -->
**How to represent Unicode characters using only ASCII characters in JS ?**::
To support programmers and systems using older technology, JavaScript defines escape sequences that allow us to write [[Unicode]] characters using only [[ASCII]] characters. 

These Unicode escapes begin with the characters \u and are either followed by exactly four hexadecimal digits (using uppercase or lowercase letters A–F) or by one to six hexadecimal digits enclosed within curly braces. 

**Exemple :**
café peut s'écrire caf\u00e9 ou caf\u{E9}

Early versions of JavaScript only supported the four-digit escape sequence. **The version with curly braces was introduced in ES6 to better support Unicode codepoints that require more than 16 bits**, such as emoji: 
console.log("\u{1F600}"); // Prints a smiley face emoji 
<!-- basicblock-end -->

<!-- basicblock-start oid="Obsh2LDJBYSXO40yG4eGtlq1" -->
**What to look out for when using non-ASCII characters in JS programs ?**::
If you use non-ASCII characters in your JavaScript programs, you must be aware that **Unicode allows more than one way of encoding the same character**. 

The string “é,” for example, can be encoded as the single Unicode character \u00E9 or as a regular ASCII “e” followed by the acute accent combining mark \u0301. 

These two encodings typically look exactly the same when displayed by a text editor, but they have different binary encodings, meaning that they are considered different by JavaScript, which can lead to very confusing programs.

The Unicode standard defines the preferred encoding for all characters and specifies a normalization procedure to convert text to a canonical form suitable for comparisons. 
<!-- basicblock-end -->