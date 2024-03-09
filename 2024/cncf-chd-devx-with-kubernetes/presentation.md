footer: @RinkiyaKeDad
slide-transition: true
build-lists: true

# [fit] Improving the
# [fit] **Development Experience**
# [fit] with Kubernetes

Arsh Sharma, Okteto

---

# What is Development Experince?
* DevX refers to the overall experience that developers have while working with a particular set of tools, technologies, frameworks, or platforms. 

---

# Current Cloud Native DevX

![inline original 65%](/Users/arsh/code/slide-decks/2023/dec-platform-engineering-blr/todolistapp.png)

---

# Current Cloud Native DevX

* microservices code
* databases
* cloud services
* devops tools like terraform, helm, etc

![right fit 45%](/Users/arsh/code/slide-decks/2023/dec-platform-engineering-blr/todolistapp.png)

---

# What can we do to improve it?

> The solution to the problem lies in the problem itself
-- Some Philosopher

---

## Why Kubernetes for Dev Platforms?

* Containerized Environment
* Consistency Across Environments
* Service Discovery
* Scalability and Resource Efficiency
* Ecosystem and Extensibility

---

## Okteto CLI

* [github.com/okteto/okteto](https://github.com/okteto/okteto)
* **Platform Engineers**: Define dev environments which will run on K8s
* **Developers**: One click deploy and develop applications directly in the cluster (`okteto up`)

---

## [fit] **Demo!**

---

## **Try it out!**

![inline original 40%](todoappindefaultns.png)

---

## Build Section

![left orginial 120%](/Users/arsh/code/slide-decks/2023/cncf-thane-leveraging-kubernetes-as-the-foundation-for-your-development-environments/folder-structure.png)
    
```yaml
build:
  server:
    context: server
  client:
    context: client
```

---

## Deploy Section

![left orginial 120%](/Users/arsh/code/slide-decks/2023/cncf-thane-leveraging-kubernetes-as-the-foundation-for-your-development-environments/folder-structure.png)

```yaml
deploy:
  image: hashicorp/terraform:1.4

  commands:
  - name: Create the AWS S3 Bucket
    command: |
        terraform init -input=false
        terraform apply -input=false -auto-approve

  - name: Create the AWS secret
    command: |
        kubectl apply -f aws-secret.yaml
```

---

## Deploy Section

![left orginial 120%](/Users/arsh/code/slide-decks/2023/cncf-thane-leveraging-kubernetes-as-the-foundation-for-your-development-environments/folder-structure.png)

```yaml
deploy:
    ...
  - name: Deploy the DB
    command: helm upgrade --install db db/chart

  - name: Deploy the Node.js Backend
    command: helm upgrade --install server server/chart \
             --set image=${OKTETO_BUILD_SERVER_IMAGE} \
             --set bucket="$S3_BUCKET_NAME"

  - name: Deploy the React Frontend
    command: helm upgrade --install client client/chart \
             --set image=${OKTETO_BUILD_CLIENT_IMAGE}
```
---

## Develop Section

![left orginial 120%](/Users/arsh/code/slide-decks/2023/cncf-thane-leveraging-kubernetes-as-the-foundation-for-your-development-environments/folder-structure.png)

```yaml
dev:
  server:
    command: bash
    sync:
      - server:/app
  client:
    command: npm start
    sync:
      - client:/app
```

---

# [fit] **Thanks**
# [fit] **for attending!**
Try Okteto for free at: [okteto.com](https://okteto.com)
For questions, reach out to me on Twitter: @RinkiyaKeDad

---

## **Learn Platform Engineering Best Practices!**

![inline original 110%](newsletter.png)

https://bit.ly/43a3vcA
