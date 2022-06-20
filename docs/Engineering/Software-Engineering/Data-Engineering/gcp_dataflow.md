# GCP Dataflow

<h3>Table of Contents</h3>

[TOC]

# Introduction
- https://cloud.google.com/dataflow

## What

## Why

## How
- https://www.ververica.com/blog/announcing-google-cloud-dataflow-on-flink-and-easy-flink-deployment-on-google-cloud
- https://research.google/pubs/pub41378/
    - https://storage.googleapis.com/pub-tools-public-publication-data/pdf/41378.pdf
- (paper:how apache beam works) https://pages.cs.wisc.edu/~akella/CS838/F12/838-CloudPapers/FlumeJava.pdf
- https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43864.pdf
- https://www.youtube.com/watch?v=3BrcmUqWNm0
- https://www.youtube.com/watch?v=a7CymWiX3oM&t=399s
- https://cloud.google.com/dataflow/docs/concepts
- https://cloud.google.com/dataflow/docs/concepts/dataflow-templates
- https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline#parallelization-and-distribution
- https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline
- https://cloud.google.com/dataflow/docs/concepts/execution-details
- https://cloud.google.com/dataflow/docs/resources/faq
    - https://cloud.google.com/dataflow/docs/resources/faq#how_many_instances_of_dofn_should_i_expect_dataflow_to_spin_up_

# Classic Template

## Why Template

Templates provide you with additional benefits compared to non-templated Dataflow deployment, such as:

- You can run your pipelines without the development environment and associated dependencies that are common with non-templated deployment. This is useful for scheduling recurring batch jobs.
- Templates separate the pipeline construction (performed by developers) from the running of the pipeline. Hence, there's no need to recompile the code every time the pipeline is run.
- Runtime parameters allow you to customize the running of the pipeline.
- Non-technical users can run templates with the Google Cloud Console, Google Cloud CLI, or the REST API.
- You can extend templates with user-defined functions.

## What

## How

## Create

Covert the Apache Beam pipeline into a Dataflow classic template.

Ref: https://cloud.google.com/dataflow/docs/guides/templates/creating-templates

## Stage

Stage the classic template in cloud storage using the following command:

```bash
$ python -m exploratory.wordcount_with_option_and_value_provider_v2 \
    --region us-central1 \                                                                      # cloud region
    --runner DataflowRunner \                                                                   # beam runner engine
    --job_name wordcount-custom-job-$(date +%Y%m%d-%H%M%S) \                                    # dataflow job name
    --project $GCP_PROJECT \                                                # cloud project
    --temp_location gs://$GCP_PROJECT-dataflow-poc/tmp/ \                   # gcs path
    --staging_location gs://$GCP_PROJECT-dataflow-poc/staging \             # gcs path for staging files
    --template_location gs://$GCP_PROJECT-dataflow-poc/templates/wordcount  # gcs path to store template file
```

## Run

#### Permission to run on Production env
tbd

### Run in Web Console

### Run as REST API
Run GCP Dataflow template job using REST API sample:

Ref: 

- https://cloud.google.com/dataflow/docs/guides/templates/provided-batch#running-the-bigquery-to-elasticsearch-template
- https://cloud.google.com/dataflow/docs/guides/templates/running-templates#example-1:-creating-a-custom-template-batch-job


```bash
$ curl \
--url "https://dataflow.googleapis.com/v1b3/projects/dataflow-eg/locations/us-central1/templates:launch?gcsPath=gs://dataflow-eg-dataflow-poc/templates/wordcount" \
--request POST \
--header "Authorization: Bearer "$(gcloud auth print-access-token) \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
    "jobName": "wordcount-curl-job-'$(date +%Y%m%d-%H%M%S)'",
    "environment": {
        "bypassTempDirValidation": false,
        "tempLocation": "gs://dataflow-eg-dataflow-poc/tmp/",
        "ipConfiguration": "WORKER_IP_UNSPECIFIED",
        "additionalExperiments": []
    },
    "parameters": {
        "input": "gs://dataflow-samples/shakespeare/kinglear.txt",
        "output": "gs://dataflow-eg-dataflow-poc/results/outputs-templated-curl"
    }
}'

# sample output:
{
  "job": {
    "id": "2022-02-16_01_15_13-5260506404532792394",
    "projectId": "dataflow-eg",
    "name": "wordcount-curl-job-20220216-144511",
    "type": "JOB_TYPE_BATCH",
    "currentStateTime": "1970-01-01T00:00:00Z",
    "createTime": "2022-02-16T09:15:13.997352Z",
    "location": "us-central1",
    "startTime": "2022-02-16T09:15:13.997352Z"
  }
}
```

