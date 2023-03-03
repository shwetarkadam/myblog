+++
title = "Today I learnt : Kubectl commands for debugging"
author = ["Shweta Kadam"]
date = 2023-03-03T23:10:00+05:30
tags = ["til", "kubectl", "debugging"]
draft = false
+++

Today I learnt a few kubectl commands which I used to for debugging a few issues in testing environment at work.


## To check logs {#to-check-logs}

```kubectl
kubectl logs  -f pod_name
```

Useful when you need to check logs inside a pod.


## To get the bin bash inside a pod {#to-get-the-bin-bash-inside-a-pod}

```kubectl
kubectl --exec --stdin --tty podname --bin/bash
```

This is useful command to check for certain versions or debugging which is done
This command was helpful for determining Java versions inside the pod which was used in a particular environment.
Anytime you want to run terminal commands such as `java --version` Or something similar to execute commands which need a bash shell.This is a good approach.
Helps to know which dependencies a pod uses.


## Scale up and downscale your pod {#scale-up-and-downscale-your-pod}

```kubectl
kubectl scale deployment <application-name> --replicas=0
kubectl scale deployment <application-name> --replicas=1
```

If your company uses a UI to scale up application pods and that UI tests your patience then this is a quick fix(Not recommended in PROD).


## Get description of your pod. {#get-description-of-your-pod-dot}

```kubectl
kubectl describe services
```

This commands gives general information regarding image IDs.
If your company uses Jenkins to make builds and then deploys them uses kubernetes,and if you need a way to verify if Jenkins deployed that particular build.This one helps as you can cross verify that information using attributes such as (sha)
