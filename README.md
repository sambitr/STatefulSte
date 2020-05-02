# STatefulSte
```
kumar_sambit7@cloudshell:~ (sambit-kubernetes)$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
kubia-0                  1/1     Running   0          3m21s
kubia-1                  1/1     Running   0          2m52s
```

```
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubernetes.io/limit-ranger: 'LimitRanger plugin set: cpu request for container
      kubia'
  creationTimestamp: "2020-05-02T06:20:48Z"
  generateName: kubia-
  labels:
    app: kubia
    controller-revision-hash: kubia-c94bcb69b
    statefulset.kubernetes.io/pod-name: kubia-0
  name: kubia-0
  namespace: default
  ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: StatefulSet
    name: kubia
    uid: 109a0936-8c3d-11ea-a0e3-42010a9e0031
  resourceVersion: "467060"
  selfLink: /api/v1/namespaces/default/pods/kubia-0
  uid: 10a50648-8c3d-11ea-a0e3-42010a9e0031
spec:
  containers:
  - image: luksa/kubia-pet
    imagePullPolicy: Always
    name: kubia
    ports:
    - containerPort: 8080
      name: http
      protocol: TCP
    resources:
      requests:
        cpu: 100m
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/data
      name: data
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-dllt7
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  hostname: kubia-0
  nodeName: gke-cluster-1-default-pool-422d69a3-k4z2
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  subdomain: kubia
  terminationGracePeriodSeconds: 30
   tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: data
    persistentVolumeClaim:
      claimName: data-kubia-0
  - name: default-token-dllt7
    secret:
      defaultMode: 420
      secretName: default-token-dllt7
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2020-05-02T06:20:54Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2020-05-02T06:21:17Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2020-05-02T06:21:17Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2020-05-02T06:20:54Z"
    status: "True"
    type: PodScheduled
    containerStatuses:
  - containerID: docker://61b68377bac4b08da8517ed4ed7569ff72784376440f885a7a1352e6d73db5da
    image: luksa/kubia-pet:latest
    imageID: docker-pullable://luksa/kubia-pet@sha256:4263bc375d3ae2f73fe7486818cab64c07f9cd4a645a7c71a07c1365a6e1a4d2
    lastState: {}
    name: kubia
    ready: true
    restartCount: 0
    state:
      running:
        startedAt: "2020-05-02T06:21:16Z"
  hostIP: 10.158.0.3
  phase: Running
  podIP: 10.52.1.6
  qosClass: Burstable
  startTime: "2020-05-02T06:20:54Z"
```
<p>The names of the generated PersistentVolumeClaims are composed of the name defined in the volumeClaimTemplate and the name of each pod. You can examine the claims’ YAML to see that they match the template.</p>

```
kumar_sambit7@cloudshell:~ (sambit-kubernetes)$ kubectl get pvc
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
data-kubia-0   Bound    pvc-109e4ffa-8c3d-11ea-a0e3-42010a9e0031   1Gi        RWO            standard       14m
data-kubia-1   Bound    pvc-217db3fa-8c3d-11ea-a0e3-42010a9e0031   1Gi        RWO            standard       14m
```
```
kumar_sambit7@cloudshell:~ (sambit-kubernetes)$ kubectl get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS        CLAIM                  STORAGECLASS   REASON   AGE
mongodb-pv                                 1Gi        ROX,RWX        Retain           Terminating   default/mongodb-pvc                            23h
pv-a                                       1Mi        RWO            Recycle          Available                                                    21m
pv-b                                       1Mi        RWO            Recycle          Available                                                    21m
pv-c                                       1Mi        RWO            Recycle          Available                                                    21m
pvc-109e4ffa-8c3d-11ea-a0e3-42010a9e0031   1Gi        RWO            Delete           Bound         default/data-kubia-0   standard                16m
pvc-217db3fa-8c3d-11ea-a0e3-42010a9e0031   1Gi        RWO            Delete           Bound         default/data-kubia-1   standard                16m
kumar_sambit7@cloudshell:~ (sambit-kubernetes)$
```
