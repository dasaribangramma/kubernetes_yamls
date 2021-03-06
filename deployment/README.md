Deployment provides declarative updates for Pods and ReplicaSets

we can use deployment for application upgrade and rollback the changes if
the desired function crashes. we can also scale the number of replicas for
the deployment as well.

#kubectl scale deployment/nginx-deployment --replicas=5

For example:
if we want to change the image for a deployment like from 1.7.9 to 1.9.1
which is upgrade of your applications

Set a deployment's nginx container image to 'nginx:1.9.1', and its busybox container image to 'busybox'.
#kubectl set image deployment/nginx busybox=busybox nginx=nginx:1.9.1

# Print result (in yaml format) of updating nginx container image from local file, without hitting the server
kubectl set image -f path/to/file.yaml nginx=nginx:1.9.1 --local -o yaml

Let’s update the nginx Pods to use the nginx:1.9.1 image instead of the nginx:1.7.9 image.
#kubectl --record deployment.apps/nginx-deployment set image deployment.v1.apps/nginx-deployment nginx=nginx:1.9.1

or

kubectl set image deployment/nginx-deployment nginx=nginx:1.9.1 --record

Tp update anotation with the changes caused:
#kubectl annotate deployment.v1.apps/nginx-deployment kubernetes.io/change-cause="image updated to 1.9.1"

How to update resources for a deployment:

#kubectl set resources deployment.v1.apps/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi

root@kubernetesmaster:~# kubectl rollout
Manage the rollout of a resource.

Valid resource types include:

  *  deployments
  *  daemonsets
  *  statefulsets

Examples:
  # Rollback to the previous deployment
  kubectl rollout undo deployment/abc

  # Check the rollout status of a daemonset
  kubectl rollout status daemonset/foo

Available Commands:
  history     View rollout history
  pause       Mark the provided resource as paused
  restart     Restart a resource
  resume      Resume a paused resource
  status      Show the status of the rollout
  undo        Undo a previous rollout

Usage:
  kubectl rollout SUBCOMMAND [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
root@kubernetesmaster:~#


HPA:
===
#kubectl autoscale deployment.v1.apps/nginx-deployment --min=10 --max=15 --cpu-percent=80


