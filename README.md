# How to Develop a Fact Skill for Alexa: Step-by-Step

We want to introduce another way to help you build useful and meaningful skills for Alexa quickly. We have launched a new fact skill template that makes it easy for developers or non- developers to create a skill similar to “Fact of the Day”, “Joke of the Day”, “Flash Cards” etc. The template leverages AWS Lambda and the Alexa Skills Kit, while providing the business logic, use cases, error handling and help functions for your skill. You just need to come up with a fact idea (like “Food Facts”), plug in your fact list and edit the sample provided (we walk you through how it’s done). It's a valuable way to quickly learn the end-to-end process for building and publishing an Alexa skill.

Using the Alexa Skills Kit, you can build an application that can receive and respond to voice requests made on the Alexa platform. In this tutorial, you’ll build a web service to handle notifications from Alexa and map this service to a Skill in the Amazon Developer Portal, making it available on your device and to all Alexa users after certification.

After completing this tutorial, you'll know how to do the following:
* **Create a fact-based skill** - This tutorial will walk first-time Alexa skills developers through all the required steps involved in creating a fact based skill using a template called ‘SpaceGeek’.
* **Understand the basics of VUI design** - Creating this skill will help you understand the basics of creating a working Voice User Interface (VUI) while using a cut/paste approach to development. You will learn by doing, and end up with a published Alexa skill. This tutorial includes instructions on how to customize the skill and submit for certification. For guidance on designing a voice experience with Alexa you can also [watch this video](https://goto.webcasts.com/starthere.jsp?ei=1087592).
* **Use JavaScript/Node.js and the Alexa Skills Kit to create a skill** - You will use the template as a guide but the customization is up to you. For more background information on using the Alexa Skills Kit please [watch this video](https://goto.webcasts.com/starthere.jsp?ei=1087595).         
* **Get your skill published** - Once you have completed your skill, this tutorial will guide you through testing your skill and sending your skill through the certification process for making it available to be enabled by any Alexa user.

## Let’s Get Started
First, **[Download the code](https://github.com/amzn/alexa-skills-kit-js/blob/master/samples/spaceGeek/FactSkillTemplate/FactSkillTemplate.zip)** and then follow the instructions below. On GitHub, click “View Raw” to download the zip file.

### Step 1 – Create an AWS Account
1. Open **[aws.amazon.com](http://aws.amazon.com)** and then choose **‘Create a Free Account’**
   a. Follow the online instructions. Do not worry about the IAM role, we will do that later.
   
   b. You will need a Valid Credit Card to set up your account (note the **AWS Free Tier** will suffice however. You can find out more about the free tier here.)
   
   c. Part of the sign-up procedure involves receiving a phone call and entering a PIN using the phone keypad.
   
2. Sign in to your Console
   
 a. It can sometimes take a couple minutes for your new AWS account to go live. You will receive an e-mail when your account is active.

### Step 2 – Create a Lambda Function
AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability.

Note: If you are new to Lambda and would like more information, visit the [Lambda Getting Started guide](http://docs.aws.amazon.com/lambda/latest/dg/getting-started.html).

1. **IMPORTANT**: Select **US East (N. Virginia)** region (upper right). This is the only region that currently supports Alexa Skill development. If you do not select the correct region, it will not work.

   
2. Select **Lambda** from Compute services (upper left)
 
3. Select **“Create a Lambda Function”** to begin the process of defining your Lambda function.

4. At the bottom of the **‘Select Blueprint’** page, select **“Skip”**

5. You should be in ‘Configure Function’
 a. Enter the **Name**, **Description**, and **Runtime** for your skill as in the example.
 
6. Select the **‘Code Entry Type’** as **‘Upload Zip File’** and upload the zip file containing the example. Here’s the [link](https://github.com/amzn/alexa-skills-kit-js/blob/master/samples/spaceGeek/FactSkillTemplate/FactSkillTemplate.zip) again for reference, you will need to click on “View Raw” to download.

7. Set your handler and role as follows: 
    a. Keep Handler as ‘index.handler’
    b. Drop down the “Role” menu and select **“* Basic execution role”**. (Note: if you have already used Lambda you may already have a ‘lambda_basic_execution’ role created that you can use.) This will launch a new tab in the IAM Management Console.
    c. You will be asked to set up your Identity and Access Management or “IAM” role if you have not done so. AWS Identity and Access Management (IAM) enables you to securely control access to AWS services and resources for your users. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources. We need to create a role that allows our skill to invoke this Lambda function.
  
8. Accept the defaults to create a new IAM Role with a role name of lambda_basic_execution. Select “Allow” in the lower right corner and you will be returned to your Lambda function.

9. Keep the Advanced settings as default. Select ‘Next’ and review. You should see something like below. Then select ‘Create Function’:

10. Next we need to create an Event source. Event sources publish events that cause the Lambda function to be invoked. Upon invocation, AWS Lambda executes your code by passing the event to the handler in your Lambda function code. You associate an event source with your Lambda function using an event source mapping. We will use the Alexa Skills Kit event source and map it to this function.
    a. In your Lambda function tabs, select **‘Event Sources’**

    b. Select **‘Add event source’**
    
    c. Select **‘Alexa Skill Kit’** from the dropdown:
    
    d. You should see the confirmation of creation of the free tier event source **“Alexa Skills Kit”**:
    
    e. Keep this tab open as you will need to copy the ARN for your Lambda function for use in the developer portal. You can find your ARN at the top right corner of the function page:
 
### Step 3 – Set-up Your Alexa Skill in the Developer Portal
Skills are managed through the Amazon Developer Portal. You’ll link the Lambda function you created above to a Skill defined in the Developer Portal.

1. Open a new tab and go to the Developer Portal. Sign in or create a free account (upper right). You might see a different image if you have registered already or our page may have changed. If you see a similar menu and the ability to create an account or sign in, you are in the right place.
  2. Once you’ve signed in, navigate to Apps & Services
 3. Then select Alexa. You can also bookmark this page for future reference https://developer.amazon.com/edw/home.html#/skills/
 
 4. Choose Alexa Skills Kit:
 5. Here is where you will define and manage your skill. Select “Add New Skill”:
 6. Add the name of the skill. You can use “My Fact Skill” for this example. Remember, when you create a skill that you will publish, you will use a name that you define for your skill. That name will be the one that shows up in the Alexa App.
7. Add the invocation name. Since we are using the sample, type “space geek”
 8. Add the ARN from the Lambda function you created in the AWS Console earlier. Select the Lambda ARN (Amazon Resource Name) radio button.
a) You should still have that browser tab open. In the AWS Management Console, copy the ARN in the upper right corner.
 b) Paste the ARN into the Endpoint field. Here’s an example:
 9. Select Next.
10. Now we need to define our skill’s interaction model. Let’s begin with the intent schema. In the context of Alexa, an intent represents an action that fulfills a user’s spoken request. Intents can optionally have arguments called slots. We will not be using custom slots in this template, but they are very useful if you want to parameterize your intents.
a) Review the Intent Schema below. This is written in JSON and provides the information needed to map the intents we want to handle programmatically. Copy this from the intent schema in the Github repository here.
Below you will see the intents for getting a new fact, and then a collection of built-in intents to simplify handling common user tasks. Help intent will handle any time the user asks for help, stop and cancel are built-in intents to make it easier for you to handle when a user wants to exit the application. For more on the use of built-in intents, go here.
{
"intents": [
{
"intent": "GetNewFactIntent"
}, {
"intent": "AMAZON.HelpIntent" },
{
"intent": "AMAZON.StopIntent"
}, {
"intent": "AMAZON.CancelIntent" }
] }
   
11. The next step is to build the utterance list.
Given the flexibility and variation of spoken language in the real world, there will often be many different ways to express the same request. Providing these different phrases in your sample utterances will help improve voice recognition for the abilities you add to Alexa. It is important to include as wide a range of representative samples as you can -– all the phrases that you can think of that are possible in use (though do not include samples that users will never speak). Alexa also attempts to generalize based on the samples you provide to interpret spoken phrases that differ in minor ways from the samples specified.
a. Now its time to add the Utterances. Copy/paste the sample utterances from github. An example of utterances is listed below. Once they are copied, the screen should look similar to the following image:
12. Select Save. You should see the interaction model being built (this make a take a minute or 2). If you select next, your changes will be saved and you will go directly to the test screen. After selecting Save, it should now look like this:
  
 13. Select Next, and you will be taken to the Configuration screen. Select “No” for account linking and Next to move to the Test screen.
 14. You have now completed the initial development of your skill. You should see a screen that looks like this.
## We are now ready to test.
15. In the Test area, we are going to enter a sample utterance in the service simulator section and see how Alexa will respond. In this example, we have called the skill ‘Space Geek’. This is the ‘Invocation Name’ we set up on the Skill Information line in the “Skill Information” section.
a) In the Service Simulator, type ‘open Space Geek’ and select “Ask My Fact Skill”.
 b) You should see the formatted JSON request from the Alexa Service and the response coming back. Verify that you get a correct Lambda response, and notice the card output. You will want to customize this output later.
 c) (Optional) Testing with your device. This is optional as you can do all the testing in the portal. Assuming your Echo device is on-line (and logged in with the same account as your developer account), you should now see your skill enabled in the Alexa app and ask Alexa to launch your skill. For more information on testing an Alexa skill and registering an Alexa-enabled device, check here
  * Not working (getting an invalid response)?
