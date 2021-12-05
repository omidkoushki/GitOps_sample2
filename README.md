# GitOps_Example

# Create flux namespace in k8s cluster

kubectl config current-context

kubectl create ns flux



    #Setup Fluxctl Binary 

sudo wget https://github.com/fluxcd/flux/releases/download/1.24.2/fluxctl_windows_amd64 -O /usr/bin/fluxctl && sudo chmod +x /usr/bin/fluxctl

fluxctl version

export GUSER=hamedfarv

fluxctl install \
--git-user=${GUSER} \
--git-email=${GUSER}@users.noreply.github.com \
--git-url=git@github.com:${GUSER}/GitOps_Example \
--git-path=kubernetes/configmaps,kubernetes/secrets,kubernetes/deployments \
--git-branch=main \
--namespace=flux | kubectl apply -f -

fluxctl list-workloads --k8s-fwd-ns flux

fluxctl sync --k8s-fwd-ns flux

fluxctl identity --k8s-fwd-ns flux


 ## unistall

flux uninstall --namespace=flux-system