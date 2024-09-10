### Kubernetes Management Techniques
* These commands use helper templates called `generators`
* Every resource in Kubernetes has a specification or "spec"
* `$ kubectl create deployment sample --image nginx --dry-run=client -o yaml`
* You can output those templates with `--dry-run=client -o yaml`