# AWS Lambda function for Alexa (NeoPixels)

A simple [AWS Lambda](http://aws.amazon.com/lambda) function that demonstrates how to write a skill for the Amazon Echo using the Alexa SDK

## Working demo video

Check out the demo on Youtube:

![Picture of my tree](https://pbs.twimg.com/media/CySuTgDXgAAAuM6.jpg:large)

[https://www.youtube.com/watch?v=u4aIFOdGP2k&index=5&list=PLlIapFDp305CPJ3dKNb_mh0vqMz865oXT](https://www.youtube.com/watch?v=u4aIFOdGP2k&index=5&list=PLlIapFDp305CPJ3dKNb_mh0vqMz865oXT)

## Quick overview:

* Follow this guide replacing "Hello World" for "Christmas Tree"

* Configure your blinkt and run this code on the Pi: [mqtt.py](https://github.com/pimoroni/blinkt/blob/master/examples/mqtt.py)

This Alexa skill works by sending an MQTT signal to iot.eclipse.org - the Raspberry Pi runs an MQTT subscription to a channel (topic) and decodes the incoming string as JSON to decide whether to change brightness or set a colour.

## Build details:

NeoPixel string plugs in on pin 18 of the Raspberry Pi via (DIN). Then connect 5v and GND.

* Tree is from Wilkos £4
* Plate is from Wilkos £2.50
* 3x jumper wires
* 1x Pi Zero
* 1x NeoPixel string - 1m with 60 LEDs

> With 60 LEDs at 100% brightness this draws around 0.85A, which should be OK without additional electronics and a quality 5v power supply for the Pi.

**Phrases:**

* Alexa tell Christmas Tree [to] change to red/green/blue
* Alexa tell Christmas Tree to turn off
* Alexa tell Christmas Tree to set brightness to 60 percent

## Setup
To run this example skill you need to do two things. The first is to deploy the example code in lambda, and the second is to configure the Alexa skill to use Lambda.

### AWS Lambda Setup
1. Go to the AWS Console and click on the Lambda link. Note: ensure you are in us-east or you won't be able to use Alexa with Lambda.
2. Click on the Create a Lambda Function or Get Started Now button.
3. Skip the blueprint
4. Name the Lambda Function "Hello-World-Example-Skill".
5. Select the runtime as Node.js
5. Go to the the src directory, select all files and then create a zip file, make sure the zip file does not contain the src directory itself, otherwise Lambda function will not work.
6. Select Code entry type as "Upload a .ZIP file" and then upload the .zip file to the Lambda
7. Keep the Handler as index.handler (this refers to the main js file in the zip).
8. Create a basic execution role and click create.
9. Leave the Advanced settings as the defaults.
10. Click "Next" and review the settings then click "Create Function"
11. Click the "Event Sources" tab and select "Add event source"
12. Set the Event Source type as Alexa Skills kit and Enable it now. Click Submit.
13. Copy the ARN from the top right to be used later in the Alexa Skill Setup

### Alexa Skill Setup
1. Go to the [Alexa Console](https://developer.amazon.com/edw/home.html) and click Add a New Skill.
2. Set "HelloWorld" as the skill name and "hello world" as the invocation name, this is what is used to activate your skill. For example you would say: "Alexa, tell Hello World to say hello"
3. Select the Lambda ARN for the skill Endpoint and paste the ARN copied from above. Click Next.
4. Copy the Intent Schema from the included IntentSchema.json.
5. Copy the Sample Utterances from the included SampleUtterances.txt. Click Next.
6. [optional] go back to the skill Information tab and copy the appId. Paste the appId into the index.js file for the variable APP_ID,
   then update the lambda source zip file with this change and upload to lambda again, this step makes sure the lambda function only serves request from authorized source.
7. You are now able to start testing your sample skill! You should be able to go to the [Echo webpage](http://echo.amazon.com/#skills) and see your skill enabled.
8. In order to test it, try to say some of the Sample Utterances from the Examples section below.
9. Your skill is now saved and once you are finished testing you can continue to publish your skill.

## Examples
    User: "Alexa, tell Hello World to say hello"
    Alexa: "Hello World!"
