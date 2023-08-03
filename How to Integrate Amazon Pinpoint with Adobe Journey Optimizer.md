# How to Integrate Amazon Pinpoint with Adobe Journey Optimizer

Amazon Pinpoint is a service that provides SDKs and APIs that allow you to embed customer communications directly into your applications and websites with minimal coding while Adobe Journey Optimizer can manage scheduled cross-channel campaigns and one-to-one moments for millions of customers. Integrating these two services allows you to use AWS’s standard pay-as-you-go pricing for message sending while retaining your data and workflows in Adobe Experience Cloud.

Pinpoint supports SMS, Email, Push/In-App Notifications, Voice, and even OTT platforms such as WhatsApp or Line. This blog post focuses on the SMS channel and how to use Adobe Journey Optimizer to manage the orchestration of customer journeys while using Pinpoint as the delivery partner for the SMS messages. This same architecture could be used to accomplish sends through the other supported channels as well.

Amazon Pinpoint SMS has a global reach that includes over 240 destinations. Origination Identities (Long Codes, Short Codes, 10DLC(US Only), Toll-Free(US Only), and Sender IDs) can be registered and purchased directly through the Amazon Pinpoint Console giving you the ability to send SMS around the world from a single source. 

How to Set Up the Integration Between Amazon Pinpoint and Adobe Journey Optimizer

* AWS Setup
    * Pinpoint
        * Procure at least one Origination Identity in Amazon Pinpoint dependent on which countries you plan on sending to
            * https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-originating-identities-choosing.html
    * Lambda
        * Create a new Lambda function that can authorize the token based API call being made from Adobe Journey Optimizer. Give it a name like "APIAuthorization-Adobe"
            * https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions/APIAuthorization-Adobe?tab=code
        * Create a Lambda that will call Amazon Pinpoint to deliver the SMS message. Give it a name like "Adobe-SMS-Send"
            * https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions/Adobe-SMS-Send?tab=configure
                * Pinpoint expects phone numbers to be in e.164 format. You can use a library such as Google's common Java, C++, and JavaScript library for parsing, formatting, and validating international phone numbers to ensure that your calls are sending the message in the expected e.164 format.
                    * https://github.com/google/libphonenumber
    * API Gateway
        * Create a new Amazon API Gateway that will serve as the destination for your  Adobe Custom Action you will create below.
            * https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html
            * Click on Authorizers and Create a New Authorizer
                * https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html
                * Give it a name
                * Choose Type of Lambda
                * Choose your Lambda Function called  "APIAuthorization-Adobe"
                * Type in your Token Source being used in your call to authenticate
            * Create a new Resource for the Adobe Custom Action to call into
            * Create a new Post Method
                * Select "Lambda Function" as the integration point for the method and copy and paste the ARN for your Lambda Function or begin to type the name of your function called "Adobe-SMS-Send" as the integration point and save.
                * Click on the method request and click the pencil next to "Authorization." Select the Authorizer Lambda you created earlier to interact with and authorize the token provided in the call from the Custom Action in Adobe Journey Optimizer that you create later
                    * https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html
* Adobe Setup
    * Create a Custom Action
        * https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration.html?lang=en
        * https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en
        * Configure the Custom Action
            * Use the Invoke URL from your API Gateway for your URL. The Method should be "POST."
                * https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-call-api.html
            * Authentication Type is API key
            * Name is what you used in your Authorization Lambda for your Token
            * Value is your secret password you set for your Authorization Token
            * Location is "Header"
            * Payload should include at a minimum:
                * Destination Number
                * Message
                * Origination Identity(Optional)
                * SMS Pool(If using SMS V2 API)
    * Create a Journey that includes your Custom Action
        * https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs.html?lang=en
    * Configure either an Entry Event or Segment that adds Profiles into your Journey.
        * https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en
            * Make sure that your profiles contain the phone number in e.164 format or that your code accounts for this format being used via the library mentioned earlier or some other means
        * You can also use test profiles prior to publishing your Journey
            * https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey.html?lang=en
    * Publish your Journey

Additional setup of this solution could include [streaming the SMS delivery data to S3](https://github.com/aws-samples/communication-developer-services-reference-architectures#pinpoint-s3-event-database) to be used for reporting purposes or even [streaming it back into Adobe via an HTTP endpoint](https://aws.amazon.com/blogs/big-data/stream-data-to-an-http-endpoint-with-amazon-kinesis-data-firehose/) and the same API gateway created in the above solution.