• Do you have the right ARN copied from your Lambda function into your Developer Portal / Skill?
• Are you calling the right invocation name?
o Are you saying launch, start or open?
o Are you sure you have no other skills in your accounts with the same invocation
name?
• For this template specifically, you should have a minimum of 20 facts for a good
customer experience.

### Step 4 – Make it Yours
1. In the Skill Information section in the Developer Console, edit the Skill Information Tab to reflect your new Fact Skill:
b. Provide a skill name that represents the new skill you are creating.
c. Come up with a cool Invocation Name that users will use to invoke your skill d. Create a fun icon. Be sure you have the rights to whatever icons you are
uploading – you will need to provide both 108x108px and 512x512px images. Need help finding an image, see PixelBay as a possible source for royalty-free images. Use an image editor (such as Paint on Windows or Preview on Mac to change the size of the image.
e. Everything else can stay as-is for now in the Developer Portal
2. Open the source file for your Lambda function, index.js, in an editor of your choice. The zip file was downloaded in an earlier step or you can find it here. You will see on line 25 the definition of the facts used in the SpaceGeek example. These are the strings you will want to edit to customize this fact for your use.
  
 3. Edit the name of the array. Change the name SPACE_FACTS to something that represents your fact type. Then use “Find” to locate the other instances of SPACE_FACTS in the code and rename them as well.
4. Edit the strings to contain what ever facts or information you would like to make randomly available when a user invokes your skill. A few suggestions:
a) Only change the text between the double quotes. These are your facts.
b) Ensure you don’t accidentally delete and quotes or commas. You can always go
back to GitHub and copy it again if you make a mistake.
c) The skill uses a mathematical randomization on your list of facts. It is a good idea
to have at least 20, but more like 100, facts in the skill to ensure that the facts do not repeat too quickly. Also remember that because it is random, it is possible that the same fact can be repeated twice.
d) For extra credit and completely optional- If you would like to ensure that the facts don’t repeat (for a “Daily Fact Skill” for example), you can use a datastore like DynamoDB to store an id that you can check when the user accesses the skill and iterate through the facts. For more information on using DynamoDB with Lambda, go here.
 
