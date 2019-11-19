# html-cleaner

If you draft emails in Google Docs and then copy and paste the content into your email client, your recipients sometimes would see annoying, unexpected line breaks that seem to be added at random. This web app fixes this issue for you. 

https://yymao.github.io/html-cleaner/ 

## Usage

1. Copy formatted text from Google Docs and paste it into the box.
2. Click "Remove white-space preservation" (this option fixes the "Google Docs -> Email" formatting issue, but preserves all other formatting), or, click "Remove all non-schematic formatting" (this will remove all non-schematic formatting like font size/family, linewidth etc). 
3. Re-select and copy the text from the box and paste into your email client.  

## A few things to note

- This software is provided "as is." Use it at your own risk.
- There are several other generic tools online (you can search for "html cleaner"), and they usually have more features than mine. Mine is pretty limited to solving the "Google Docs -> email" formatting issue. 
- All operations are done locally on the client side. No data is transmitted to the server or a third party. You can [check the source code](index.html) to be sure.
- You can also use this tool to fix an ill-formatted email that you received. While that is not the intended usage, it should still fix most formatting issues. 
- It works the best on Firefox, but should work fine on Chrome and Safari too. I am not certain if it works on IE/Edge at all. 
- Feel free to [open issues](https://github.com/yymao/html-cleaner/issues) if you see any; I'll try my best to address them (no guarantees though). 

## Technical details behind this formatting issue

_(No, you don't really care about this.)_

When copying formatted text from Google Docs, Google Docs need to insert some formatting CSS (i.e., the `style` tag) to the copied text to preserve the format. 
Among those CSS properties, one is `white-space: pre-wrap;`, which is to preserve sequences of white space and to interpret newline characters as line breaks ([ref](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space)). 
While this setting is useful in some cases, it becomes problematic when used in emails, because some email servers/clients may insert some newline characters in the HTML message when transmitting/rendering the message. 
Usually these newline characters should have no effect in HTML (they are just treated as regular space), but with the `white-space: pre-wrap;` CSS property, they become actual line break! 
That's why the formatting issue manifests as additional, unexpected line breaks. 

I should note that this issue is not really about Google Docs but about the interplay between email services and HTML, which is a mess to say the least. In practice, the simple fix is to just removes any occurance of `white-space: pre-*;`, which is exactly what the "Remove white-space preservation" option in this tool does. 
