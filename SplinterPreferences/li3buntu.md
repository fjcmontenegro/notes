#### install i3
`sudo apt install i3`

#### natural scrolling
Add `exec --no-startup-id synclient NaturalScrolling=1 VertScrollDelta=-113` to _~/.config/i3/config_

#### install sublime-text
```
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
```
