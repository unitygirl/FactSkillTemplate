# FactSkillTemplate
Template for buidling a fact-based skill for Alexa

After completing this tutorial, you'll know how to do the following:

*	<b>Create a fact-based skill</b> - This tutorial will walk first-time Alexa skills developers through all the required the steps involved in creating a skill using the fact skill template, called ‘SpaceGeek’. 
*	<b>Understand the basics of VUI design</b> - Creating this skill will help you understand the basics of creating a working Voice User Interface (VUI) while using a cut/paste approach to development. You will learn by doing, and end up with a published Alexa skill. This tutorial includes instructions on how to customize the skill and submit for certification. For guidance on designing a voice experience with Alexa you can also watch this video.
*	<b>Use JavaScript/Node.js and the Alexa Skills Kit to create a skill</b> - You will use the template as a guide but the customization is up to you. For more background information on using the Alexa Skills Kit please watch this video. 
*	<b> Get your skill published </b>- Once you have completed your skill, this tutorial will guide you through testing your skill and sending your skill through the certification process for making it available to be enabled by any Alexa user.


Remember, the more facts you add, the more compelling your experience will be for customers. We recommend a minimum of 20, but at least 100 is best for user engagement.


#Let's Get Started
First download the script and then follow the instructions below. Be sure you have the fact skill template, "SpaceGeek" set up properly before you move on to customizing it to your set of facts. 
</br>

<b>Step #1 – Create an AWS Account</b>
	1.	Open aws.amazon.com and then choose ‘Create an Free AWS Account’ 
		a.	Follow the online instructions. Do not worry about the IAM role, we will do that later.
		b.	You will need a Valid Credit Card to set up your account (note this is a free tier however)
		c.	Part of the sign-up procedure involves receiving a phone call and entering a PIN using the phone keypad.
	2.	Sign in to your Console 
		a.	It can sometimes take while for your new AWS account to go live. You will receive an e-mail when your account is active.
	</br>
