# Troubleshooting
## Use these helpful tips to get yourself out of sticky situations in the Linux terminal.
* <b>Lost</b>
    * In the directory structure? Go back home:
        ```
        cd ~
        ```
* <b>Unsure</b> 
    * Of how to use any command and its options? Use `man` to get the manual. Hit `q` to quit the manual:
        ```
        man <command-to-lookup>
        ```
* <b>Stuck</b> 
    * And can't do anything? 
    * Try hitting the control and c keys together: `Ctrl+C`. Commonly needed when you see a carrot like this: `>` in a new line and nothing else.
    * If you are stuck in the `vi` editor, hit the `Esc` key, and then type `:q!` to quit without saving or `:wq` to save and exit.
    * If you need a compelete reset, logout with `exit`:
        ```
        exit
        ```
    * If you are the root user, you will have to `exit` twice. Once to logout of the root user, and once to logout of the server entirely.
* <b>Frozen?</b>
    * If you can't do anything at all... no keys are working, no responses. Then most likely your terminal session timed-out, especially if this is after leaving and coming back after some time. In this situation, close the terminal window and re-initiate your SSH session via Terminal (Mac) or PuTTY (Windows).