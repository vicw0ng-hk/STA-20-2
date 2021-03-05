# [code-server](https://github.com/cdr/code-server)

Run [VS Code](https://github.com/microsoft/vscode) on the [CS department](https://www.cs.hku.hk/)'s [`academy`](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/account.jsp#login) server and open it in your local device's browser. 

### Current method of coding on `academy` server

- Text editors such as [VIM](https://github.com/vim/vim), [GNU nano](https://www.nano-editor.org/) in terminal after [`SSH`](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/ssh.jsp#connectcs)
- Text editors such as [Gedit](https://gitlab.gnome.org/GNOME/gedit), [Atom](https://github.com/atom/atom) after connecting via [X2Go](https://intranet.cs.hku.hk/csintranet/contents/technical/howto/x2go/index.jsp)
- Using local text editors to open files during SFTP connection.
- ...

### Why code-server?

It resembles the [CS50 IDE](https://ide.cs50.io/) used by [Harvard University](https://www.harvard.edu/)'s [CS50](https://cs50.harvard.edu/) and is even more powerful. It provides access to file manager, terminal emulator, text editor, a huge selection of extensions and so much more, in a browser. 

It is easier to get used to than Vim and nano. 

It requires less bandwidth than X2Go and hence is a lot smoother. 

It provides an integratd coding environment so you don't have to switch apps between writing and compiling.

...

### Installation

Since students don't have root privileges on department servers, installation process can be a bit tricky. 

Use the [Standalone Releases](https://github.com/cdr/code-server/blob/main/docs/install.md#standalone-releases) of the code-server repo to install. 

### Running

On `academy11`/`academy21`, run `code-server`. This will have code-server running. Check out the port number (`<port_number>`) it is running on. 

Or better, I recommend using `code-server --port <port_number>` to specify a port number, but avoid using [commonly used ports](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers#Well-known_ports). This will help if you want to install a separate web app for VS Code on `academy`.

### Opening in local browser

Before opening in local browser, you should forward to ports to your local machine. 

If you are already connected to [HKUVPN](https://www.its.hku.hk/documentation/guide/network/remote/hkuvpn2fa), just run step 2. Otherwise, you need to run Step 1 and 2.

#### Step 1
```
ssh -L <port_number>:localhost:<port_number> <account>@gatekeeper.cs.hku.hk
# you can substitute gatekeeper with gatekeeper2 if gatekeeper is too busy
```

#### Step 2
```
# if you are running code-server on academy11
ssh -L <port_number>:localhost:<port_number> <account>@academy11.cs.hku.hk
# or,
# if you are running code-server on academy21
ssh -L <port_number>:localhost:<port_number> <account>@academy21.cs.hku.hk
```
