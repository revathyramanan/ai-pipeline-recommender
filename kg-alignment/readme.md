## Alignment of KG Concepts
As the data from various sources follow different nomenclature and data structure, we propose Common Metadata Ontology(CMO) to unify them. The mapping of each data source to CMO can be found below.


|     **Nodes   in Common Metadata Ontology**                                                                             |     **Papers-with-Code**                  |     **OpenML**                   |     **Huggingface**                   |
|---------------------------------------------------------------------------------------------------------------------|-----------------------------------------|------------------------------|-------------------------------------|
|     **Pipeline:**  AI pipeline executed to solve a Task                                                               |     Extracted from   Paper              |     Flow                     |     Extracted from   Models         |
|     **Report:**     Any   published text document regarding the pipeline implementation                                  |     Paper                               |     Extracted from   runs    |     Extracted from   Model Cards    |
|     **Task:**     The   AI Task for which the pipeline is implemented. Example: image classification                     |     Task                                |     Task type   + Dataset    |     Pipeline   Tag                  |
|     **Framework:**     The   framework used to implement the pipeline and their code repository                          |     Extracted from   Git Repository     |     Extracted from   Runs    |     Library                         |
|     **Stage:**     Various   stages of the pipeline such as data preprocessing, training, testing or   evaluation        |     Generated                           |     Generated                |     Generated                       |
|     **Execution:**     Multiple   executions of a given stage in a pipeline                                              |     Generated                           |     Runs                     |     Generated                       |
|     **Artifact:**     Artifacts   such as model, dataset and metric generated at the end of each execution               |     Generated                           |     Generated                |     Generated                       |
|     **Metric:**     Subclass   of artifact. The evaluation result of each execution                                      |     Evaluation   and Results            |     Extracted from   runs    |     N/A                             |
|     **Dataset:**     Subclass   of artifact. The dataset used in each execution.                                         |     Dataset                             |     Dataset                  |     Dataset                         |
|     **Model:**     Subclass   of artifact. The model used in each execution or produced as a result of an   execution    |     Method                              |     Extracted from   Flow    |     Model                           |
|     **Hyperparameters:**     Parameter   setting using for each execution of a stage                                     |     N/A                                 |     Extracted from   runs    |     N/A                             |


The current data source do not provide a detailed information on the stage (data preprocessing, training or testing) of the pipeline excution. On the other hand, we know that the pipeline metadata exposed are for train/test stages. Hence we generate the information for stage and so execution. The properties of each node can be found below.

##### Pipeline
* pipeline_id
* pipeline_name
* pipeline_source
* source_id
* custom_properties*

##### Report
* report_id
* report_title
* report_pdf_url
* source
* source_id
* abstract*
* custom_properties*

##### Task
* task_id
* task_name
* task_description
* task_type
* modality
* category
* source
* custom_properties*

##### Framework
* framework_id
* framework_name
* code_repo_url
* framework_version
* source

##### Stage
* stage_id
* stage_name
* source
* pipeline_id
* pipeline_name
* custom_properties

##### Execution
* execution_id
* execution_name
* stage_id
* stage_name
* pipeline_id
* pipeline_name
* source
* command (CLI command to run the execution)
* custom_properties

##### Artifact
* artifact_id
* artifact_name
* pipeline_id
* pipeline_name
* execution_id
* source
* custom_properties

##### Dataset
* dataset_id
* dataset_name
* dataset_url
* modality
* description
* source
* custom_properties

##### Model
* model_id
* model_name
* model_class
* description
* artifact_id
* source
* custom_properties

##### Metric
* metric_id
* metric_name
* artifact_id
* evaluations
* source
* custom_properties**

##### Hyperparameters
* parameter_id
* parameter_setting (key-value pair)
* source
* model_id
* custom_properties


NOTE: 
* *are optional properties
* There additional information on each node, different for each source. As of now, there are included in the KG for efficient search. But they are available to be used in the future to extract the data and populate as node properties.
* **For metric, there are umpteen possible metric names and values. Therefore, we capture all of them as a key value pair under evaluations
* custom_properties are where user can enter custom properties for each node while executing a pipeline
* source is the source from which the node is obtained - papers-with-code, openml, huggingface


