=Topic 10 Ansible=

1. I list the ip@s of the pods using kubectl get po -o wide. In my case they were:
    1. 172.18.0.10
    2. 172.18.0.8
    3. 172.18.0.6
2. I wasn't able to change the configs inside the pods. I could change the manually by using kubectl exec vi and change what was necessary and by using kubectl cp I was able to copy the necessary files. Still I wasn't able to find a way for ansible to do this. One issue is that the pods are not exposed to the host network,  and the ips listed above are only accesible by the k8s internal network. I could possibly use port-forward for each of the necessary containers but I am sure there is a better solution to this that I couldn't find.
3. 
