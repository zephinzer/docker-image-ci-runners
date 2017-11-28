# Google Container Engine (GKE) Deployer

An image that is intended for use in Continuous Integration/Delivery (CI/CD) pipelines where a deployment to Google Container Engine (GKE) is required. 

This image includes:

- GCloud SDK (latest)
- Kubectl (bundled with GCloud SDK)
- Git
- Docker

Exact versions can be viewed from the Docker Hub tags page: https://hub.docker.com/r/zephinzer/gke-deployer/tags/.

## Usage

Use this image to run your job in your pipelines. The image does not define any settings so you'll need to configure them yourself.

```yaml
image: zephinzer/gke-deployer:177.0.0
# or if gcloud sdk version doesn't matter:
image: zephinzer/gke-deployer:latest
```

The full list of tags can be found at: https://hub.docker.com/r/zephinzer/gke-deployer/tags/.

### API Keys
You will need to download your GCloud API keys.

#### Generate your keys
Go to your Cloud Console and navigate to **APIs & Services** > **Credentials**.

Click on the **Create credentials** button and select **Service account key**.

In the following page, select **Compute Engine default service account** from the Service account dropdown menu, and set the **Key type** to **JSON**. Click on **Create** and download your keys.

#### Obscure your keys
Do a base64 encoding of your keyfile by running the following command:

```bash
$ base64 /path/to/your/keyfile.json
```

Copy the output and set it as an environment variable in your CI pipeline. For the example below, it assumes you've set the environment variable `GCAPIKEY_JSON` to the base64 encoded keyfile.

#### Configure the image
Before being able to use the `gcloud` command to deploy your application, you'll need to configure it to know who you are. Add the following to your job's script prior to deploying:

```bash
echo "${GCAPIKEY_JSON}" | base64 -d > ./gcapikey.json \
  && gcloud auth activate-service-account --key-file ./gcapikey.json \
  && gcloud config set project ${GCP_PROJECT_ID} \
  && gcloud config set compute/region ${GCP_PROJECT_REGION} \
  && gcloud config set compute/zone ${GCP_PROJECT_ZONE} \
  && gcloud container clusters get-credentials ${GCP_GKE_CLUSTER_NAME} \
  && rm -rf ./gcapikey.json;
```

Where:

- `${GCP_PROJECT_ID}` is the ID of your project in Google Cloud,
- `${GCP_PROJECT_REGION}` is the region you wish to deploy to,
- `${GCP_PROJECT_ZONE}` is the zone you wish to deploy to,
- `${GCP_GKE_CLUSTER_NAME}` is the cluster you are deploying to

#### Deploy your stuff
After configuring `gcloud`, you should be able to use `kubectl` to deploy your specfiles:

```bash
$ kubectl apply -f /path/to/your/specfile.yaml
```