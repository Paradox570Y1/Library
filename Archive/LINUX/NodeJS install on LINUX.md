1. Install curl
```
sudo apt-get install curl
```
2. Install `nvm` (Node Version Manager)
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```
3. Verify if nvm is installed
```
command -v nvm 
// it should return nvm (otherwise reopen ubuntu terminal)

nvm ls  
// to check currently installed version of node.
```
4. Install current stable LTS release of node
```
nvm install --lts
//to install
```
now check for version
![[Pasted image 20241217184045.png|300]]