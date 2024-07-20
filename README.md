- 👋 Hi, I’m @Ilegat
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Ilegat/Ilegat is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Navigation Menu
Sign in
ProgerXP
/
Orphus
Public
A Tiny Typo Reporter For Web Pages

License
 CC0-1.0 license
 17 stars  3 forks  Branches  Tags  Activity
Code
Issues
Pull requests
ProgerXP/Orphus
Folders and files
Name	
Latest commit
ProgerXP
ProgerXP
last year
History
original
4 years ago
LICENSE
4 years ago
README.md
last year
orphus-min.js
4 years ago
orphus-min.js.map
4 years ago
orphus-ru.js
4 years ago
orphus.js
4 years ago
orphus.php
2 years ago
screenshot.png
4 years ago
Repository files navigation
README
CC0-1.0 license
Orphus.js - A Tiny Typo Reporter
Orphus is a tiny zero-configuration typo reporter for web pages.

6K minified, 2K gzipped, no dependencies
invoked by Ctrl+Enter
reports arriving by e-mail (by default)
CORS-friendly (no AJAX, using <iframe> + <form>)
cross-browser - supports even Internet Explorer 6
You can see it in action here, here or here. Read about patching for WordPress here (in Russian).

Screenshot

Installation
Frontend (JavaScript)
Put the following line anywhere inside <body> (not inside <head>):

<script src="https://proger.me/orphus.js"></script>
It's best put early in <body> so that Ctrl+Enter starts working without waiting for a long page to finish loading. Also, adding async or defer to that <script> improves performance (but defer has the same effect as putting <script> right before </body>).

If you want to configure Orphus, do this anywhere before that line. For example, by default reports are sent to /orphus.php but you can use the PHP script on my page without touching your backend:

<script>
  // Keys for what will become orphus.opt after loading.
  orphus = {
    action: 'https://proger.me/orphus.php',
    strings: {
      subject: 'Typo Reported',
    },
    // If using proger.me/orphus.php, tell me where to forward your reports:
    //email: 'you@example.com',
  }
</script>
orphus.js hooks onkeypress immediately after it was loaded (warning: document's properties onkeypress and onkeydown must not be used outside of Orphus).

Thereafter you can call its methods via the global orphus object which can be also used for configuration:

orphus.opt.strings.send = 'Отправить'
orphus.show()
Finally, write and include your own styles (you can take original/orphus-orig.css as a basis). Note: centering works best with #orphusp { box-sizing: border-box; }.

Self-Hosted (PHP 5.4+)
Follow the instructions above to install the frontend, then copy orphus.php to your web root (or change orphus.opt.action).

After that either edit the PHP script (not recommended) or create a new script orphus-local.php alongside the first and put your specific configuration there. At minimum, you need to set the recipient's e-mail address because for spam reasons ?email (orphus.opt.email) is ignored by default.

<?php
// orphus-local.php
$vars['email'] = 'webmaster@proger.me';
You can also override the texts, input variables, mail() function, etc. - see orphus.php for details.

License Information
Sadly, the license terms are not mentioned anywhere on the original project's page. However, it was abandoned since at least 2015 (see my forum post; archived version) so there should be no issue in using it.

I have written the server-side PHP reporting script from scratch and that one is released in public domain (CC0). My edits on orphus.js are also under CC0.

Attribution
http://www.orphus.ru - the original project's homepage
http://www.koterov.ru - the original author's homepage
Differences
These are in addition to differences described here:

exposed all methods and options via window.orphus
made it possible to initialize opt by setting window.orphus before the script was loaded
removed default email, changed homepage, renamed width to maxWidth (and changed from 550 to 650 pixels)
added new opt.strings.submitex and a try/catch in showFor()
removed showMethod variable (direct call by name), renamed showMethod() to showFor()
moved iframe, submitted and lastComment to self/window.orphus
moved email deobfuscation from run() to self.deobfuscate()
removed setting zIndex on #orphusp
removed the code for temporary hiding <select>s for IE <= 6
removed hardcoded margins (was min. X/Y 10px)
added the check for no ranges in getSelection() to avoid subsequent exception in getRangeAt(0) (can happen if user didn't click inside <body> since loading)
To Do
add background shader while #orphusp is visible
click on it works as Cancel
replace using onkeypress/onkeyup with addEventListener()
migrate CSS classes to BEM (will require changing existing stylesheets)
