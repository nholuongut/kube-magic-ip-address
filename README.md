# Magic IPs Address

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

is a Kubernetes daemonset to implement [magic IP addresses](https://github.com/nholuongut/kubernetes/issues), that are useful to serve [node-local services](https://github.com/nholuongut/kubernetes/issues/).

Magic IP addresses are static IP addresses that are well-known in your cluster. They are typically assigned to daemonset pods, so that the pods are accessible from other consumer pods that are collocated on the same nodes.

One of typical use-cases of this project is to connect your applicaton pod to a Datadog's dd-agent, agent pods. From your application, just point your tracer to the collector endpoint `169.254.210.210`. netfiler/iptables will redirect packets to the agent pod on the same node according to pod selector you've provided.

## Alternatives

A possible alternative to use `magic-ip-address` is to use the downward API to obtain the IP address of the node, while running the agent pod with `hostNetwork: true`. However, it has two downsides. One is that you have to open up your network to allow pods to directly access the nodes running them, which results in a extra attack surface. Another alternative would be to use a deployment, which means that you're giving up adding a meaningful node-related metadata(node's ip address, name, namespace, and labels that your application pod is running on) to the traces collected by the agents.

In contrast to the two alternatives, `magic-ip-address` allows you add meaningful node metadata to your application traces, without exposing the agent pods via the host network.

## How It Works

Under the hood, `magic-ip-address` periodically polls the Kubernetes API to find one of targeted daemonset pods that are collocated on the same node as the `magic-ip-address` pod, by matching the pod selector. The targeted daemonset pods are assigned the magic IP address like `169.254.210.210`, which can then be accessed by other pods.

## Developping kube-magic-ip-address

Once you've updated your scripts or Dockerfile, rebuild the docker image and push it by running:

```
$ emacs Makefile

# Bump APP_VERSION in the Makefile and then...

$ eval $(minikube docker-env)
$ dvm detect

$ make build publish
```

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: Nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)
* [PayPal.me](https://www.paypal.com/paypalme/nholuongut)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟
