# [code-server](https://github.com/cdr/code-server)

Run [VS Code](https://github.com/microsoft/vscode) on the [CS department](https://www.cs.hku.hk/)'s [`academy`](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/account.jsp#login) server and open it in your local device's browser. 

### Current method of coding on `academy` server

- CLI Text editors such as [VIM](https://github.com/vim/vim), [GNU nano](https://www.nano-editor.org/) in terminal after [SSH](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/ssh.jsp#connectcs) in a terminal;
- GUI Text editors such as [Gedit](https://gitlab.gnome.org/GNOME/gedit), [Atom](https://github.com/atom/atom) after connecting via [X2Go](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/x2go/index.jsp);
- Using local text editors to open files over SFTP connection;
- ...

### Why code-server?

It resembles the [CS50 IDE](https://ide.cs50.io/) used by [Harvard University](https://www.harvard.edu/)'s [CS50](https://cs50.harvard.edu/) and is even more powerful. It provides access to file manager, terminal emulator, text editor, a huge selection of extensions and so much more, in a browser; 

It is easier to get used to than Vim and nano; 

It requires less bandwidth than X2Go and hence is a lot smoother; 

It provides an integrated coding environment so you don't have to switch apps between writing and compiling; 

...

### Installation

Since students don't have root privileges on department servers, installation process can be a bit tricky. 

Use the [Standalone Releases](https://github.com/cdr/code-server/blob/main/docs/install.md#standalone-releases) of the code-server repo to install. 

### Running

On `academy11`/`academy21`, run `code-server`. This will have code-server running. Check out the port number (`<port_number>`) it is running on. 

Or better, I recommend using `code-server --port <port_number>` to specify a port number, but avoid using [commonly used ports](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers#Well-known_ports). (Think of a unique number unlikely to be thought of by others) This will help if you want to install a separate web app for VS Code on `academy`.

### Opening in local browser

Before opening in local browser, you should forward to ports to your local machine. 

If you are already connected to [HKUVPN](https://www.its.hku.hk/documentation/guide/network/remote/hkuvpn2fa), just run [**Step 2**](#step-2). Otherwise, you need to run [Steps **1 and 2**](#step-1).

#### Step 1
```bash
ssh -L <port_number>:localhost:<port_number> <account>@gatekeeper.cs.hku.hk
# you can substitute gatekeeper with gatekeeper2 if gatekeeper is too busy
```

#### Step 2
```bash
# if you are running code-server on academy11
ssh -L <port_number>:localhost:<port_number> <account>@academy11.cs.hku.hk
# or,
# if you are running code-server on academy21
ssh -L <port_number>:localhost:<port_number> <account>@academy21.cs.hku.hk
```

Open `localhost:<port_number>` in your local browser. It should prompt you to input a password, just check out the file it mentions for password. 

And, you are in!

### Change password and hide your password

Anything you store on the department server is accessible by the department (The same goes for the University and you Google Drive, Microsoft OneDrive, etc on your University account). DO NOT STORE ANYTHING PERSONAL IN PLAINTEXT, including passwords. 

In the file storing your password, change `password` to `hashed-password` and hash a password of your choice. See [Guide](https://github.com/cdr/code-server/blob/v3.8.0/doc/FAQ.md#can-i-store-my-password-hashed). 

### Install it as a separate app

On browsers such as Google Chrome, you can install the webpage as a [separate web app](https://support.google.com/chrome_webstore/answer/3060053?hl=en). 

If you run every time with your own port number (`<port_number>`) in [**Running**](#running), and that port number is not likely to be already taken by others, then you can use that port every time and your port web app would still work. 

### Extensions

Note that not all extensions will work. Some of them require certain packages to be installed on the server and since you don't have root privileges that's not possible. 

Still a large number of extensions will work. For example, [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) will help you compile and run code. Just remember to go to the extension's settings and add arguments `-pedantic-errors -std=c++11` after `g++` in `code-runner.executorMap`'s `cpp` entry. 

### Update

When there is an update, it will prompt you with the message. Or, you could also take notice of the development of code-server yourself, watching their repo.

Because the app is a few hundred MB, and you only have a 5GB disk quota on academy, you need to delete the old version when installing the new version.

Differences to initial install:

Before `ln -s ~/.local/lib/code-server-<new-version>/bin/code-server ~/.local/bin/code-server`, execute `rm ~/.local/bin/code-server` and `rm -rf ~/.local/lib/code-server-<old-version>` (of course, replace `<old-version>` with the version of the older app), the first you must do before the `ln` line, the latter you can do afterwards.
