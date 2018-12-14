# kubernetes_snippets



kubectl check-health

kubectl describe nodes

kubectl get pods --all-namespaces | awk '{print $2}' | grep -v NAME | xargs -I POD kubectl logs POD -n kube-system  | grep -A3  -i error | less -S




