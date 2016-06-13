powerline
=========

Powerline configs for gnome-terminal. Tested and configured on **Ubuntu-16.04** under **gnome-terminal**.
Please note, this instruction (fonts installation part) will not work under any terminal emulator. It's confirmed to work under **gnome-terminal**, but it aslo should work under **konsole**.

For further info please refer:
https://powerline.readthedocs.org/en/latest/

Screenshots
-----------
* bash shell example (running local shell with python virtualenv activated):
![bash shell look1](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_shell.png)
* bash shell example (running remote shell via SSH):
![bash shell look2](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_shell2.png)
* vim statusline example (normal mode):
![vim look1](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_vim1.png)
* vim statusline example (replace mode):
![vim look2](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_vim2.png)


Requirements
------------
* git (```sudo apt-get install git```)

Installation
------------

Installation consists of two parts:
* Installing fonts for terminal emulator (**gnome-terminal** or **konsole**) - this should be done on a PC you're going to run terminal emulator on.
* Installing and configuing **powerline** shell prompt on needed hosts for needed shell users.

### Installing fonts
**Ubuntu 16.04:**

```bash
sudo apt-get install fonts-powerline
```

You may need to restart your terminal emulator in order to apply changes.

### Installing and configuring powerline shell prompt
On a host you want to enable **powerline** shell prompt:

* install packages:

```bash
sudo apt-get install powerline python3-powerline
```

* run the following commands under needed shell user, this user should have ```bash``` shell:

```bash
# configure powerline
sed -i '1i term screen-256color' ~/.screenrc
git clone https://github.com/adidenko/powerline ~/.config/powerline

# enable in vim
echo "set laststatus=2" >> ~/.vimrc
echo -e "python3 from powerline.vim import setup as powerline_setup" >> ~/.vimrc
echo -e "python3 powerline_setup()\npython3 del powerline_setup" >> ~/.vimrc

# enable in shell
echo ". /usr/share/powerline/bindings/bash/powerline.sh" >> ~/.bashrc

# configure TERM variable to work properly under gnome-terminal with and without screen
echo 'if [ "$TERM" != "screen-256color" ] ; then' >> ~/.bashrc
echo -e "\texport TERM=xterm-256color\nfi" >> ~/.bashrc
```

That's it, now you should have **powerline** shell prompt and vim status line.
