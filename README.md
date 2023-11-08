# AKS-blog
## STEPS
1.  Create RG and AKS from Azure portal 
    ### Dev/test, myk8 name, node B2s, another node pool-super worker, manuel scale…

2. Create My_Blog folder and inside this folder user_service and post_service
3. First go with user_service folder; open it with vsCode and then follow below steps...
    create app.py python file
    from command palette create virtual env.for python 3.11
    use updated requirements.txt file
    test the app.py file (you should see from web page)
    containerize  your app.py file. to do this use command palette with docker
    push your docker image to GitHub and Docker Hub

4. Follow the same steps with post_service folder.
5. From My_Blog folder on vsCode create blog_deployment.yaml file
6. Connect to your AKS cluster from CLI and test followings...
    from Azure cluster do it merge and from kubernetes extention do it current cluster your aks and ...
    kubectl get nodes
    kubectl get pods
    kubectl apply -f blob_deployment.yaml
    kubectl get svc
    kubectl port-forward svc/user-service 5000:5000
    kubectl port-forward svc/post-service 5001:5001

7. After uncommenting (load balancer part of the yaml file (89---101 lines))
    k apply -f blog_deployment.yaml
    you'll see public IP (test with it)

8. After uncommenting (test of autoscaling part (124---135))
    k apply -f blog_deployment.yaml
    kubectl get hpa

9. Replica test
    k scale deployment user-service-deployment --replicas=4
    k scale deployment post-service-deployment --replicas=4
    k get pods (you should see 8 pods)

    k scale deployment user-service-deployment --replicas=0
    k scale deployment post-service-deployment --replicas=0
    k get pods (you should see 0 pods)

10. Delete the deployment
    kubectl delete -f blog_deployment.yaml

    # THANK YOU !!!