### Run as Python GCP Client

```python
# dataflow/run_template/main.py 

from googleapiclient.discovery import build

project = 'your-gcp-project'
job = 'unique-job-name'
template = 'gs://dataflow-templates/latest/Word_Count'
parameters = {
    'inputFile': 'gs://dataflow-samples/shakespeare/kinglear.txt',
    'output': 'gs://<your-gcs-bucket>/wordcount/outputs',
}

dataflow = build('dataflow', 'v1b3')
request = dataflow.projects().templates().launch(
    projectId=project,
    gcsPath=template,
    body={
        'jobName': job,
        'parameters': parameters,
    }
)

response = request.execute()
```

Ref: https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/dataflow/run_template

### Run using gcloud CLI

```bash
$ gcloud dataflow jobs run dataflow-templated-wordcount-custom-gcloud-job \
    --region us-central1 \
    --gcs-location gs://apache-beam-eg/templates/wordcount \
    --parameters input=gs://dataflow-samples/shakespeare/kinglear.txt,output=gs://apache-beam-eg/results/output_wordcount_gcloud

# sample output:
createTime: '2022-02-11T09:37:25.311851Z'
currentStateTime: '1970-01-01T00:00:00Z'
id: 2022-02-11_01_37_24-16510436790575398178
location: us-central1
name: dataflow-templated-wordcount-custom-gcloud-job
projectId: apache-beam-eg
startTime: '2022-02-11T09:37:25.311851Z'
type: JOB_TYPE_BATCH
```

## Schedule

Refer to [DevOps/GCP/Setup/gcloud CLI](/Engineering/Software-Engineering/DevOps/Clouds/gcp/).

## Clean

### Clean up the Classic Template resources

Stop the Dataflow pipeline.

```
gcloud dataflow jobs list \
  --filter 'NAME=<job name> AND STATE=Running' \
  --format 'value(JOB_ID)' \
  --region "$REGION" \
  | xargs gcloud dataflow jobs cancel --region "$REGION"
```

Delete the template spec file from Cloud Storage.

```
gsutil rm <TEMPLATE_PATH>
```

### Clean up Google Cloud project resources
Delete the Cloud Scheduler jobs.

```
gcloud scheduler jobs delete <scheduler job name>
```


### how gcp dataflow stores things

```
bucket
    staging/
        job_name_uniq/
            requirements.txt
            apache_beam-2.36.0-cp38-cp38-manylinux1_x86_64.whl
            dataflow_python_sdk.tar
            excel2json_3-0.1.6-py3-none-any.whl
            extra_packages.txt
            pickled_main_session                                # python pickled data of __main__ context
            pipeline.pb                                         # python pickled data of whole python code
            workflow.tar.gz
    templates/
        bigquery-poc-template                                   # a json file
    tmp/
        job_name_uniq/                                          # same as staged one, but here temporary
            requirements.txt
            apache_beam-2.36.0-cp38-cp38-manylinux1_x86_64.whl
            dataflow_python_sdk.tar
            excel2json_3-0.1.6-py3-none-any.whl
            extra_packages.txt
            pickled_main_session                                # python pickled data of __main__ context
            pipeline.pb                                         # python pickled data of whole python code
            workflow.tar.gz
```

### Python packaging
- use of MANIFEST.in with `include_package_data=True` vs `package_data={}`
    - Ref: https://stackoverflow.com/questions/1612733/including-non-python-files-with-setup-py
    - https://docs.python.org/3/distutils/sourcedist.html#the-manifest-in-template

### to
- mention python dependencies
    - https://beam.apache.org/documentation/sdks/python-pipeline-dependencies/ 
    - https://github.com/apache/beam/blob/master/sdks/python/apache_beam/examples/complete/juliaset/setup.py
