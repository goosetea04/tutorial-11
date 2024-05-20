# tutorial-11

## Reflection on Hello-Kube

1.  Compare the application logs before and after you exposed it as a Service.Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

### Before exposure
![image](https://github.com/goosetea04/tutorial-11/assets/126388982/3cf44a32-ce2d-4fb3-8fe7-1f2f6550ce99)

### After Exposure
![image](https://github.com/goosetea04/tutorial-11/assets/126388982/1e14c077-7fc2-409f-b1a5-e46e7739a215)

Before exposure we see that it just contains the logs regarding starting the server and the subsequent UDP server on the mentioned ports. There is nothing more to add here. What is different is that after exposure, for each subsequent acces, there are two GET/ logs added. This is because of the HTTP and UDP counting as twice for each access.

2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

The `-n` option in Kubernetes stands for `--namespace`. Namespaces isolate groups of resources within a cluster. Resource names must be unique within a namespace but not across namespaces. The `-n` option allows specifying the namespace for an operation. If no namespace is specified, the `default` namespace is used. This is why your explicitly created pods or services were not listed initially - they were likely in a different namespace than `default`. To list resources from other namespaces, use the `-n` option with the desired namespace name.

## Reflection Part 2

1. What is the difference between Rolling Update and Recreate deployment strategy?

Rolling Update: Gradual updates, no downtime (maintains old versions during update).
Recreate: Faster, less resource usage (terminates old versions), but service has downtime.

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt. and Prepare different manifest files for executing Recreate deployment strategy.

While the Recreate strategy offered faster updates with lower resource consumption by terminating old versions, it also means that there will be service downtime. To implement this, I simply modified the deployment.yaml file, swapping the strategy from RollingUpdate to Recreate. For the deployment itself, I opted for a clean approach. I deleted the existing minikube cluster, set up a fresh one, and then applied both the modified deployment.yaml and the previously created service.yaml files.

3. What do you think are the benefits of using Kubernetes manifest files?

Using manifest files enhances the efficiency, scalability, and maintainability of project deployments. They streamline the process by allowing a single `kubectl apply -f` command to deploy and expose services with all necessary options, saving time compared to manually writing commands. Manifest files also maintain consistency in settings, reducing the risk of incorrect configurations that can be hard to identify and fix.

Moreover, manifest files promote scalability by serving as clear documentation of deployment settings and being easily adjustable. This clarity and ease of configuration simplify the deployment process and reduce the likelihood of errors, making it a more efficient and reliable method compared to manually inputting commands.

Group Project Deployment: https://frightened-manya-zeus-adpro-d40b7de3.koyeb.app/listings/
