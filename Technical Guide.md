# Communication Developer Services ISV Partner Guide
## What is Communication Developer Services(CDS)?
Communication Developer Services (**CDS**) is the new portfolio name that refers to three AWS services (Pinpoint, SES, and Chime SDK) coming together to form the foundation of communication cloud services. The capabilities of these cloud services are used by enterprises to reach their customers to improve communication engagement. Use cases like identity verification through One-Time-Password, Interactive Voice Response, appointment reminders, and notifications are growing as enterprises expand adoption of digital engagement with their customers and citizens. CDS is a set of stand-alone services or SDKs and APIs that allow developers to embed customer communications directly into their applications, which reduce the need for specialized developers and a one size fits all approach to scaled customer engagement. CDS is part of the CPaaS market category and our ability to build demand generation was enhanced with the recent inclusion of CDS in the Gartner CPaaS Market Category and Customer Guide, with Gartner highlighting SMS Application to Person message sending, two factor authentication and IVR, as foundational services within CPaaS. These foundational capabilities align with the capabilities provided by Pinpoint, SES and Chime SDK

## Use Cases
- [Common Pinpoint Use Cases ](https://docs.aws.amazon.com/pinpoint/latest/userguide/welcome.html) 
	- **Omni-Channel Messaging** - Leverage email, SMS, push, in-app notifications, voice, or custom channels to deliver communications via API or a console based experience
	- **Alerts + Notifications -** Send customers alerts or notifications through email, SMS, push, in-app notifications, or voice via API or a console based experience
	- **Promotional Messages -** Send promotions and marketing messages with segmented and personalized messaging through one or many different channels via API or a console based experience
	- **Transactional Messages -** Send transactional messages with segmented and personalized messaging through one or many different channels via API or a console based experience
	- **Triggered Messages -** Send messages in response to events in real-time with segmented and personalized messaging through one or many different channels via API or a console based experience
	- **Journeys -** Create multi-step engagement experiences through one or many different channels via API or a console based experience that can change based on the response of the customers enrolled 
- [Common SES Use Cases](https://docs.aws.amazon.com/ses/latest/dg/Welcome.html)
	- **Promotional Messages -** Send promotional and marketing email programmatically using APIs or SMTP
	- **Transactional Messages -** Send transactional email programmatically using APIs or SMTP
	- **Receive and Process Email** - Use a rules based engine to receive and process email 
- [Common Chime Use Cases](https://docs.aws.amazon.com/chime-sdk/latest/ag/what-is-chime-sdk.html)
	-  **In-App Video -** Build your application or website with scalable video technology that can support telehealth, field support, education, and more
	-  **Interactive Voice Response (IVR) -** Build an IVR system that can support touch-tone, conversation voice bots, and text-to-speech
	- **Real-Time Call Transcription and Analytics -** Generate live, user-attributed transcripts of your meetings and at the same time identify customer experience issues and sentiment in real time

- ## Common Combined Use Cases by Industry  
	- **Telehealth**:
		- Schedule appointments online or with a mobile app
		- Appointment confirmations 
		- Receive SMS reminders and useful information about your upcoming visit 
		- Meet your healthcare provider via audio/video
	-   **Local Ordering and Delivery:**
		- Order food by calling the restaurant
		- Restaurant agentless order taking
			- Once the order is confirmed, customer receives email confirmation
			- As the customer heads to pickup, the customer gets SMS notifications about the order progress until delivery
			- Finally once the order is complete, the customer receives an email with the final invoice and order summary
	-   **Contact Center/Customer Engagement:**
		- Incoming/Outgoing call
		- SMS notifications on progress of request
		- Email confirmation &/or Follow Ups
		- Automated Ticket Booking
	-   **Travel Interruption:**
		- \1-800 call to Contact Center
 		- SMS confirmation of use identity and selection of refund options
 		- Confirmation of modified itinerary via email
	-	**Bank Fraud Alert:**
 		- Automated call to alert regarding suspicious activity on bank account
 		- Authentication and confirmation/rejection of suspect transactions via SMS
 		- Email confirmation regarding removal of temporary freeze or dispatch of new card via email
	-	**Edutech:**
 		- Video classes
 		- In-class engagement questions and polls sent
		- Follow up / Email engagement	
	
# CDS Services

## What is Amazon Pinpoint?
Amazon Pinpoint is a multi-channel communication orchestration service. It enables you to coordinate and send messages across email, SMS, push, in-app, voice, and custom channels. Pinpoint is an integral part of our suite of Communication Developer Services. 

## What is Amazon Simple Email Service(SES)?
Amazon SES is a cloud email service provider that can integrate into any application for bulk email sending. Whether you send transactional or marketing emails, you pay only for what you use. Amazon SES also supports a variety of deployments including dedicated, shared, or owned IP addresses. Reports on sender statistics and a deliverability dashboard help businesses make every email count.

## What is Chime SDK?
The Amazon Chime SDK is a set of real-time communications components that you can use to quickly add messaging, audio, video, and screen sharing capabilities to their web or mobile applications.

You can use the Amazon Chime SDK to build real-time media applications that can send and receive audio and video and allow content sharing.

**Other Commonly Used Services
-   [Amazon Personalize](https://aws.amazon.com/personalize/)
	- Amazon Personalize allows developers to quickly build and deploy curated recommendations and intelligent user segmentation at scale using machine learning (ML). Because Amazon Personalize can be tailored to your individual needs, you can deliver the right customer experience at the right time and in the right place.
		- In Amazon Pinpoint, [you can connect to a certain type of ML model](https://docs.aws.amazon.com/pinpoint/latest/userguide/ml-models.html), referred to as a _recommender model_, to predict which items a user will interact with and to send those items to message recipients as personalized recommendations. A _recommender model_ is an ML model that's designed to answer the question, "What will a user like or be interested in?" It predicts what a particular user will prefer from a given set of products or items, and it provides that information as a set of recommendations for the user. By using recommender models with Amazon Pinpoint, you can send personalized recommendations to message recipients based on each recipient's attributes and behavior. Email, SMS, and Push templates can all use recommendations.
-   [Amazon Connect](https://aws.amazon.com/connect/)
	- Amazon Connect is an easy-to-use omnichannel cloud contact center service offering superior, low-cost customer service using machine learning (ML), interactive voice response (IVR), and call center routing.
		- [Connect can be used with Pinpoint Journeys](https://docs.aws.amazon.com/pinpoint/latest/userguide/journeys-add-activities.html#journeys-add-activities-procedures-contact-center) to do outbound dialing at scale. You can configure this activity type to dial the journey participant's phone number and either connect them to an agent, or play a voice message. 
-   [Amazon Kinesis](https://aws.amazon.com/kinesis/data-firehose/)
	- Amazon Kinesis Data Firehose is an extract, transform, and load (ETL) service that reliably captures, transforms, and delivers streaming data to data lakes, data stores, and analytics services.
		- [Amazon Pinpoint can stream engagement and application usage data](https://docs.aws.amazon.com/pinpoint/latest/userguide/analytics-streaming.html), known as _event data_, to supported AWS services that provide more options for analysis and storage. Amazon Pinpoint retains this data for 90 days. To keep this data for an indefinite period of time or to analyze it with custom queries and tools, you can configure Amazon Pinpoint to send event data to Amazon Kinesis.
			- A [common implementation is streaming to S3](https://aws.amazon.com/solutions/implementations/digital-user-engagement-events-database/?did=sl_card&trk=sl_card) where it can be queried by Amazon Athena or leverage Amazon Quicksight to build BI dashboards
-    [Amazon S3](https://aws.amazon.com/s3/)
	- Amazon Simple Storage Service (Amazon S3) is an object storage service offering industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can store and protect any amount of data for virtually any use case, such as data lakes, cloud-native applications, and mobile apps.
		- S3 is commonly used for:
			- [Data Lakes for Message Archiving](https://github.com/aws-samples/communication-developer-services-reference-architectures#Pinpoint-Message-Archiver)
			- [Importing Endpoints](https://github.com/aws-samples/communication-developer-services-reference-architectures/blob/master/README.md#Amazon-S3-Triggered-Endpoint-Imports)
			- [Hosting Images](https://github.com/aws-samples/communication-developer-services-reference-architectures#simple-cms-or-static-website-host)
			- [Hosting Files to be attached](https://github.com/aws-samples/communication-developer-services-reference-architectures#simple-cms-or-static-website-host)
			- [Hosting Static Websites](https://github.com/aws-samples/communication-developer-services-reference-architectures/blob/master/README.md#simple-cms-or-static-website-host)
			- [Hosting Preference Centers](https://aws.amazon.com/solutions/implementations/amazon-pinpoint-preference-center/)
- [Amazon Athena](https://aws.amazon.com/athena/)
	- Amazon Athena is a serverless, interactive analytics service built on open-source frameworks, supporting open-table and file formats. Athena provides a simplified, flexible way to analyze petabytes of data where it lives. Analyze data or build applications from an Amazon Simple Storage Service (S3) data lake and 25+ data sources, including on-premises data sources or other cloud systems using SQL or Python.
- [Amazon Quicksight](https://aws.amazon.com/quicksight/)
	- Amazon QuickSight powers data-driven organizations with unified business intelligence (BI) at hyperscale. With QuickSight, all users can meet varying analytic needs from the same source of truth through modern interactive dashboards, paginated reports, embedded analytics, and natural language queries.
- [AWS Lambda](https://aws.amazon.com/lambda/)
	- AWS Lambda is a serverless, event-driven compute service that lets you run code for virtually any type of application or backend service without provisioning or managing servers. You can trigger Lambda from over 200 AWS services and software as a service (SaaS) applications, and only pay for what you use.
		- Lambda is used heavily in many areas of Pinpoint architecture. Some common uses include:
			- [Custom Channels](https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-custom.html)
				- [Connect to 3rd party services with a REST API](https://github.com/aws-samples/communication-developer-services-reference-architectures#connect-or-facebook-whatsapp-twitter-anything-as-a-pinpoint-campaign-channel). Pinpoint passes 50 endpoints at a time to Lambda which can be used to interact with services such as WhatsApp, Twitter, Slack, Amazon Connect, etc.

## CDS Resources
#### Pinpoint
* [Amazon Pinpoint Home](https://aws.amazon.com/pinpoint/)
* [Amazon Pinpoint Documentation](https://docs.aws.amazon.com/pinpoint/)
* [Solution Repository](https://github.com/aws-samples/digital-user-engagement-reference-architectures)
* [Pinpoint Workshop](https://catalog.us-east-1.prod.workshops.aws/workshops/070a93a2-3373-4736-8af0-f7a08c9eb08a/en-US/getting-started)
#### SES
* [Amazon Simple Email Service Home](https://aws.amazon.com/ses/)
* [Amazon Simple Email Service Documentation](https://docs.aws.amazon.com/ses/index.html)
#### Chime
* [Amazon Chime SDK Home](https://aws.amazon.com/chime/chime-sdk/)
* [Amazon Chime SKD Documentation](https://docs.aws.amazon.com/chime-sdk/index.html)
* [Live Sandbox](https://codesandbox.io/s/amazon-cds-meeting-sandbox-3mxuzz)
* [Live Demo](https://demo.chime.aws/)