- nameerror in main.py dataflow template
    - https://cloud.google.com/dataflow/docs/resources/faq#how_do_i_handle_nameerrors
        - use `save_main_session=True`
- pardo examples
    - https://beam.apache.org/documentation/transforms/python/elementwise/pardo/
- job failing due to dependenciesGIT_PAGER
    - not working with requirements mentioned inside setup.py while combination of 3 works i.e.
        - setup.py (required if local imports)
        - extra_packages (required if local deps/.whl/tar.gz)
        - requirements_text (required if pypi/git/remote deps)
        - which contradicts https://issues.apache.org/jira/browse/BEAM-10115
    - setup.py thing not working in flex template
        - symptom: module not found
        - solution: use explicit `--setup_file`
- develop io connector
    - https://beam.apache.org/documentation/io/developing-io-java/
    - https://www.youtube.com/watch?v=e5EdPNAw6N4
    - https://www.youtube.com/watch?v=eAN6rNc6EjE
- production ready arch
    - https://cloud.google.com/architecture/building-production-ready-data-pipelines-using-dataflow-developing-and-testing
- empty PCollection
    - https://stackoverflow.com/questions/47624146/apache-beam-initialize-an-pcollection-to-empty
- DoFn vs PTransforms
    - https://stackoverflow.com/questions/47706600/apache-beam-dofn-vs-ptransform
- catch:
    - while running flex template, don't set runner explicitely to Dataflow otherwise another additional job gets triggered
    - by default is uses Dataflow runner only
- observations
    -  work user a/c started experiencing some issue, started using my personal account
    - wheel containing cloudvision-python as git dep `pkg @ url` works fine - except the kedro logging.yml part - on my personal account (see below cmd)
    - multiple `--extra_package` is allowed - incase need to pass cloudvision.whl




# Flex Template

- https://cloud.google.com/dataflow/docs/guides/templates/using-flex-templates#python_3

## Why

### Flex Template over Classic Template
Ref: https://cloud.google.com/dataflow/docs/concepts/dataflow-templates

## What

## How

- Note: For readability, we recommend that you set the entry point in your Dockerfile. When ENTRYPOINT is not set, Dataflow sets the entry point to the template launcher binary based on SDK language.
    - https://cloud.google.com/dataflow/docs/guides/templates/configuring-flex-templates
- allowed parameters/flags
    - https://cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.locations.flexTemplates/launch#flextemplateruntimeenvironment

## Create

## Stage

## Run

### Permission required
- for Flex templates: https://cloud.google.com/dataflow/docs/guides/templates/configuring-flex-templates#understanding_flex_template_permissions


### Allowed ENV variables
- https://cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.locations.flexTemplates/launch#flextemplateruntimeenvironment

## Build
### Allowed options/args/params
- https://cloud.google.com/sdk/gcloud/reference/beta/dataflow/flex-template/build

- `--env`
    - https://cloud.google.com/sdk/gcloud/reference/beta/dataflow/flex-template/build#--env
    - Allowed ENV vars
        - https://cloud.google.com/dataflow/docs/guides/templates/configuring-flex-templates#setting_required_dockerfile_environment_variables

### Custom Worker Image

- Use mutistage Docker build
    - https://cloud.google.com/dataflow/docs/guides/using-custom-containers?hl=en#use_a_custom_base_image_or_multi-stage_builds

# Tech Concept

https://cloud.google.com/dataflow/docs/concepts

# Setup

## GCP Account
- https://console.cloud.google.com/freetrial

## gcloud CLI

Refer to [DevOps/GCP/Setup/gcloud CLI](/Engineering/Software-Engineering/DevOps/Clouds/gcp/).

## `python 3.8`

Use `pyenve`/`conda` to install appropriate python version.

# Apache Beam Job

- https://cloud.google.com/dataflow/docs/quickstarts/quickstart-python
Follow [Apache Beam](/Engineering/Software-Engineering/Data-Engineering/apache_beam/) to write a sample Apache Beam pipeline, run them locally using Dataflow runner.

# Authentication & Authorization

To run the GCP dataflow template in cloud using REST.

Authorization:

- OAuth2/OIDC scope: https://cloud.google.com/dataflow/docs/reference/rest/v1b3/projects.templates/launch

Authentication:

