# Kubectl + awscli + skaffold + docker env

This docker container is used to create a full environment for running skaffold and deploying to your EKS installation.

It installs `openrc` `kubectl` `docker` `skaffold` `awscli` on top of an alpine image.

### Using this Action

Create your `KUBE_CONFIG` secret to connect to your EKS cluster by running:

    cat ~/.kube/config | base64

Then use the action like so (you will need to pass in the awscli env vars to the action, as it needs to login to ECR and both kubectl and skaffold invoke awscli):

```
- name: Skaffold.dev utility for EKS
  uses: tarrynn/skaffold-action@1.3
  env:
    KUBE_CONFIG: ${{ secrets.KUBE_CONFIG }}
    AWS_REGION: ${{ secrets.AWS_REGION }}
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_KEY }}
    AWS_ACCOUNT_ID: ${{ secrets.AWS_ACCOUNT_ID }}
```
