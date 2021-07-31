# 0. What does Kubernetes do?

- [k8s docs](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/#why-you-need-kubernetes-and-what-can-it-do).

# 1. K8s Components

[k8s docs](https://kubernetes.io/docs/concepts/overview/components/).

- Types of machines in a k8s cluster:
  * control plane node(s) (or just called control plane),
  * worker nodes (or just called nodes).
- control plane has
   * `kube-apiserver`: k8s API frontend,
   * `etcd`: key-value store for cluster data,
   * `kube-scheduler`: assigns resources to nodes based on current constraints,
   * `kube-controller-manager`: several control loops in one process,
   * `cloud-controller-manager`: several *cloud-specific* control loops in one process.
- worker nodes have
   * `kubelet`: manages containers deployed to that node,
   * `kube-proxy`: manages network rules on nodes,
   * Container Runtime: what runs the containers. Any implementation of the K8s
     Container Runtime Interface (e.g., CRI provided for Docker is the most common).

# 2. K8s API Objects

- Abstraction of Workload:
    * [__Pod__](https://kubernetes.io/docs/concepts/workloads/pods/): smallest deployable
      unit — holds one or more containers and runs it in a shared context
    * [Workload resources](https://kubernetes.io/docs/concepts/workloads/controllers/):
      Used to manage groups of Pods
        + [__Deployment__](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/): for managing stateless Pods
            + [__ReplicaSet__](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/):
              abstraction to manage a number of identical Pods. Typically not used
              directly.
        + [__StatefulSet__](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/):
          for managing stateful Pods (e.g., DBs)
- Abstraction of Storage
    * [__Volume__](https://kubernetes.io/docs/concepts/storage/volumes/): many
      types of volumes provided by plugins (local, network/distributed FS, cloud)
- Abstraction of Networking
    * [__Service__](https://kubernetes.io/docs/concepts/services-networking/service/)
    * [__Ingress__](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- Abstraction of Configuration
    * [__ConfigMaps__](https://kubernetes.io/docs/concepts/configuration/configmap/)
    * [__Secrets__](https://kubernetes.io/docs/concepts/configuration/secret/)

# 3. K8s

## Install minikube and kubectl

- <https://kubernetes.io/docs/tasks/tools/>
- <https://minikube.sigs.k8s.io/docs/start/>

- eval "$( kubectl completion bash )"
- eval "$( minikube completion bash )"

## Minikube

- `minikube start`

- `kubectl get nodes`

- `minikube status`

- `kubectl version`

- `minikube delete`

## Kubectl

- `kubectl get nodes`

- `kubectl get pod`

- `kubectl get pod -o wide`

- `kubectl get services`

- `kubectl create deployment nginx-deploy --image=nginx`

- `kubectl get deployment`

- `kubectl get replicaset`

- `kubectl edit deployment nginx-deploy`

- `kubectl logs [pod]`

- `kubectl exec -it {pod} -- bin/bash`

- `kubectl delete deployment nginx-deploy`

## MongoDB deployment

- taken from <https://gitlab.com/nanuchi/youtube-tutorial-series/-/tree/master/demo-kubernetes-components>

```
  kubectl apply -f mongodb/mongo-secret.yaml
  kubectl apply -f mongodb/mongo.yaml
  kubectl apply -f mongodb/mongo-configmap.yaml 
  kubectl apply -f mongodb/mongo-express.yaml
```

```
  kubectl get pod
  kubectl get pod --watch
  kubectl get pod -o wide
  kubectl get service
  kubectl get secret
  kubectl get all | grep mongodb
```

```
  kubectl describe pod mongodb-deployment-xxxxxx
  kubectl describe service mongodb-service
  kubectl logs mongo-express-xxxxxx
```

```
  minikube service mongo-express-service
```

# 4. Patterns / Applications

- <https://helm.sh/>
- <https://k3s.io/>

# 5. Alternatives

- [Docker Swarm](https://docs.docker.com/engine/swarm/)
- [HashiCorp Nomad](https://www.nomadproject.io/)

# Other resources

- [Kubernetes Tutorial for Beginners (FULL COURSE in 4 Hours)](https://www.youtube.com/watch?v=X48VuDVv0do)
   * <https://gitlab.com/nanuchi/youtube-tutorial-series/-/tree/master/>
- [Perlcon: Deploying Perl Apps using Docker, Gitlab & Kubernetes](https://perlcon.eu/talk/27)
- [Salt Lake Perl Mongers - 11/8/16 - Scott Wiersdorf - "High Availability Perl with Kubernetes"](https://www.youtube.com/watch?v=zqLdmNINhrY)
  *  <https://solitum.net/posts/high-availability-perl-with-kubernetes/>
  *  <https://github.com/scottw/ha-perl-k8s>
