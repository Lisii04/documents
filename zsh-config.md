# 安装并配置zsh
安装zsh:
```
sudo apt install zsh
```
再执行
```
sh -c "$(wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh -O -)" \
sed -i 's/ZSH_THEME=\"[a-z0-9\-]*\"/ZSH_THEME="af-magic"/g' ~/.zshrc \
sed -i 's/plugins=(git)/plugins=(git zsh-syntax-highlighting zsh-autosuggestions)/g' ~/.zshrc 
```
之后安装插件
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting && git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
最后
```
source ~/.zshrc
```
