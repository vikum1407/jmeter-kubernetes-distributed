Installations and Run:
    1. Install Helm 
    2. Go charts
    3. Change domain name(hostAliases) and IP address on 'jmeter-slave-deployment.yaml' file 
    4. Add following prometheus scrape_configs for gafana data fetch
                scrape_configs:
                        - job_name: 'jmeter'
                        metrics_path: '/metrics'
                        scrape_interval: 2s
                        scheme: 'http'
                        static_configs:
                        - targets: ['jmeter-slave.default.svc:60001']
    4. Execute 'helm install jmeter jmeter' command
    5. Create your jmeter script using jmeter-5.4 version and copy into the script folder
    6. Copy jmeter script file to master pod using following command
            - kubectl cp <HOME>/scripts/JMeter-Script.jmx $(kubectl get pod -l "app=jmeter-master" -o jsonpath='{.items[0].metadata.name}'):/scripts/
    7. Execute the jmeter script using following command
            - kubectl exec  -it $(kubectl get pod -l "app=jmeter-master" -o jsonpath='{.items[0].metadata.name}') -- sh -c 'ONE_SHOT=true; /jmeter-script.sh'

References :-

Helm installation:  https://www.cyberithub.com/steps-to-install-helm-kubernetes-package-manager-on-linux/