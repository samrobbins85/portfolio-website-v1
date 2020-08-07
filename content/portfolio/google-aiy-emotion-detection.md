+++
categories = ["python"]
coders = []
date = 2020-08-01T23:00:00Z
description = "A device to detect if you are sad and send dog pictures"
github = ["https://github.com/samrobbins85/google-aiy-emotion"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1596387335/product_vision_1x-removebg_ggmlzk.png"
title = "Google AIY Emotion Detection"
type = ""
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1596387392/AIY_logo_blue_zabled.svg"
name = "Google AIY"
url = "https://aiyprojects.withgoogle.com/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793277/logos/logos_raspberry-pi_y4fqbh.svg"
name = "Raspberry Pi"
url = "https://www.raspberrypi.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793276/logos/logos_python_pjlesq.svg"
name = "Python"
url = "https://www.python.org/"
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1596387508/sendgrid-2_gygpj0.svg"
name = "SendGrid"
url = "https://sendgrid.com/"

+++
This project started with assembling the Google AIY Vision Kit, this was very enjoyable and gave me a good insight into what makes up the device.

This code is a fork of the Google example [face_camera_detection](https://github.com/google/aiyprojects-raspbian/blob/aiyprojects/src/examples/vision/face_detection_camera.py).

Building on top of this example, I created a counter, which allowed me to keep track of how consistently happy or sad the face in the frame is.

```python
if avg_joy_score(faces) > 0.8:
	if joy_counter < 0:
		joy_counter = 0
  else:
 		joy_counter += 1
if avg_joy_score(faces) < 0.1:
 	if joy_counter > 0:
 		joy_counter = 0
  else:
    joy_counter -= 1
if joy_counter > 20:
	print("Happy")
joy_counter = 0
```

## Sending Emails

The code for sending emails is nested under a conditional of `if joy_counter < -20` in a similar way to the Happy branch is defined above.

For sending emails, I first had to work with the Reddit API, this is fairly simple as adding `/random.json` to the end of a subreddit will give you a response with a random post from that subreddit. So I just used `urllib` to make a request in the following way

```python
request_url = urllib.request.urlopen("https://www.reddit.com/r/dogpictures/random.json")
```

Then it comes to parsing the response, as the URL to the image is deep in the JSON response. The `json` package works for this, with `result` being set as a string of the URL

```python
result = json.loads(request_url.read().decode())[0]["data"]["children"][0]["data"]["url"]
```

Then it comes to working with SendGrid, this is very simple with the `sendgrid` Python library

```python
message = Mail(
	from_email='contact@samrobbins.uk',
	to_emails='samrobbinsgb@gmail.com',
	subject='Sending with Twilio SendGrid is Fun',
	html_content='<img src='+result+'>')
	try:
		sg = SendGridAPIClient(env.str('SENDGRID_API_KEY'))
		response = sg.send(message)
		print(response.status_code)
	except Exception as e:
		print(e.message)
```

With those simple modifications, it will now send the image when you get sad.