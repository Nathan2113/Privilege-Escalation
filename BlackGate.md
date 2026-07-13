make a privesc page about statuslines when home

![[Pasted image 20260713112710.png]]
- just ssh and redis 4.0.14

found [this](https://github.com/n0b0dyCN/redis-rogue-server) GitHub link for Redis 4.x RCE
![[Pasted image 20260713113643.png]]
- did reverse instead of more stability

put my ssh key in there and connected directly
![[Pasted image 20260713113957.png]]

for proof
![[Pasted image 20260713114032.png]]


![[Pasted image 20260713114046.png]]
- notes file in prudence home directory
	- protected mode is off

sudo version 1.9.1
![[Pasted image 20260713114238.png]]

![[Pasted image 20260713114349.png]]
- can run redis as sudo


need an authorization key to use redis-status
![[Pasted image 20260713114636.png]]

![[Pasted image 20260713115819.png]]
- maybe?


![[Pasted image 20260713115847.png]]
- another yellow

running strings on the binary gives the authorization key
![[Pasted image 20260713133324.png]]
```
ClimbingParrotKickingDonkey321
```


once in, type `!/bin/bash` to get root
![[Pasted image 20260713135505.png]]
![[Pasted image 20260713135552.png]]