- https://cloud.google.com/docs/authentication/
- https://cloud.google.com/docs/authentication/getting-started#auth-cloud-implicit-python
- https://stackoverflow.com/questions/57433397/how-to-authorize-an-http-post-request-to-execute-dataflow-template-with-rest-api

# Access Control with IAM

For service accounts:

- https://cloud.google.com/dataflow/docs/concepts/access-control#roles


# Network Config
- https://console.cloud.google.com/networking/networks/list?project=dataflow-eg


# CI/CD / Production Grade / Best Practice

- https://cloud.google.com/architecture/cicd-pipeline-for-data-processing
- https://cloud.google.com/architecture/building-production-ready-data-pipelines-using-dataflow-deploying
- https://medium.com/@zhongchen/dataflow-ci-cd-with-cloudbuild-1ad503c1c81
- https://medium.com/everything-full-stack/dataflow-ci-cd-with-github-actions-65765f09713f
- https://medium.com/@emailchhavisharma/quick-steps-to-build-deploy-dataflow-flex-templates-python-java-728fc366f0d1
- https://github.com/kwadie/dataflow-templates-cicd
- https://dataintegration.info/why-you-should-be-using-flex-templates-for-your-dataflow-deployments
    - https://github.com/slilichenko/dataflow-jdbc-replication


# Observability

## Monitoring & Troubleshooting

- https://cloud.google.com/dataflow/pipelines/dataflow-monitoring-intf
- https://cloud.google.com/dataflow/pipelines/troubleshooting-your-pipeline

## Execution Detail

https://cloud.google.com/dataflow/docs/concepts/execution-details

# FAQ
https://cloud.google.com/dataflow/docs/resources/faq


# Deep
- https://storage.googleapis.com/pub-tools-public-publication-data/pdf/41378.pdf
- https://medium.com/@raigonjolly/dataflow-for-google-cloud-professional-data-exam-9efd59377068

## Parallelism

- https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline#parallelization-and-distribution
- --num_workers=1-1000|3
- --autoscaling_algorithm=NONE|THROUGHPUT_BASED
- max_num_workers

## Autoscaling
- https://thegcpgurus.com/cloud-dataflow-how-to-implement-auto-scaling-data-pipelines/
- https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline#batch-autoscaling
- https://www.youtube.com/watch?v=a7CymWiX3oM&t=399s

## Autoscaling not working
- https://stackoverflow.com/questions/53885306/why-do-i-need-to-shuffle-my-pcollection-for-it-to-autoscale-on-cloud-dataflow

### Reshuffling
- https://beam.apache.org/documentation/transforms/python/other/reshuffle/
- https://stackoverflow.com/questions/54121642/apache-beam-dataflow-reshuffle
- https://www.programcreek.com/python/example/122924/apache_beam.Reshuffle
- https://beam.apache.org/releases/pydoc/current/apache_beam.transforms.util.html?highlight=reshuffle#apache_beam.transforms.util.Reshuffle
- https://stackoverflow.com/questions/53885306/why-do-i-need-to-shuffle-my-pcollection-for-it-to-autoscale-on-cloud-dataflow
- https://stackoverflow.com/questions/41212272/google-cloud-dataflow-consume-external-source
- https://stackoverflow.com/questions/46116443/dataflow-streaming-job-not-scaleing-past-1-worker
- https://stackoverflow.com/questions/46807450/scaling-of-pardo-transforms-having-blocking-network-calls
- https://stackoverflow.com/questions/41268877/dataflow-is-it-possible-to-run-parts-of-the-pipeline-synchronously-and-other-pa


## Optimization
- https://www.carted.com/blog/improving-dataflow-pipelines-for-text-data-processing/
- https://cloud.google.com/dataflow/docs/concepts/execution-details

# References
- external
    - https://medium.com/@zhongchen/schedule-your-dataflow-batch-jobs-with-cloud-scheduler-8390e0e958eb
    	- https://github.com/zhongchen/GCP-Demo/tree/master/demos/scheduler-dataflow-demo/terraform
    - https://medium.com/@jamesmoore255/creating-a-template-for-the-python-cloud-dataflow-sdk-2fe36cc4167f
- google
    - [pricing calc](https://cloud.google.com/products/calculator)
