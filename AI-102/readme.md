# Microsoft Certified: Azure AI Engineer Associate (AI-102) <img src="images/microsoft-certified-associate-badge.svg" style="width:60px; height:60px;">

Design and implement an Azure AI solution using Azure AI services, Azure AI Search, and Azure Open AI.

- ### Microsoft Learn [link](https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-engineer) 

## [Get started with Azure AI Services](https://learn.microsoft.com/en-us/training/paths/get-started-azure-ai/)

- ### [Plan and prepare to develop AI solutions on Azure](https://learn.microsoft.com/en-us/training/modules/prepare-azure-ai-development/)
    - **Hubs**: A hub provides a centrally managed collection of shared resources and management configuration for AI solution development. You need at least one hub to use all of the solution development features and capabilities of AI Foundry. When you create a Azure AI Hub, four additional resources are created: A multi-service Azure AI Services, a KeyVault, a Storage Account and (optionally) an Azure AI Search.
    - **Projects**: A hub can support one or more projects, each of which is used to organize the resources and assets required for a particular AI development effort.
    - **Azure AI Developer** role: All permissions except create new hubs and manage the hub permissions.
    - **Azure AI Inference Deployment Operator** role : All permissions required to create a resource deployment within a resource group.
    - **Responsible AI**
        - Fairness
        - Reliability and safety
        - Privacy and security
        - Inclusiveness
        - Transparency
        - Accountability


- ### [Create and consume Azure AI services](https://learn.microsoft.com/en-us/training/modules/create-manage-ai-services/)
    - You can provision an AI services resource that supports multiple different AI services. For example, you could create a single resource that enables you to use the Azure AI Language, Azure AI Vision, Azure AI Speech, and other services.
    - To consume the service through the endpoint, applications require the following information:
        - **The endpoint URI**. This is the HTTP address at which the REST interface for the service can be accessed.
        - **A subscription key**. Access to the endpoint is restricted based on a subscription key. Client applications must provide a valid key to consume the service. 
        - **The resource location**. When you provision a resource in Azure, you generally assign it to a location, which determines the Azure data center in which the resource is defined.
    - Azure AI services provide **REST** application programming interfaces (APIs) that client applications can use to consume services.



- ### [Secure Azure AI services](https://learn.microsoft.com/en-us/training/modules/secure-ai-services/)
    - **Regenerate keys**: You should regenerate keys regularly to protect against the risk of keys being shared with or accessed by unauthorized users. You can regenerate keys using the Azure portal, or using the az cognitiveservices account keys regenerate Azure command-line interface (CLI) command.
    - **Azure Key Vault**: Azure Key Vault is an Azure service in which you can securely store secrets (such as passwords and keys). Access to the key vault is granted to security principals, which you can think of user identities that are authenticated using Microsoft Entra ID. Administrators can assign a security principal to an application (in which case it is known as a service principal) to define a managed identity for the application.
    - Authenticate using service principals: Assign the *Cognitive Services Users* role.
    - Authenticate using managed identities: We have two types, System-assigned managed identity and User-assigned managed identity, you give the *Cognitive Services Contributor* role.
    - Configuring network access restrictions: 
        - **Selected Networks and Private Endpoints**: Blocks connections to the resource, unless a rule allows access to it. These rules can be set for Azure virtual networks, IP addresses, CIDR, or Private Endpoints. 
        - **Disabled**: Blocks all traffic to the resource. You can still add access to Private Endpoints. This is the most restrictive option.
- ### [Monitor Azure AI services](https://learn.microsoft.com/en-us/training/modules/monitor-ai-services/)
    - **Azure Event Hubs** allows you to forward the data on to a custom telemetry solution and connect directly to some third-party solutions. However, in most cases you'll use one (or both) of the following kinds of resource within your Azure subscription:
        - **Azure Log Analytics**: a service that enables you to query and visualize log data within the Azure portal.
        - **Azure Storage**: a cloud-based data store that you can use to store log archives.
- ### [Deploy Azure AI services in containers](https://learn.microsoft.com/en-us/training/modules/investigate-container-for-use-with-ai-services/)
    - Azure AI services container configuration: When you deploy an Azure AI services container image to a host, you must specify three settings.

        Setting | Description
        ---|---
        ApiKey | Key from your deployed Azure AI service; used for billing
        Billing	| Endpoint URI from your deployed Azure AI service; used for billing.
        Eula	| Value of accept to state you accept the license for the container.
