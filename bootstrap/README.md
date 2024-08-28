## Install Bootstrap Application for GitOps Automation

To enabled the GitOps automation you must create the required resources in the target cluster.

Before applying the manifests, there is a need to replace the `__REPLACE_SSH_PRIVATE_KEY__` string in onboarding999999-argocd-repo.yaml with the SSH key to enable access to the Git repository.

Either manually edit the file or login to the target cluster and run the following command:

```
git clone https://github.com/orchestrator-test/onboarding999999-gitops.git
cd onboarding999999-gitops/bootstrap

# Optionally, if edited the file manually
SSH_PRIVATE_KEY=$(oc get secrets -n orchestrator-gitops git-ssh-credentials -o jsonpath='{.data.id_rsa}')
sed -i "s/__REPLACE_SSH_PRIVATE_KEY__/$SSH_PRIVATE_KEY/" onboarding999999-argocd-repo.yaml

kubectl apply -f .
```

**Note:** If you're not logged into the repository, you need to provide a personal access token (PAT) as part of the clone URL.

```
git clone https://<PAT>@github.com/orchestrator-test/onboarding999999-gitops.git
```

Replace `<PAT>` with your personal access token. Ensure the token has the necessary permissions to access the repository.

If you encounter issues with the clone, refer to [GitHub's troubleshooting documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) for assistance.
