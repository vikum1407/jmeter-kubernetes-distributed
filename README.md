
# JMeter Distributed setup on kubernetes, HelmChart with Grafana and Prometheus

Install JMeter Distributed environment easly with the helm chart on Kubernetes setup to trigger different types of performance tests on your product.

* Install HelmChart
* Clone the git repo from master branch
* Go to 'chart' folder


## Product domain initialization

* Change domain name(hostAliases) and IP address on 'jmeter-slave-deployment.yaml' file

```bash
    spec:
      hostAliases:
        - ip: 19x.x2.23.xx
          hostnames:
            - apigateway.bom.vk.com

```
        
## Prometheus Scrape Config

Add Prometheus Scrape config as follows

```bash
scrape_configs:
    - job_name: 'jmeter'
      metrics_path: '/metrics'
      scrape_interval: 2s
      scheme: 'http'
      static_configs:
    - targets: ['jmeter-slave.default.svc:60001']
```
## Start Jmeter Helmchart

Execute following command from 'chart' folder

```bash
helm install jmeter jmeter
```

* Create your jmeter script using jmeter-5.4 version and copy into the script folder
* Copy jmeter script file to master pod using following command

```bash
kubectl cp <HOME>/scripts/JMeter-Script.jmx $(kubectl get pod -l "app=jmeter-master" -o jsonpath='{.items[0].metadata.name}'):/scripts/
```
* Execute the jmeter script using following command

```bash
kubectl exec  -it $(kubectl get pod -l "app=jmeter-master" -o jsonpath='{.items[0].metadata.name}') -- sh -c 'ONE_SHOT=true; /jmeter-script.sh'

```


![Logo](https://github.com/vikum1407/jmeter-kubernetes-distributed/blob/master/Jmeter_DistributedSetup_K8.PNG?raw=true)

