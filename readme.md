HOW TO CREATE ARGOCD APPLICATION USING CLI
================================

#create a namespace:
====================

kubectl create ns dev

TO GET THE ARGOCD PASSWORD:
===========================

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

argocd app logs <IP>

argocd app create my-jojo \
  --repo https://github.com/joehaddy07/GitOps-Joe.git \
  --path . \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace dev \
  --sync-policy automated



#Verify if the Application is created:
======================================

argocd app get my-jojo

#sync the application

argocd app sync my-jojo

#Run the following to inspect:
==============================

argocd app get my-jojo

kubectl get all -n dev

#Disable auto-sync for the application:
=======================================

argocd app set my-jojo --sync-policy none


# rollback. Put the number you will like to rollback :
======================================================

argocd app rollback my-jojo 3

#Re-enable auto-sync if necessary:
==================================

argocd app set my-jojo --sync-policy automated