5. You will also want to make sure to change the “Space Geek” references to the name of your skill. You don’t have to edit them all, but the following reference changes are required for certification.
a) Find this code in the HelpIntent, and change Space Geek to your custom fact name:
  "AMAZON.HelpIntent": function (intent, session, response) {
          response.ask("You can ask Space Geek tell me a
  space fact, or, you can say exit... What can I help you
  with?", "What can I help you with?");
b) Find the HandleNewFactRequest function, and change the highlighted references to your custom fact name. By now, the SPACE_FACTS array should have already been renamed:
  function handleNewFactRequest(response) {
      // Get a random space fact from the space facts list
      var factIndex = Math.floor(Math.random() *
  SPACE_FACTS.length);
      var fact = SPACE_FACTS[factIndex];
      // Create speech output
      var speechOutput = "Here's your space fact: " + fact;
      response.tellWithCard(speechOutput, "SpaceGeek",
  speechOutput);
}
   c) Optionally, you can change the console log output to have the custom name as well. Look for the following code, and change SpaceGeek to your custom fact name.
       console.log("SpaceGeek
 6. In order to control who accesses your web service, we should validate the application id in requests made to your web service. Let’s go back to your Alexa skill in your
Developer Portal for a moment. Copy in your Application ID from the ‘Skill Information’ section in your developer portal / skill and copy it into your Lambda function.
 8. In your AWS lambda function, in the index.js file, find the applicationId section and copy YOUR Application ID into the section indicated, notice the quotes. (do not copy the ID below, which is just an example). It looks something like this when you are done: (be sure to SAVE)
// Route the incoming request based on type (LaunchRequest, IntentRequest,
// etc.) The JSON body of the request is provided in the event parameter. exports.handler = function (event, context) {
try {
console.log("event.session.application.applicationId=" + event.session.application.applicationId);
/**
* Uncomment this if statement and populate with your skill's application ID to
* prevent someone else from configuring a skill that sends requests to this function.
*/
if (event.session.application.applicationId !== "amzn1.echo-sdk- ams.app.8b7e6904-f4f1-4715-b2df-a8c0a9583acd") {
   
context.fail("Invalid Application ID"); }
9. A minimum of 20 facts is needed to get started, about 100 is a good number to keep users engaged. The more the better.
10. Be sure to select SAVE when you are all done. Note: we test in the Developer Portal, not in our Lambda function (AWS).
11. Log back into your AWS console and upload the changes you have just made. First you will need to zip up the files into a new archive. You can do this by selecting the 2 files that you need (AlexaSkill.js and your updated index.js) into a new archive. Be sure that those are the only 2 files in your archive file. Here is an example of what this looks like on a Mac, but the context menu on Windows also provides a similar option for creating a compressed file.
On a Mac:
On Windows:
 
 12. Select your Lambda function and on the Code tab, select “Upload” to add the archive you just created.
 13. Once you have successfully added the file you will see it on the screen, then select “Save”:
 14. Repeat the tests you performed earlier to ensure your changes are functioning properly. See step 12 for a review of how to performs functional tests. We will not be submitting to certification until we have customized this skill.
 
### Step 5 – Publish Your Skill
Now we need to go back to our Developer Portal to test and edit our skill and we will be ready for certification.
1. In your skills Test section, enter your Utterances into the Simulator to make sure everything is working with your new facts.
2. Optionally, you can test with your Alexa-enabled device to make sure everything is working correctly. You may find a few words that need to be changed for a better user experience.
Some things to think about:
* Does every fact sound correct? Do you need to change any words to make them sound correct? Because we are randomizing our facts, this could take a while. Instead, you can use the Voice Simulator in the Test section to simulate Alexa’s responses. In the Voice Simulator, type in each fact that you are using to test how Alexa will say it. Use additional punctuation or possibly SSML if you need to better control how Alexa responds. You can find out more about SSML here.
* Have you added in YOUR ApplicationID as per the previous instruction?
3. Select the Description area of your skill next:
  
a) Spend some time coming up with an enticing, succinct description. This is the only place you have to attract new users. These descriptions show up on the list of skills available in the Alexa app.
b) In your example phrases, be sure that the examples you use match the utterances that your created in the Interaction Model section. Remember, there are built-in intents such as help and cancel. You can learn more about built-in intents here. You can also find a list of supported phrases to begin a conversation here.
c) Be sure you have the rights to whatever icons you are uploading – you will need to provide both 108x108px and 512x512px images. If there is any question the Amazon certification team will fail your Alexa skill submission.
     4. Once you have uploaded your icons, you should see a success message at the bottom of the screen.
5. IMPORTANT: Add the text “This is based on the Fact Skill Template” to the Testing Instructions section. This alerts the Certification team of your submission using this standardized template, smoothing the road to a faster publish. Finally, select Next.
 6. Privacy and Compliance.
a. On the Privacy and Compliance section, select ‘No’ for spending real money and
collecting personal information. Privacy and Terms URL’s are optional. Choose to certify that your skill can be imported to and exported from the US.
 b. Select “Save”.
 c. Select “Submit for Certification”
 d. Finally, confirm your submission. Select “Yes” to submit your skill.
 
Congratulations! You have published a new skill. You will receive progress e-mails and possibly other suggestions from the team on how you can make your skill even better. You can update your skills at any time.
Get Started Today
Check out these Alexa developer resources:
Alexa Skills Kit (ASK)
Alexa Developer Forums
Knowledge Base
Intro to Alexa Skills Kit - On Demand Webinar Voice Design 101 - On Demand Webinar Developer Office Hours
      