<b>Step #2 – Create a Lambda Function</b>
	1. Select US East (N. Virginia) region (upper right)</br>
	![Alt text](/path/to/selectRegion.jpg)
	2. Select Lambda from Compute services (upper left) <br>
	![Alt text](/path/to/selectRegion.jpg)<br>
	3. Skip ‘Select Blueprint’<br>
	4.You should be in ‘Configure Function’
		a. Enter the Name/Description/Runtime for your skill as in the example  
	5. Select the ‘Code Entry Type’ as ‘Edit code inline’ and copy/paste the Lambda function code   node.js script  you downloaded at the beginning. Here’s the link again for reference. It should look like this:
	Note – the AWS Lambda inline code editor is limited in size and you may hit the cap (currently 20KB) while creating your skill. We reccommend that you package the code (and any dependent libraries) as a ZIP and upload it using the AWS CLI from your local environment, or specify an Amazon S3 location where the ZIP file is located. Uploads must be no larger than 50MB (compressed). Visit the Lambda Getting Started guide to get started.
	6. Set your handler and role as follows:
		a.   Keep Handler as ‘index.handler’
		b.   Add a new role for ‘lambda_basic_execution’  (note IAM role in next step. Note also if you have already used Lambda you may already have a ‘lambda_basic_execution’ role created you can use.
	7.   You will be asked to set up your IAM role if you have not done so.
	8.   Keep the Advanced settings as default
		a.   Select ‘Next’ and review. You should see something like below. Then ‘Create your Function’:
	9.   Next we need to create an Event source
		a.   In your Lambda function tabs, select ‘Event Source’
	10.   Select ‘Add event source’
		a.   Select type as ‘Alexa Skill Kit’
	11.   You should see the following free tier event source:
	12.   Copy the ARN for your Lambda function. You will need it for setting up your skill in the Developer Portal. You can find your ARN here:
	<b>Step #3 – Set-up Your Skill in the Developer Portal</b>
	1.	Sign in or create a free account on the Developer Portal (upper right)
	2.	Once you’ve signed in, navigate to Apps& Services/Alexa/Alexa Skills Kit in the post-login experience
	3. This is where your skill will be defined and managed
	Select add new skill and add your name/invocation name/version and your ARN endpoint. Example here:
	a.	Select Save and Next
	a.	We need to define our skill’s interaction model. 
	i.	Copy/paste the following Intent Schema
	{
	  "intents": [
	    {
	      "intent": "AnswerIntent",
	      "slots": [
	        {
	          "name": "Answer",
	          "type": "LIST_OF_ANSWERS"
	        }
	      ]
	    },
	        {
	      "intent": "AnswerOnlyIntent",
	      "slots": [
	        {
	          "name": "Answer",
	          "type": "LIST_OF_ANSWERS"
	        }
	      ]
	    },
	    {
	      "intent": "AMAZON.StartOverIntent"
	    },
	    {
	      "intent": "AMAZON.RepeatIntent"
	    },
	    {
	      "intent": "AMAZON.HelpIntent"
	    },
	    {
	      "intent": "AMAZON.StopIntent"
	    },
	    {
	      "intent": "AMAZON.CancelIntent"
	    }
	  ]
	}
	i.	Add Slot Type as below screenshot:

	i.	Add the Utterances 
	1.	Copy/paste the following:
	AnswerIntent the answer is {Answer}
	AnswerIntent my answer is {Answer}
	AnswerIntent is it {Answer}
	AnswerIntent {Answer} is my answer
	AnswerOnlyIntent {Answer}
	 
	AMAZON.StartOverIntent start game
	AMAZON.StartOverIntent new game
	AMAZON.StartOverIntent start
	AMAZON.StartOverIntent start new game
	4.   Select save. You should see the model being built (this make a take a minute or 2)
	a.   It should now look like this:

	b.   Select Next
	5.   We are ready to test!
	a.	In the Test tab, we are going to enter a sample utterance in the service simulator tab. 
	i.	In this example, we have called the skill ‘reindeer games.’ This is the ‘Invocation Name’ we set up on the Skill Information line in step #2.
	ii.	Enter ‘open reindeer games’ and select Ask.
	iii.	You should see the formatted JSON request from the Alexa Service and the response coming back.
	iv.	Assuming your Echo device is on-line (and logged in with the same account as your developer account), you should now see your skill enabled in the Alexa Companion app and ask Alexa to launch your skill!

	                * Not working (invalid response)?
	o	Do you have the right ARN copied from your Lambda function into your Developer Portal / Skill?
	o	Are you calling the right invocation name? 
	o	Are you saying launch, start or open?
	o	Are you sure you have NO other skills in your accounts with the same invocation name?
	o	For this template specifically, you need to have a minimum of 7 questions/answers for the business logic to function.
	Step #4 – Make it Yours
	1.   Edit the Skill Information to reflect your new trivia Game
	a.	A new Name
	b.	A cool Invocation Name
	c.	A fun icon
	d.	Everything else can stay as-is for now in the Developer Portal
	2.   Log back into your AWS console and edit the Trivia Game Function you have already created. We are going to copy in your new trivia game questions and answers.
	a.	As we have elected to edit our code in-line, you just need to edit the questions and answers JSON to reflect your trivia game. A few suggestions: 
	i.	Note than the format calls for one question and 4 answers for each question. The first answer is the correct answer. The script logic takes care of randomizing the questions and answers for you.

	3.   Back to your Developer Portal / Skill for a moment. Copy in your Application ID from the ‘Skill Information’ tab in your developer portal / skill into your Lambda script.

	In your AWS lambda function find the applicationId section and copy YOUR Application ID into the section indicated (do not copy the ID below, which is just an example). It looks something like this when you are done: (be sure to SAVE)
	// Route the incoming request based on type (LaunchRequest, IntentRequest,
	// etc.) The JSON body of the request is provided in the event parameter.
	exports.handler = function (event, context) {
	    try {
	        console.log("event.session.application.applicationId=" + event.session.application.applicationId);
	 
	        /**
	         * Uncomment this if statement and populate with your skill's application ID to
	         * prevent someone else from configuring a skill that sends requests to this function.
	         */
	 
	         if (event.session.application.applicationId !== "amzn1.echo-sdk-ams.app. amzn1.echo-sdk-ams.app.05aebcb3-1461-48fb-a008-8ddccd1e2b516") {
	         context.fail("Invalid Application ID");
	         }
	4.   Be sure to remove any Reindeer questions (kind of goes without saying)
	5.   A minimum of 20 questions is needed to get started, about 100 is a good number to keep users engaged. The more the better.
	6.   Be sure to select SAVE when you are all done. Note we test in the Developer Portal, not in our Lambda function (AWS).
	7.   Now we need to go back to our Developer Portal to test and edit our skill and we will be GO for certification.
	a.   In your skills Test tab, enter your Utterances to make sure everything is working with your new questions and answers.
	b.   Go ahead and test with your Alexa-enabled device to make sure everything sounds right, you may find a few words that need to be changed for a better user experience. 
	<IMPORTANT> 
	We recommend actually running your skill on an Echo device and testing every intent and question. We do this as part of the certification process and you will FAIL certification if there are any issues.
	    * Does ever question and answer sound correct? Do you need to change any words to make them sound correct?
	    *   Have you added in YOUR ApplicationID as per the previous instruction?
	c.   Select the Description tab next
	i.  Spend some time coming up with an enticing, succinct description. This is the only place you have to attract new users. These descriptions show up on the Companion Apps list of new skills available.
	ii.   Be sure you have the rights to whatever icons you are uploading – you will need to provide both 108x108px and 512x512px images. If there is any question the certification team will fail your submission.

	 
	8.   Select Save and SUBMIT FOR CERTIFICATION.
	a.    On your Publishing section select ‘No’ for Account linking, spend money and personal information. Privacy and Terms URL’s are optional.
	                b.    Note in your testing instructions that you are using the Trivia Game Template.
	c.   You will receive progress e-mails and possibly other suggestions from the team on how you can make your skill even better. You can update your skills at any time.

	
	
	