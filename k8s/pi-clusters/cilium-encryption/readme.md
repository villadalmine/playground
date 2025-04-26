# Cluster Dev

In this cluster the goal is :


- Deploy basic cluster
  - basic rke2 
  - using the [labslabs rke2 ansible](https://github.com/lablabs/ansible-role-rke2)
  - all master or worker, it is not important now
- Configure cilium
  - encryption
    - nodeencryption
    - pod2pod strict
    - wireguard
  - envoy
  - kubeproxyReplacement
  - routing vxlan
  - Host routing bpf
- Test all cilium features

```
[dalmine@toolbox infra]$ ansible-playbook -i dev.yaml site.yaml -u dalmine -kk
PLAY RECAP ***********************************************************************
master01                   : ok=36   changed=5    unreachable=0    failed=0    skipped=38   rescued=0    ignored=0   
master02                   : ok=36   changed=11   unreachable=0    failed=0    skipped=35   rescued=0    ignored=0   
```



# Deploy the cluster




  After deploy it, i just removed the taint to work with master nodes. Maybe there is in the ansible some option to do it.

  ```
   kubectl taint nodes master01 node.cloudprovider.kubernetes.io/uninitialized=true:NoSchedule-
   ```



## Access

In the folder where you run the ansible command you have the kubeconfig file. Remember to edit the server with the ip you configured to reach the kube-api.

```
 export KUBECONFIG=var/home/dalmine/Nextcloud/Repos/infra/rke2.yaml
[dalmine@toolbox infra]$ kubectl  get nodes
NAME       STATUS   ROLES                       AGE     VERSION
master01   Ready    control-plane,etcd,master   11m     v1.32.3+rke2r1
master02   Ready    control-plane,etcd,master   8m46s   v1.32.3+rke2r1
[dalmine@toolbox infra]$ 

```