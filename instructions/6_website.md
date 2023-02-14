# Customizing your Website
## Follow these steps to customize your website from the Linux terminal and learn more commands.

If you cannot yet see the `Red Hat Enterprise Linux Test Page` when you type in the following in a web browser, return to [step 5](./5_services.md), 
```
http://<ip-address>
```
Again, make sure to type in 'http' not 'https', sometimes web browsers will automatically switch it to 'https'. If this happens, use Firefox.

## Adding a Custom Homepage to your Website
* So now you have a website running, but it's not really that interesting. It doesn't feel like it's <i>yours</i> yet. 
* Let's get rid of this default test page by adding a homepage of our own!
* Website contents for httpd are stored in the directory `/var/www/html`.
* You may recognize 'www' from URLs you've seen before on the internet, and 'html' refers to Hyper-Text Markup Language. You can read more about HTML [here](https://www.hostinger.com/tutorials/what-is-html).
* As the `root` user, or with `sudo`, use the `touch` command to create a file called `index.html` in the /var/www/html directory.
```
touch /var/www/html/index.html
```
* If you return to your website, you'll notice that the `Red Hat Enterprise Linux Test Page` is no longer there. Great! But now we just have a boring white page.
* Let's first change into the /var/www/html directory:
```
cd /var/www/html
```
* Now use the `vi` command to open the 'visual' text editor and customize your newly created `index.html` file.
```
vi index.html
```
* Which will open an empty page that looks like this:
```

~
~
~
```
* To start editing, press the `i` key to enter 'insert' mode.
* Now go wild! Fill your index.html file with text, headers, colors, images! Customize to your hearts content! Do whatever you want with your website! Refer to this [HTML cheat sheet](https://web.stanford.edu/group/csp/cs21/htmlcheatsheet.pdf) for a quick guide on getting the most out of your customization.
* When you are done editing, hit the `Esc` key to exit 'insert' mode, then type `:wq` to 'write' (save) and 'quit'.
* If you want to quit without saving, do the same as above, except `:q!`
* To return editing your index file again, use the `vi` command again.
* <b>Pro Tip!</b> You can use the `Tab` key to autocomplete path and file names. Try it out the nex time you're typing in a filename, i.e. `vi in<tab>` and it should autocomplete the filename `index.html` for you.
## Creating Webpages
* Now that we have a homepage squared away (I hope you got creative!), you can create other pages for your website too.
* From the /var/www/html directory (`pwd` should return '/var/www/html'), create a sub-directory called `page2` (or anything you like) using the `mkdir` (short for 'make directory'):
```
mkdir page2
```
* Now create an `index.html` page for your new webpage:
```
touch page2/index.html
```
* You could customize this page too, if you like, and then go to your `http://<ip-address>/page2` and see that webpage. 
* Let's delete that for now though, using the `rm` (for 'remove') command.
```
rm page2/index.html
```
Which will prompt you:
```
rm: remove regular file 'page2/index.html'? 
```
* Hit the `y` key for 'yes' and then Enter to delete it. 
* You can use the `-f` option for 'force' to avoid having to answer this prompt in the future. Be careful though! There's no equivalent to the 'Recycle Bin' by default, so once you delete a file, it's gone.
* You can also remove an empty directory using the `rmdir` command:
```
rmdir page2
```
* You can also delete directories with the `rm` command with the `-r` for 'recursive' option. When ombined with the `-f` this can be a powerful, and very dangerous command, especially when run as root, so be careful!

## Big Picture
Are you starting to see how to the internet is formed?
* It's all made up of servers exposing files to each other over publicly accessible networks. The files are get fancier, with [Javascript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript) and [CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/What_is_CSS), but the concepts are the same.
* And instead of using IP addresses to access those servers' files, we generally use names like [www.ibm.com](www.ibm.com) instead, right? These names are converted to IP addresses by [DNS](https://www.cloudflare.com/learning/dns/what-is-dns/) (or Domain Name System). You could [purchase a domain name](https://www.pcmag.com/news/how-to-register-a-domain-name-for-your-website) for your website so that people could more easily find and navigate to it!
* Although since we only have `http` set up, and not `https` (["What's the difference?](https://www.keycdn.com/blog/difference-between-http-and-https)), people would get a security warning before they got to your website.
* So although this is far from a full-fledged website, hopefully this helped you get a better picture of how the internet works, and you learned some Linux terminal skills along the way!

## Review
You've made it a long way in this tutorial of the basics of the Linux terminal. You now have the beginnings of a website, and you've learned some more commands:
* `touch <file>` to create a file
* `vi <file>` to edit a file
* `mkdir <directory>` to create a directory
* `rm <file>` to delete a file
* `rmdir <directory>` to delete a directory

## Hands-On Lab Complete!
* Nice work!! If you've made it this far, you're well on your well to becoming a Linux terminal pro!
* I hope this tutorial was helpful and interesting for you.
* You will have access to this server for about a week and a half, but you can request a two-week extension by emailing linux1@us.ibm.com
* If you have comments, questions, feedback concerns, I'd love to hear them! 
* Please reach out to me at jacob.emery@ibm.com
