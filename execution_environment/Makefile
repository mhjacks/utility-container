OPENSHIFT_CLIENT_VERSION=4.10.3
TKN_VERSION=0.24.0
YQ_VERSION=4.25.3
KUSTOMIZE_VERSION=4.5.5
PFX=context/bin

ee: download
	ansible-builder build --tag=hybridcloudpatterns-utility-ee

download: clean bin oc argocd helm azuretrim yq tkn kustomize

argocd:
	curl -sSL -o $(PFX)/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
	chmod 755 $(PFX)/argocd

helm:
	curl -sSL -o $(PFX)/helm https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/helm/latest/helm-linux-amd64
	chmod 755 $(PFX)/helm

kustomize:
	curl -sLfO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv$(KUSTOMIZE_VERSION)/kustomize_v$(KUSTOMIZE_VERSION)_linux_amd64.tar.gz
	tar xvf kustomize_v$(KUSTOMIZE_VERSION)_linux_amd64.tar.gz -C $(PFX)
	rm -f kustomize_v$(KUSTOMIZE_VERSION)_linux_amd64.tar.gz
	chmod 755 $(PFX)/kustomize

# We'll symlink kubectl in the container build process
oc:
	curl -sLfO https://mirror.openshift.com/pub/openshift-v4/clients/ocp/$(OPENSHIFT_CLIENT_VERSION)/openshift-client-linux-$(OPENSHIFT_CLIENT_VERSION).tar.gz
	tar xvf openshift-client-linux-$(OPENSHIFT_CLIENT_VERSION).tar.gz -C $(PFX)
	rm -rf openshift-client-linux-$(OPENSHIFT_CLIENT_VERSION).tar.gz
	rm -f $(PFX)/kubectl
	rm -f $(PFX)/README.md

azuretrim:
	curl -sSL -o $(PFX)/azure_sdk_trim.py https://raw.githubusercontent.com/clumio-code/azure-sdk-trim/main/azure_sdk_trim/azure_sdk_trim.py
	chmod 755 $(PFX)/azure_sdk_trim.py

tkn:
	curl -sLfO https://github.com/tektoncd/cli/releases/download/v$(TKN_VERSION)/tkn_$(TKN_VERSION)_Linux_x86_64.tar.gz
	tar xvf tkn_$(TKN_VERSION)_Linux_x86_64.tar.gz -C $(PFX)
	rm -rf tkn_$(TKN_VERSION)_Linux_x86_64.tar.gz
	chmod 755 $(PFX)/tkn
	rm -f $(PFX)/LICENSE
	rm -f $(PFX)/README.md

yq:
	curl -sSL -o $(PFX)/yq  https://github.com/mikefarah/yq/releases/download/v$(YQ_VERSION)/yq_linux_amd64
	chmod 755 $(PFX)/yq

clean:
	rm -rf $(PFX)

bin:
	mkdir $(PFX)
