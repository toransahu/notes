<h1>Google Cloud Dataflow </h1>

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
    - arista user a/c started experiencing some issue, started using my personal account
    - wheel containing cloudvision-python as git dep `pkg @ url` works fine - except the kedro logging.yml part - on my personal account (see below cmd)
    - multiple `--extra_package` is allowed - incase need to pass cloudvision.whl




# Flex Template

## Why

## What

## How

# Tech Concept

https://cloud.google.com/dataflow/docs/concepts

# Observability
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
