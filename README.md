# OCP-Volume-Configmap-Secret

# OCP-Volume-part1

$ ls
pv01-claim.json pv02-claim.json volpod.yaml
$ oc get pv
NAME CAPACITY ACCESSMODES STATUS CLAIM REASON AGE
pv01 1Gi RWO,RWX Available 2d
pv02 2Gi RWO,RWX Available 2d
pv03 3Gi RWO,RWX Available 2d
[vagrant@rhel-cdk volume]$ oc get pvc

# OCP-Volume-part2 
$ oc create -f pv01-claim.json
persistentvolumeclaim "pv01-claim" created
[vagrant@rhel-cdk volume]$ oc get pvc
NAME STATUS VOLUME CAPACITY ACCESSMODES AGE
pv01-claim Bound pv01 1Gi RWO,RWX 8s
[vagrant@rhel-cdk volume]$ oc get pv
NAME CAPACITY ACCESSMODES STATUS CLAIM REASON AGE
pv01 1Gi RWO,RWX Bound blog/pv01-claim 2d
pv02 2Gi RWO,RWX Available 2d
pv03 3Gi RWO,RWX Available 2d

# OCP-Volume-part3

$ oc create -f volpod.yaml
pod "volpod" created
[vagrant@rhel-cdk volume]$ oc get pods
NAME READY STATUS RESTARTS AGE
bigredis 1/1 Running 0 1h
pod-with-secret 1/1 Running 0 5h
volpod 0/1 ContainerCreating 0 6s
[vagrant@rhel-cdk volume]$ oc get pods
NAME READY STATUS RESTARTS AGE
bigredis 1/1 Running 0 1h
pod-with-secret 1/1 Running 0 5h
volpod 1/1 Running 0 44s

