


## Issue: The connection to the server 10.0.x.x:6443 was refused after restarting the VM where kubernetes master was installed using kubeadm

https://stackoverflow.com/questions/50386844/the-connection-to-the-server-10-0-x-x6443-was-refused-after-restarting-the-vm-w


UPDATE:

After restarting VM this is what I have to do to make the master node start:
```
sudo swapoff -a
sudo systemctl restart kubelet.service
```
Why? How can I fix it so that it starts without having to input that?


## Solution:

The problem is that if I stop the machine and restart it the master node seems to be down
Since it was kubeadm installation that worked properly before restarts, seems like Env var is missing after restart. Try to run this before kubectl get nodes:
```
export KUBECONFIG=/etc/kubernetes/admin.conf
```
If it starts normally, then you need to make sure that KUBECONFIG environment variable is properly configured upon restart either adding it to .bashrc or similar...

