If `vim` is the editor used by `git`, git will open `vim` for things such as amending commits or interactive rebase. Therefore, the buffer will be open according to the git action we are performing. After you're done, you save the changes and quit the buffer. Finally, git will take it from there and do the necessary actions.

If you want to quit the commit or the rebase w/o letting git perform any action, we can use `:cq` Ex command. This command will let you exit vim with error code sent to the process/application that called `vim`. This way, git will recieve the error and won't proceed with the action.

I typically use this often when I am in the middle of writing a commit message and realize that I need to check/change some things before committing.