- ### [Use AI responsibly with Azure AI Content Safety](https://learn.microsoft.com/en-us/training/modules/responsible-content-safety/)
    - **Content Safety**: Azure AI Content Safety is a set of advanced content moderating features that can be incorporated into your applications and services. Azure AI Content Safety is available as a resource in the Azure portal. It is designed to be used in applications and services to protect against harmful user-generated and AI-generated content. Azure AI Content Safety is available as part of Azure AI Foundry.
    - Azure AI Content Safety classifies content into four categories:

        ![content_safety_cats](images/content_safety_cats.png)
    - **Prompt shields** is a unified API to identify and block jailbreak attacks from inputs to LLMs
    - **Groundedness** detection protects against inaccurate responses in AI-generated text by LLMs.


## [Create computer vision solutions with Azure AI Vision](https://learn.microsoft.com/training/paths/create-computer-vision-solutions-azure-ai/)

- ### [Analyze images](https://learn.microsoft.com/en-us/training/modules/analyze-images/)
    - **Azure AI Vision** service is designed to help you extract information from images
    - Use **Analyze Image** REST method or the SDK of C#/Python
        ```python
        from azure.ai.vision.imageanalysis import ImageAnalysisClient
        from azure.ai.vision.imageanalysis.models import VisualFeatures
        from azure.core.credentials import AzureKeyCredential

        client = ImageAnalysisClient(
            endpoint=os.environ["ENDPOINT"],
            credential=AzureKeyCredential(os.environ["KEY"])
        )

        result = client.analyze(
            image_url="<url>",
            visual_features=[VisualFeatures.CAPTION, VisualFeatures.READ],
            gender_neutral_caption=True,
            language="en",
        )
        ```
        - VisualFeatures.TAGS: Identifies tags about the image, including objects, scenery, setting, and actions
        - VisualFeatures.OBJECTS: Returns the bounding box for each detected object
        - VisualFeatures.CAPTION: Generates a caption of the image in natural language
        - VisualFeatures.DENSE_CAPTIONS: Generates more detailed captions for the objects detected
        - VisualFeatures.PEOPLE: Returns the bounding box for detected people
        - VisualFeatures.SMART_CROPS: Returns the bounding box of the specified aspect ratio for the area of interest
        - VisualFeatures.READ: Extracts readable text
    - Result of analyze images is a JSON
    ```json
        {
            "apim-request-id": "abcde-1234-5678-9012-f1g2h3i4j5k6",
            "modelVersion": "<version>",
            "denseCaptionsResult": {
                "values": [
                {
                    "text": "a house in the woods",
                    "confidence": 0.7055229544639587,
                    "boundingBox": {
                    "x": 0,
                    "y": 0,
                    "w": 640,
                    "h": 640
                    }
                },
                {
                    "text": "a trailer with a door and windows",
                    "confidence": 0.6675070524215698,
                    "boundingBox": {
                    "x": 214,
                    "y": 434,
                    "w": 154,
                    "h": 108
                    }
                }
                ]
            },
            "metadata": {
                "width": 640,
                "height": 640
            }
        }
    ```
- ### [Classify images](https://learn.microsoft.com/en-us/training/modules/classify-images/)
    - **Azure AI Custom Vision** service enables you to build your own computer vision models for image classification or object detection Creating an Azure AI Custom Vision solution involves two tasks:
        1. Use existing (labeled) images to train an Azure AI Custom Vision model.
        2. Create a client application that submits new images to your model to generate predictions.
    - To use the Azure AI Custom Vision service, you **must provision two kinds** of Azure resource:
         1. A training resource used to train your models. This can be an Azure AI services multi-service resource or an Azure AI Custom Vision (Training) resource.
         2. A prediction resource, used by client applications to get predictions from your model. This can be an Azure AI services multi-service resource or an Azure AI Custom Vision (Prediction) resource.
- ### [Detect objects in images](https://learn.microsoft.com/en-us/training/modules/detect-objects-images/)
    - The most significant difference between training an image classification model and training an object detection model is the labeling of the images with tags. While image classification requires one or more tags that apply to the whole image, object detection requires that each label consists of a tag and a region that defines the bounding box for each object in an image.
