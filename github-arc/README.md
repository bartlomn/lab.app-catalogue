# github-arc

## Deployment

The deployment here needs to be staged, because we need to deal with secret for github auth

### Create github app

Get all the details needed to create the secret

[actions-runner-controller/authenticating-to-the-github-api.md at master · actions/actions-runner-controller](https://github.com/actions/actions-runner-controller/blob/master/docs/authenticating-to-the-github-api.md#deploying-using-github-app-authentication)

- create the app in ArgoCD, don’t sync the whole thing
- sync only the namespace
- create the secret, like so

```jsx
kubectl create secret generic ${SECRET_NAME} \
    -n ${NAMESPACE} \
    --from-literal=github_app_id=${APP_ID} \
    --from-literal=github_app_installation_id=${INSTALLATION_ID} \
    --from-file=github_app_private_key=${PRIVATE_KEY_FILE_PATH}
```

- sync CRDS, use replace feature
- sync the rest of the app APART FROM the deployment
- sync the deployment
