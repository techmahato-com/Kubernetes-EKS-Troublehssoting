# Kubernetes-EKS-Troublehssoting
EKS Command cheatsheet and troubleshooting
# 
	kubectl config get-contexts
	kubectl config use-context arn:aws:eks:ap-south-1:5123456789:cluster/TM-Prod

# List Clusters:
	aws eks list-clusters
	
# Describe Cluster (for a specific cluster):
	aws eks describe-cluster --name <cluster-name>

# Cluster Version
	kubectl version
	
# Check Namespace
	kubectl get ns

# Describe Namespace:
	kubectl describe namespace <namespace-name>

# List Pods in a Namespace:
	kubectl get pods -n <namespace-name>

# Check Pods Running which Nodes.
	kubectl get po -n app -o wide

# Describe Pod in a Namespace:
	kubectl describe pod <pod-name> -n <namespace-name>

# List Services in a Namespace:
	kubectl get services -n <namespace-name>

# Describe Service in a Namespace:
	kubectl describe service <service-name> -n <namespace-name>


# Check how many pods running in which NodeGroup.
	k get po -n app -o wide | grep myapp-nodejs | awk '{print $7}' | sort | uniq -c
	
# List Nodegroups:
	eksctl get nodegroups --cluster=<cluster-name>
	
# Error: Error: could not create cluster provider from options: checking AWS STS access – cannot get role ARN for current session: operation error STS: GetCallerIdentity, failed to resolve service endpoint, an AWS region is required, but was not found

## Solution: he error message suggests that there is an issue with resolving the AWS region for the current session. To resolve this, you need to ensure that the AWS region is properly configured in your environment.

	eksctl get nodegroups --cluster=RCB-FAN-APP-Prod --region ap-south-1

# Describe Nodegroup:
	eksctl get nodegroup --cluster=<cluster-name> --name=<nodegroup-name>

# List Nodes in a Nodegroup:
	kubectl get nodes -l eks.amazonaws.com/nodegroup=<nodegroup-name>

# Describe Node:
	kubectl describe node <node-name>

# List Pods Scheduled on Nodes in a Nodegroup:
	kubectl get pods -o wide --field-selector spec.nodeName=<node-name>
	
# Troubleshoot Nodegroup Scaling:
		eksctl get nodegroup --cluster=<cluster-name> --name=<nodegroup-name> --output=json