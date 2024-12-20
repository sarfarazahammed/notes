# kubectl

- Command line tool for communicating with a cluster's control plane using kubernetes API

## Installation on mac

1. Run installation command
`brew install kubectl`

2. Ensure the version installed
`kubectl version --client`

## Syntax

`kubectl [command] [TYPE] [NAME] [flags]`

`command`: specifies the operation that you wnat to perform on one or more resources, for eg: `create`, `get`, `describe`, `delete`

`TYPE`: specifies the resource type. value is case insensitive

`NAME`: specifies the name of the resource. value is case sensitive

`flags`: specifies optional flags

## Important Commands

[kubectl commands reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)

- `kubectl api-resources` : lisst resources in kubernetes along with their api-version and kind
- `kubectl api-versions` : lists supported API versions on the server, in the form of "group/version"
- `kubectl cluster-info` : display address of control plane & cluster services
- Context & config commands: context is to access multiple kuberenetes clusters
    | Command | Description |
    | --- | --- |
    | `kubectl config current-context` | Display the current context |
    | `kubectl config get-contexts` | Display a list of available contexts |
    | `kubectl config set-context --current --namespace=<namespace>` | Set the namespace for the current context |
    | `kubectl config set-context <context-name> --namespace=<namespace>` | Set the namespace for a specific context |
    | `kubectl config use-context <context-name>` | Switch to a different context |
    | `kubectl config delete-context <context-name>` | Delete a context |
    | `kubectl config rename-context <old-context-name> <new-context-name>` | Rename a context |
    | `kubectl config view` | Display detailed information about the current context |
    | `kubectl config get-clusters` | Display a list of available clusters |
    | `kubectl config get-users` | Display a list of available users |
    | `kubectl config view --minify` | Display the current configuration in a minified format |
    | `kubectl config view --flatten` | Display the current configuration in a flattened format |
    | `kubectl config view --raw` | Display the current configuration in a raw format |
