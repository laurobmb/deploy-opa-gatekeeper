# Gatekeeper

## Add labels 
source check-ignore-label.gatekeeper.sh

## Install 
oc apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml

oc apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/release-3.8/deploy/gatekeeper.yaml


## Remove securityContext and annotations from the deployments

    oc patch Deployment/gatekeeper-audit --type json -p='[{"op": "remove", "path": "/spec/template/metadata/annotations"}]' -n gatekeeper-system
    oc patch Deployment/gatekeeper-controller-manager --type json -p='[{"op": "remove", "path": "/spec/template/metadata/annotations"}]' -n gatekeeper-system
    oc patch Deployment/gatekeeper-audit --type json --patch '[{ "op": "remove", "path": "/spec/template/spec/containers/0/securityContext" }]' -n gatekeeper-system
    oc patch Deployment/gatekeeper-controller-manager --type json --patch '[{ "op": "remove", "path": "/spec/template/spec/containers/0/securityContext" }]' -n gatekeeper-system

## Active
oc apply -f gatekeeper-config.yml

oc apply -f gatekeeper-constraintTamplate-k8sallowedroutes.yml
oc apply -f gatekeeper-k8sallowroutes.yml
oc apply -f gatekeeper-constraintTamplate-k8suniueroutehost.yml
oc apply -f gatekeeper-k8suniueroutehost.yml

# Reference
https://github.com/gatekeeper/gatekeeper-operator
https://access.redhat.com/articles/6067691
https://access.redhat.com/solutions/6758941
https://access.redhat.com/articles/6047221
https://vikaspogu.dev/posts/opa-gatekeeper-openshift/

## UNInstall 
oc delete -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml
