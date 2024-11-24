# gcp-infra

This is the terraform code for the gcp infrastructure.

## Preparations

1. Allow direnv to load `.envrc`

2. Install `terraformer`
   - Reference Issue
     - Apple Silicon : <https://github.com/GoogleCloudPlatform/terraformer/issues/1925>
     - plugin error : <https://github.com/GoogleCloudPlatform/terraformer/issues/590>

3. Set environment variables

    ```bash
    source .envrc
    ```

4. Enable `compute.googleapis.com` API (Need to set up a billing account for your GCP project through Google Cloud Console)

    ```bash
    # It takes a few minutes to enable
    gcloud services enable compute.googleapis.com --project=$GCP_PROJECT_ID
    gcloud services list --enabled --project=$GCP_PROJECT_ID | grep compute.googleapis.com
    ```

    <!-- https://console.developers.google.com/apis/api/compute.googleapis.com/overview?project=test-jaesoon 에서도 활성화 가능 -->
    or Visit Google Cloud Console and enable `compute.googleapis.com` API ([link](https://console.cloud.google.com/apis/api/compute.googleapis.com/overview?project=$GCP_PROJECT_ID))

## Usage

1. Check `GOOGLE_APPLICATION_CREDENTIALS` info (ref: [application-default-credentials](https://cloud.google.com/docs/authentication/application-default-credentials))

    ```bash
    # macOS: $HOME/.config/gcloud/application_default_credentials.json
    export GOOGLE_APPLICATION_CREDENTIALS=/path/to/your/gcp-credentials.json
    ```

2. Import existing resources

    - All resources

      ```bash
      terraformer import google --resources=all --projects=$GCP_PROJECT_ID --regions=$GCP_REGION
      ```

    - Specific resources

      ```bash
      terraformer import google --resources=storage,compute --projects=$GCP_PROJECT_ID --regions=$GCP_REGION
      ```
