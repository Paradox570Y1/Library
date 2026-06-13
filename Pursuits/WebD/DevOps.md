Three concepts of Devops:-
- CICD
- Containerization
- IAC

#### Problem 1
The wall of confusion: Suppose web team has made a website which is working locally  but when it is sent  to DevOps for deployment ,it was crashing .
- Bottle Necks
- Delays
- Normal Error

![[Pasted image 20241026172455.png]]

Sources
- CICD - Jenkins
- Containerization - Docker- K8s
- IAC - Terraforming
- provisioning - ansible
- M - rafana
![[Pasted image 20241026180723.png|200]]


morining mein ek developer atta hai, wo ek code likhta and github pe daalta hai , samjhlete ahi ke whatsapp mein status add krne ka feature add kiya, fir wo automatic build hota hai , test hota hai and then production mein jaata hai and after the webite will become live. Then evening monitering start hoti hai website ki







#### Reconciliation
- LHS = RHS where current state is LHS and desired state is RHS.
- git is reconciling , means keeping track of checkpoints you have been through while building the project.
- GitHub is software on top of git which allows you to centralize the reconciling system , hosting globally, so that you can see checkpoints of your co-workers too and collaborate with co-workers, managers etc.

Kubernetes
- it is a declarative framework.
- used in Microsoft architecture


## Github
- Different types to access the code
	- HTTPS - in case of public repo use HTTPS
	- SSH
	- GitHub CLI


Why to set your own ssh?
- if you use the default ssh then you will not have complete control of all git commands , if you setup your own ssh then you will get access to more commands.
To set your own ssh
![[Pasted image 20241027201204.png|300]]
Private key system pe , public key GitHub pe
![[Pasted image 20241027201335.png|330]]
in case of windows just remove --apple-use-keychain
![[Pasted image 20241027201636.png]]

## To know all commands related to some command
use 'man command'
![[Pasted image 20241027202042.png]]
this will open documentation
use :q to quit

## To use output of one command as input of another command
```bash
ls | grep "pattern"
```


![[Pasted image 20241027202550.png|400]]


![[Pasted image 20241027204623.png|400]]