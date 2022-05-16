# Install ECK(NG)

1. `kubectl create -f https://download.elastic.co/downloads/eck/2.2.0/crds.yaml`
2. `kubectl apply -f https://download.elastic.co/downloads/eck/2.2.0/operator.yaml`
3. `kubectl apply -f elasticsearch.yaml`
4. `kubectl apply -f kibana.yaml`
5. `kubectl apply -f apm-server.yaml`
6. get kibana login password `kubectl get secret -n elastic-system quickstart-es-elastic-user -o=jsonpath='{.data.elastic}' | base64 --decode; echo`
7. get apm token `kubectl get secret/apm-server-quickstart-apm-token -o go-template='{{index .data "secret-token" | base64decode}}'`

# Install Fleet Example(OK)

[https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-elastic-agent-fleet-configuration-examples.html](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-elastic-agent-fleet-configuration-examples.html)

# Java Elastic APM Demo
[https://github.com/elastic/opbeans-java](https://github.com/elastic/opbeans-java)
```
java -javaagent:./elastic-apm-agent-1.30.1.jar \                                                                   ✔  took 15s   at 00:55:32 
-Delastic.apm.service_name=opbeans-java \
-Delastic.apm.server_urls=http://localhost:8200 \
-Delastic.apm.secret_token= \
-Delastic.apm.environment=production \
-Delastic.apm.application_packages=co.elastic.apm.opbeans -jar \
./target/opbeans-0.0.1-SNAPSHOT.jar
```

# Install ArgoCD

1. `kubectl create namespace argocd`
2. `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
3. get admin login password `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`
4. `kubectl port-forward -n argocd service/argocd-server 10443:443`
