## How To Removed A "Terminating" Namespace

See YouTube Video Demo: https://youtu.be/ebxbJcyMD-o

If you know you have removed everything and still cannot seem to get the project/namespace to delete, you can force it with these procedures. 
Please note, it's not recommended in production. I you have a situation like this, please contact Red Hat Support.

1. `oc get ns $NAMESPACE -o yaml > $FILENAME.yaml`
2. `vi $FILENAME.yaml` \
    Remove the line "- kubernetes"
3. `oc proxy &`
4. `curl -k -H "Content-Type: application/yaml" -X PUT --data-binary @$FILENAME.yaml http://127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize`
5. `oc get ns $NAMESPACE`

The namespace should now be forceably removed.
