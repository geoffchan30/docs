1. Verify that you are in the correct Kubernetes context. You want to install the RNA in the cluster where you deploy your apps.

1. Add the Armory Helm repo:

   ```bash
   helm repo add armory https://armory.jfrog.io/artifactory/charts
   ```

   You only need to do this once.

1. Refresh the repo cache:

   ```bash
   helm repo update
   ```

1. Create the namespace where the RNA is installed:

   ```bash
   kubectl create ns armory-rna
   ```

1. Create secrets from your Client ID and Client Secret:

   ```bash
   kubectl --namespace armory-rna create secret generic rna-client-credentials --type=string --from-literal=client-secret=<your-client-secret> --from-literal=client-id=<your-client-id>
   ```

   The examples use Kubernetes secrets to encrypt the value. You supply the encrypted values in the Helm command to install the RNA.

1. Install the Helm chart.

    For most scenarios, you install one RNA per cluster. Use the `agentIdentifier` parameter to give each RNA a unique name. When you deploy your app, you specify which RNA to use, so Armory recommends creating a name that identifies the cluster.

    ```bash
    helm upgrade --install armory-rna armory/remote-network-agent \
        --set agentIdentifier=<rna-name> \
        --set 'clientId=encrypted:k8s!n:rna-client-credentials!k:client-id' \
        --set 'clientSecret=encrypted:k8s!n:rna-client-credentials!k:client-secret' \
        --namespace armory-rna
    ```

    The encrypted values for `clientId` and `clientSecret` reference the Kubernetes secrets you generated in an earlier step.

   For advanced use cases such as proxy configurations, custom annotations, labels, or environment variables, see the [`values.yaml` for the RNA](https://github.com/armory-io/remote-network-agent-helm-chart/blob/master/values.yaml?rgh-link-date=2022-02-02T22%3A38%3A35Z). For information about using a `values file`, see the [Helm documentation](https://helm.sh/docs/chart_template_guide/values_files/).

1. Verify the RNA connection. Go to the [Agents page](https://console.cloud.armory.io/configuration/agents) in the Configuration UI, and look for the Agent identifier you assigned to your target deployment cluster. You should see it along with some basic information:

   > Note that you may see a "No Data message" when first loading the Agent page.

   {{< figure src="/images/cdaas/ui-rna-status.jpg" alt="The Connected Remote Network Agents page shows connected agents and the following information: Agent Identifier, Agent Version, Connection Time when the connection was established, Last Heartbeat time, Client ID, and IP Address." >}}



   If you do not see the RNA for your target deployment cluster, check the logs for the target deployment cluster to see if the RNA is up and running.

