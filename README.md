powerline
=========

Powerline configs for gnome-shell. Tested and configured on **Ubuntu-13.10** under **gnome-shell**.
Please note, this instruction will not work under any terminal emulator. It's confirmed to work under **gnome-shell** only.

For further info please refer:
https://powerline.readthedocs.org/en/latest/

Screenshots
-----------
* bash shell example:
![bash shell look1](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_shell.png)
* bash shell example:
![bash shell look2](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_shell2.png)
* vim statusline example:
![vim look](https://raw.github.com/adidenko/adidenko.github.io/master/images/powerline/powerline_vim.png)

Requirements
------------
* pip (```sudo apt-get install python-pip```)

Installation
------------

Just run the following commands under the user you want to configure powerline for (does not require sudo privileges).

```bash
pip install --user git+git://github.com/Lokaltog/powerline

# make sure pip install finished successfully, then continue:

mkdir ~/.fonts.conf.d ~/.fonts
wget -O ~/.fonts/PowerlineSymbols.otf \
https://github.com/Lokaltog/powerline/raw/develop/font/PowerlineSymbols.otf
fc-cache -vf ~/.fonts
wget -O ~/.fonts.conf.d/10-powerline-symbols.conf \
https://github.com/Lokaltog/powerline/raw/develop/font/10-powerline-symbols.conf

mkdir ~/.config/powerline
cp -a ~/.local/lib/python2.7/site-packages/powerline/config_files/* ~/.config/powerline/

# enable in vim
echo "set laststatus=2" >> ~/.vimrc
echo -e "python from powerline.vim import setup as powerline_setup" >> ~/.vimrc
echo -e "python powerline_setup()\npython del powerline_setup" >> ~/.vimrc

# enable in bash
echo export PATH="\"\$PATH:$(readlink -f ~/.local/bin)\"" >> ~/.bashrc
echo ". $(readlink -f ~/.local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh)" \
>> ~/.bashrc

# configure gnome-shell profiles
sed -i '1i term screen-256color' ~/.screenrc
rm -rf /tmp/tmp_powerline && mkdir -p /tmp/tmp_powerline
git clone --depth 1 https://github.com/adidenko/powerline /tmp/tmp_powerline
cp -R /tmp/tmp_powerline/{colorschemes,themes,config.json} ~/.config/powerline/
rm -rf /tmp/tmp_powerline
```

Hints
-----
If you're not using screen, you may need to set your ```TERM``` env variable to something like this:

```bash
export TERM=xterm-256color
```
