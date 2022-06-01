# GCP

[TOC]
# Getting Started
Ref: https://cloud.google.com/dataflow/docs/quickstarts/quickstart-python

In the Google Cloud Console, on the project selector page, select or create a Google Cloud project.
Note: If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

Go to project selector

Make sure that billing is enabled for your Cloud project. Learn how to check if billing is enabled on a project.
Enable the Dataflow, Compute Engine, Cloud Logging, Cloud Storage, Google Cloud Storage JSON, BigQuery, Cloud Pub/Sub, Cloud Datastore, and Cloud Resource Manager APIs.

Enable the APIs

Create a service account:

    In the Cloud Console, go to the Create service account page.
    Go to Create service account
    Select your project.

    In the Service account name field, enter a name. The Cloud Console fills in the Service account ID field based on this name.

    In the Service account description field, enter a description. For example, Service account for quickstart.
    Click Create and continue.

    To provide access to your project, grant the following role(s) to your service account: Project > Owner .

    Click the Select a role field, then select the first (or only) role.

    For additional roles, click Add another role and add each additional role.
    Note: The Role field affects which resources your service account can access in your project. You can revoke these roles or grant additional roles later. In production environments, do not grant the Owner, Editor, or Viewer roles. Instead, grant a predefined role or custom role that meets your needs.
    Click Continue.

    Click Done to finish creating the service account.

    Do not close your browser window. You will use it in the next step.

Create a service account key:

    In the Cloud Console, click the email address for the service account that you created.
    Click Keys.
    Click Add key, then click Create new key.
    Click Create. A JSON key file is downloaded to your computer.
    Click Close.

Set the environment variable GOOGLE_APPLICATION_CREDENTIALS to the path of the JSON file that contains your service account key. This variable only applies to your current shell session, so if you open a new session, set the variable again.

Example: Linux or macOS

export GOOGLE_APPLICATION_CREDENTIALS="KEY_PATH

"

Replace KEY_PATH with the path of the JSON file that contains your service account key.

For example:

export GOOGLE_APPLICATION_CREDENTIALS="/home/user/Downloads/service-account-file.json"

Example: Windows

For PowerShell:

$env:GOOGLE_APPLICATION_CREDENTIALS="KEY_PATH

"

Replace KEY_PATH with the path of the JSON file that contains your service account key.

For example:

$env:GOOGLE_APPLICATION_CREDENTIALS="C:\Users\username\Downloads\service-account-file.json"

For command prompt:

set GOOGLE_APPLICATION_CREDENTIALS=KEY_PATH

Replace KEY_PATH with the path of the JSON file that contains your service account key.
Create a Cloud Storage bucket:

    In the Cloud Console, go to the Cloud Storage Browser page.

    Go to Browser
    Click Create bucket.
    On the Create a bucket page, enter your bucket information. To go to the next step, click Continue.
        For Name your bucket, enter a unique bucket name. Don't include sensitive information in the bucket name, because the bucket namespace is global and publicly visible.
        For Choose where to store your data, do the following:
            Select a Location type option.
            Select a Location option.
        For Choose a default storage class for your data, select the following: Standard.
        For Choose how to control access to objects, select an Access control option.
        For Advanced settings (optional), specify an encryption method, a retention policy, or bucket labels.
    Click Create.

Copy the Google Cloud project ID and the Cloud Storage bucket name. You need these values later in this document.

# Logging

## Structured Logging
https://cloud.google.com/logging/docs/structured-logging

# [BigQuery](/Engineering/Software-Engineering/Database/gcp_bigquery/)

# [Dataflow](/Engineering/Software-Engineering/Data-Engineering/gcp_dataflow/)

# Storage

## Cost

https://cloud.google.com/storage/pricing#storage-pricing

# GCP Cost

## Estimate
- https://cloud.google.com/products/calculator
