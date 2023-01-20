##### Supply Chain Security Tools for Tanzu – Store

Supply Chain Security Tools - Store saves software bills of materials (SBoMs) to a database and allows you to query for image, source code, package, and vulnerability relationships. It integrates with Supply Chain Security Tools - Scan to automatically store the resulting source code and image vulnerability reports. 

###### Tanzu Insight CLI plug-in

The Tanzu Insight CLI plug-in is the primary way to view results from the Supply Chain Security Tools - Scan of source code and image files. Use it to query by source code commit, image digest, and CVE identifier to understand security risks.

```dashboard:open-url
url: https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.3/tap/GUID-scst-store-install-scst-store.html
```

###### Supported use cases: 

The following are a few use cases supported by the CLI:

 - What packages and CVEs exist in a particular image? (image)
 
 - What packages and CVEs exist in my source code? (source)

 - What dependencies are affected by a specific CVE? (vulnerabilities)


When using an Ingress setup, the Store creates a specific TLS Certificate for HTTPS communications under the metadata-store namespace.

###### To get a certificate, run:

```execute  
kubectl get secret ingress-cert -n metadata-store -o json | jq -r '.data."ca.crt"' | base64 -d > insight-ca-new.crt
```

###### Set the target by running:

```execute  
tanzu insight config set-target https://metadata-store.tanzupartnerdemo.com --ca-cert insight-ca-new.crt
```

###### Add an image report

Note: For this workshop, we have already included image-cve-report as part of the image. 
  
```execute  
tanzu insight image add --cyclonedxtype xml --path image-cve-report
```

###### List the dependencies that are affected by a specific CVE: 

```execute  
tanzu insight vuln get --cveid CVE-2020-16156
```

###### List the image that are affected by a specific CVE:

```execute  
tanzu insight vuln images --cveid CVE-2020-16156
```

###### List the image and CVE details of a specific package: 

```execute  
tanzu insight package images --name perl-base
```

###### List the packages and images that a specific image contain: 

```execute  
tanzu insight image get --digest sha256:ab699d1caf2f36d55170f5570c30e28164039873384523a2ffc8b8cb3631ce3e
```
