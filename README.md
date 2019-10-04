# Run Kafka on Kubernetes
- Install Docker for Ubuntu 16.x

    docker-install.sh

- Zookeeper on Kubernetes
    ```
    $ kubectl create -f zookeeper.yml
    ```

- Create a Kafka Service
    ```
    $ kubectl create -f kafka-service
    ```

- Check Ingress (internal IP)
    ```
    $ kubectl describe svc kafka-service
    Name: kafka-service
    Namespace: default
    Labels: name=kafka
    Annotations: kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"name":"kafka"},"name":"kafka-service","namespace":"default"},"spec":{"ports...
    Selector: app=kafka,id=0
    Type: LoadBalancer
    IP: 10.105.148.62
    LoadBalancer Ingress: 192.168.1.240
    Port: kafka-port 9092/TCP
    TargetPort: 9092/TCP
    NodePort: kafka-port 30718/TCP
    Endpoints: 10.44.0.4:9092
    Session Affinity: None
    External Traffic Policy: Cluster
    Events: <none>
    ```

    Replace IP in kafka-broker.yml config and create resource

    ```
    $ create -f kafka-broker.yml
    ```

    Check it's running

    ```
    $ kubectl get pod kafka-broker0
    ```

- Check with KafkaCat

    ```
    $ apt-get install kafkacat
    ```

    ```
    $ kafkacat -b 192.168.1.240:9092 -t admintome-test
    ```

    ```
    $ cat README.md | kafkacat -b 192.168.1.240 -t admintome-test
    ```