- ### [Detect, analyze, and recognize faces](https://learn.microsoft.com/en-us/training/modules/detect-analyze-recognize-faces/)
    - **Face** service offers more comprehensive facial analysis capabilities than the Azure AI Vision service.
    - To detect and analyze faces with the Azure AI Vision service, call the **Analyze Image** function (SDK or equivalent REST method), specifying ***People*** as one of the visual features to be returned.
    - To train a facial recognition model with the Face service:
        1. Create a **Person Group** that defines the set of individuals you want to identify (for example, employees).
        2. Add a **Person** to the **Person Group** for each individual you want to identify.
        3. Add detected faces from multiple images to each **person**, preferably in various poses. The IDs of these faces will no longer expire after 24 hours (so they're now referred to as *persisted faces*).
        4. Train the model.

            ![Face_person_groups](images/Face_person_groups.png)

- ### [Read Text in images and documents](https://learn.microsoft.com/en-us/training/modules/read-text-images-documents-with-computer-vision-service/)
  
  - **Image Analysis Optical character recognition (OCR)**:
        - Use this feature for general, unstructured documents with smaller amount of text, or images that contain text.
        - Results are returned immediately (synchronous) from a single API call.
        - Has functionality for analyzing images past extracting text, including object detection, describing or categorizing an image, generating smart-cropped thumbnails and more.
        - Examples include: street signs, handwritten notes, and store signs.
  - **Document Intelligence**:
        - Use this service to read small to large volumes of text from images and PDF documents.
        - This service uses context and structure of the document to improve accuracy.
        - The initial function call returns an asynchronous operation ID, which must be used in a subsequent call to retrieve the results.
        - Examples include: receipts, articles, and invoices.
    - If using the **REST API**, specify the feature as `read`: ```https://<endpoint>/computervision/imageanalysis:analyze?features=read&...```

- ### [Analyze video](https://learn.microsoft.com/en-us/training/modules/analyze-video/)

    - The **Azure Video Indexer** service is designed to help you extract information from videos.
    - **Azure Video Indexer API**: `https://api.videoindexer.ai/Auth/<location>/Accounts/<accountId>/AccessToken`. You can then use your token to consume the REST API and automate video indexing tasks, creating projects, retrieving insights, and creating or deleting custom models. For example, a GET call to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Customization/CustomLogos/Logos/<logoId>?<accessToken>` REST endpoint returns the specified logo. In another example, you can send a GET request to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos?<accessToken>`, which returns details of videos in your account

## [Develop natural language processing solutions with Azure AI Services](https://learn.microsoft.com/en-us/training/paths/develop-language-solutions-azure-ai/)

- ### [Analyze text with Azure AI Language](https://learn.microsoft.com/en-us/training/modules/analyze-text-ai-language/)
  
  - **Azure AI Language** is designed to help you extract information from text.
  - **Language detection** - determining the language in which text is written.
    - Document size under 5,120 characters.
    - Limit per document is 1,000 items(IDs)
    - Example request body with a list of **documents**, containing a unique **id** and the **text** to be analyzed. **countryHint** improves the prediction performance:
    ```json
    {
    "kind": "LanguageDetection",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
              {
                "id": "1",
                "text": "Hello world",
                "countryHint": "US"
              },
              {
                "id": "2",
                "text": "Bonjour tout le monde"
              }
        ]
    }
    ```
    - If the text you provide cannot be parsed by the analyzer, the **(Unkownn)** will be returned as result ion the *name and ISO*, as well as **0** in *confidenceScore*
  - **Key phrase extraction** - identifying important words and phrases in the text that indicate the main points.
    - Document size under 5,120 characters.
    - Limit per document is 1,000 items(IDs)
    - Example REST request:
    ```json
    {
        "kind": "KeyPhraseExtraction",
        "parameters": {
            "modelVersion": "latest"
        },
        "analysisInput":{
            "documents":[
                {
                "id": "1",
                "language": "en",
                "text": "You must be the change you wish 
                        to see in the world."
                },
                {
                "id": "2",
                "language": "en",
                "text": "The journey of a thousand miles 
                        begins with a single step."
                }
            ]
        }
    }
    ```
  - **Sentiment analysis** - quantifying how positive or negative the text is.
    - Example REST request:
    ```json
    {
        "kind": "SentimentAnalysis",
        "parameters": {
            "modelVersion": "latest"
        },
        "analysisInput": {
            "documents": [
            {
                "id": "1",
                "language": "en",
                "text": "Good morning!"
            }
            ]
        }
    }
    ```
  - **Named entity recognition** - detecting references to entities, including people, locations, time periods, organizations, and more.
    - Entities are grouped into categories (e.g., Person, Location, DateTime, Organization, etc.)
  - Example REST request:
    ```json
    {
        "kind": "EntityRecognition",
        "parameters": {
            "modelVersion": "latest"
        },
        "analysisInput": {
            "documents": [
            {
                "id": "1",
                "language": "en",
                "text": "Joe went to London on Saturday"
            }
            ]
        }
    }
    ```
  - **Entity linking** - identifying specific entities by providing reference links to Wikipedia articles.
    - Entity linking can be used to disambiguate entities of the same name by referencing an article in a knowledge base.
    - Example REST request:
    ```json
    {
        "kind": "EntityLinking",
        "parameters": {
            "modelVersion": "latest"
        },
        "analysisInput": {
            "documents": [
            {
                "id": "1",
                "language": "en",
                "text": "I saw Venus shining in the sky"
            }
            ]
        }
    }
    ```
- ### [Create question answering solutions with Azure AI Language](https://learn.microsoft.com/en-us/training/modules/create-question-answer-solution-ai-language/)

    - Azure AI Language includes a *question answering capability*, which enables you to define a **knowledge base** of question and answer pairs that can be queried using natural language input. **Knowledge base** can be created from existing sources, including:
      - Web sites containing frequently asked question (FAQ) documentation.
      - Files containing structured text, such as brochures or user guides.
      - Built-in chit chat question and answer pairs that encapsulate common conversational exchanges.
    - Comparison between *question answering client* and *language understanding*
  
        |  | Question answering | Language understanding |
        |---	|---	|---	|
        | Usage pattern 	| User submits a question, expecting an answer 	| User submits an utterance, expecting an appropriate response or action 	|
        | Query processing 	| Service uses natural language understanding to match the question to an answer in the knowledge base 	| Service uses natural language understanding to interpret the utterance, match it to an intent, and identify entities 	|
        | Response 	| Response is a static answer to a known question 	| Response indicates the most likely intent and referenced entities 	|
        | Client logic 	| Client application typically presents the answer to the user 	| Client application is responsible for performing appropriate action based on the detected intent 	|
    - To consume the published knowledge base, you can use the REST interface. The minimal request body for the function contains a question, like this:
        ```json
        {
        "question": "What do I need to do to cancel a reservation?",
        "top": 2,
        "scoreThreshold": 20,
        "strictFilters": [
            {
            "name": "category",
            "value": "api"
            }
        ]
        }
        ```
    - **Active learning** enhances the ability to improve responses to user questions by considering different phrasings that convey the same meaning. It helps in continuously refining answers by evaluating various ways questions might be asked. This process is enabled by default.

- ### [Build a conversational language understanding model](https://learn.microsoft.com/en-us/training/modules/build-language-understanding-model/)
  
  - **Pre-configured features**: Summarization, Named entity recognition, Personally identifiable information (PII) detection, Key phrase extraction, Sentiment analysis, Language detection
  - **Personally identifiable information (PII)** detection helps identify, categorize, and redact sensitive information such as email addresses, home addresses, IP addresses, names, and protected health information. For instance, an email address like "email@contoso.com" in a query can be identified and redacted to protect privacy.
  - **Learned features** require you to label data, train, and deploy your model to make it available to use in your application. These features allow you to customize what information is predicted or extracted.
    - Conversational language understanding (CLU): CLU does require data to be tagged by the user to teach it how to predict intents and entities accurately.
    - Custom named entity recognition
    - Custom text classification
    - Question answering
  - **Authentication**: We MUST use the **Ocp-Apim-Subscription-Key** to the header of our request, to use the Azure AI Language
  - REST endpoint for conversational language understanding: `{ENDPOINT}/language/authoring/analyze-conversations/projects/{PROJECT-NAME}/deployments/{DEPLOYMENT-NAME}?api-version={API-VERSION}`
  - Query your model with REST API: `{ENDPOINT}/language/:analyze-text?api-version={API-VERSION}`. Within the body of that request, you must specify the `kind` parameter, which tells the service what type of language understanding you're requesting. (For CLU: `{ENDPOINT}/language/:analyze-conversations?api-version={API-VERSION}`)