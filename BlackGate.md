make a privesc page about statuslines when home

<img width="862" height="309" alt="image" src="https://github.com/user-attachments/assets/9980cbf3-d9d4-4b31-bb54-27b0343f6b90" />

- just ssh and redis 4.0.14

found [this](https://github.com/n0b0dyCN/redis-rogue-server) GitHub link for Redis 4.x RCE
<img width="823" height="512" alt="image" src="https://github.com/user-attachments/assets/8051e4fa-3c5e-4d20-a53a-53789cbd32b6" />

- did reverse instead of more stability

put my ssh key in there and connected directly
<img width="730" height="744" alt="image" src="https://github.com/user-attachments/assets/cfd77b5e-83a8-4a2e-8cd2-f958a83c63a5" />


for proof
<img width="138" height="92" alt="image" src="https://github.com/user-attachments/assets/b69dfd4c-aaeb-4deb-aadc-022f059ef3e8" />



<img width="452" height="107" alt="image" src="https://github.com/user-attachments/assets/57ec2ae8-1e3f-409f-8558-7aac127f1716" />

- notes file in prudence home directory
	- protected mode is off


<img width="854" height="173" alt="image" src="https://github.com/user-attachments/assets/bcc5f7f2-83f5-4366-a6ee-81acebfb82ee" />

- can run redis as sudo


need an authorization key to use redis-status
<img width="256" height="96" alt="image" src="https://github.com/user-attachments/assets/88bdb8cb-8937-4db9-9605-d4ab3db9b39f" />


running strings on the binary gives the authorization key
<img width="642" height="331" alt="image" src="https://github.com/user-attachments/assets/e69050ce-ac45-47ef-ab18-4f93d3af32c4" />

```
ClimbingParrotKickingDonkey321
```


once in, type `!/bin/bash` to get root
<img width="500" height="126" alt="image" src="https://github.com/user-attachments/assets/e0166e8b-df7b-4282-a00b-f57115c04a93" />
<img width="370" height="92" alt="image" src="https://github.com/user-attachments/assets/22400baa-0d51-4618-85e2-57bb28799675" />


