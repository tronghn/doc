# Cloud Storage Buckets

{% hint style="danger" %}
Cloud Storage buckets is in ALPHA and MUST NOT be used in production environments.
{% endhint %}

You can request a Google Cloud Storage bucket through the NAIS manifest. This feature is only available in GCP clusters.

Bucket names must be globally unique across the entire Google infrastructure.

``` yaml
apiVersion: "nais.io/v1alpha1"
kind: "Application"
metadata:
  name: app-a
...
spec:
  ...
  gcp:
    buckets:
      - name: my-very-stable-and-fast-bucket
```

Once a bucket is provisioned, it *will not* be automatically deleted. This means that any cleanup must be done manually:

```bash
kubectl delete storagebucket my-very-stable-and-fast-bucket
kubectl delete storagebucketaccesscontrol my-very-stable-and-fast-bucket
```

If having problems getting your bucket up and running, the name might be taken already. Check errors in the event log:

```bash
kubectl describe storagebucket my-very-stable-and-fast-bucket
```
