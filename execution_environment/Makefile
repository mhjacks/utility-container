OPENSHIFT_CLIENT_VERSION=4.10.3
YQ_VERSION=v4.25.3
PFX=context/bin

ee: download
	ansible-builder build --tag=hybridcloudpatterns-utility-ee

download: clean bin oc argocd helm azuretrim

argocd:
	curl -sSL -o $(PFX)/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
	chmod 755 $(PFX)/argocd

helm:
	curl -sSL -o $(PFX)/helm https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/helm/latest/helm-linux-amd64
	chmod 755 $(PFX)/helm

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

yq:
	curl -sSL -o $(PFX)/yq  https://github.com/mikefarah/yq/releases/download/$(YQ_VERSION)/yq_linux_amd64
	chmod 755 $(PFX)/yq

clean:
	rm -rf $(PFX)

bin:
	mkdir $(PFX)
