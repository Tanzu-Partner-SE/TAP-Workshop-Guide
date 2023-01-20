###### Delete the accelerator 

```execute
tanzu accelerator delete {{ session_namespace }}
```

###### List the workloads

```execute
tanzu apps workload list -n tap-install
```

###### Delete the workload {{ session_namespace }}

```execute
tanzu apps workload delete {{ session_namespace }} -n tap-install -y
```

###### Delete the workload {{ session_namespace }}-a

```execute
tanzu apps workload delete {{ session_namespace }}-a -n tap-install -y
```

###### List the workloads

```execute
tanzu apps workload list -n tap-install
```
