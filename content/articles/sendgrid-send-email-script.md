---
title: "SendGrid Send Email Script"
date: 2023-01-18T19:05:42+05:30
draft: false
---

![sendgrid](../images/blog-sendgrid.png)
**Send EMAIL via SendGrid API using Shell Script**

We had a requirement to send the Emails via SendGrid using a shell script, SendGrid does expose their HTTP API's. Below are some cURL examples for several basic use cases to get you sending email through SendGrid's v3 Mail Send endpoint right away!

```bash
curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{"personalizations": [{"to": [{"email": "recipient@example.com"}]}],"from": {"email": "sendeexampexample@example.com"},"subject": "Hello, World!","content": [{"type": "text/plain", "value": "Heya!"}]}'
```

**Sending a Basic Email to Multiple Recipients**

```bash
curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{"personalizations": [{"to": [{"email": "recipient@example.com"}],"cc": [{"email":"recipient2@example.com"}, {"email": "recipient3@example.com"}, {"email":"recipient4@example.com"}]}], "from": {"email": "sendeexampexample@example.com"},"subject":"Hello, World!", "content": [{"type": "text/plain", "value": "Heya!"}]}'
```

**Sending a Basic Email Using a Template**
```bash
curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{"personalizations": [{"to": [{"email": "recipient@example.com"}]}],"from": {"email": "sendeexampexample@example.com"},"subject":"Hello, World!","content": [{"type": "text/plain","value": "Heya!"}], "template_id" : "YOUR_TEMPLATE_ID"}'
  ```

  **Sending a Basic Email with Attachment**
  ```bash
  curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{"personalizations": [{"to": [{"email": "recipient@example.com"}]}],"from": {"email": "sender@example.com"},"subject":"Hello, World!","content": [{"type": "text/html","value": "Hey,<br>Please find attachment."}], "attachments": [{"content": "BASE64_ENCODED_CONTENT", "type": "text/plain", "filename": "attachment.txt"}]}'
```

**Sending a Basic Email at a Scheduled Time**
```bash
curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{"personalizations": [{"to": [{"email": "recipient@example.com"}]}],"from": {"email": "sendeexampexample@example.com"},"subject":"Hello, World!","content": [{"type": "text/plain","value": "Heya!"}], "send_at" : UNIX_TIMESTAMP_HERE}'
  ```

Now, Let come to the interesting part, We had to write a script to send multiple attachments to multiple email ids, considering TO, CC and BCC. As you know, Building the JSON for the API Payload using the Shell Script is pretty complex.

Here is the script which you can use...

```bash
sh sendEmail.sh 
        -t 'to1@gmail.com;to2@gmail.com' 
        -c 'cc1@gmail.com;cc2@gmail.com' 
        -b 'bcc1@gmail.com;bcc2@gmail.com' 
        -s 'EMAIL SUBJECT' 
        -o 'Email body goes here' 
        -a '/tmp/test.sh;/tmp/test2.sh'
```

here is the code for your reference
```bash
#!/bin/bash
# Author: Amith Chandrappa

# Usage
# Options:
# 	-t: To Emails, Separated by ";"
# 	-c: CC Emails, Separated by ";"
# 	-b: BCC Emails, Separated by ";"
# 	-s: Subject
# 	-o: Email body
# 	-a: Attachment Files, Separated by ";"
#
#	Example: 
#	sh sendEmail.sh 
#		-t 'to1@gmail.com;to2@gmail.com' 
#		-c 'cc1@gmail.com;cc2@gmail.com' 
#		-b 'bcc1@gmail.com;bcc2@gmail.com' 
#		-s 'FINAL SCRIPT' 
#		-o '<p>Email body goes here</p>' 
#		-a '/tmp/test.sh;/tmp/test2.sh'

# Your Sendgrid API Key
SENDGRID_API_KEY="<YOUR API KEY>"

FROM_NAME="<FROM NAME>"
FROM_EMAIL="<FROM EMAIL ADDRESS>"

# Get the arguments
while getopts t:c:b:s:o:a: flag
do
    case "${flag}" in
        t) to=${OPTARG};;
        c) cc=${OPTARG};;
        b) bcc=${OPTARG};;
		s) subject=${OPTARG};;
		o) body=${OPTARG};;
		a) attachments=${OPTARG};;
    esac
done


# Start building the JSON
sendGridJson="{\"personalizations\": [{";

# Convert the String to Array, with the delimiter as ";"
IFS='; ' read -r -a to_array <<< "$to"
IFS='; ' read -r -a cc_array <<< "$cc"
IFS='; ' read -r -a bcc_array <<< "$bcc"
IFS='; ' read -r -a attachments_array <<< "$attachments"


if [ ${#to_array[@]} != 0 ] 
then
	sendGridJson="${sendGridJson} \"to\": ["
	
	for email in "${to_array[@]}"
	do
	    sendGridJson="${sendGridJson} {\"email\": \"$email\"},"
	done

	sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	sendGridJson="${sendGridJson} ],"

	if [ ${#cc_array[@]} == 0 ] && [ ${#bcc_array[@]} == 0 ] 
	then
		sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	fi
fi

if [ ${#cc_array[@]} != 0 ] 
then
	sendGridJson="${sendGridJson} \"cc\": ["
	
	for email in "${cc_array[@]}"
	do
	    sendGridJson="${sendGridJson} {\"email\": \"$email\"},"
	done

	sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	sendGridJson="${sendGridJson} ],"

	if [ ${#bcc_array[@]} == 0 ] 
	then
		sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	fi
fi

if [ ${#bcc_array[@]} != 0 ] 
then
	sendGridJson="${sendGridJson} \"bcc\": ["
	
	for email in "${bcc_array[@]}"
	do
	    sendGridJson="${sendGridJson} {\"email\": \"$email\"},"
	done

	sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	sendGridJson="${sendGridJson} ]"
fi

sendGridJson="${sendGridJson} }],\"from\": {\"email\": \"${FROM_EMAIL}\",\"name\": \"${FROM_NAME}\"},\"subject\":\"${subject}\",\"content\": [{\"type\": \"text/html\",\"value\": \"${body}\"}],"

if [ ${#attachments_array[@]} != 0 ] 
then
	sendGridJson="${sendGridJson} \"attachments\": ["
	
	for attachment in "${attachments_array[@]}"

	# Converting the File Content to Base64
	# For OSX use base64 <fileName>
	# For linux use base64 -w 0 <fileName>

	do
		base64_content=$(base64 -w 0${attachment})
		fileName="$(basename $attachment)"
	    sendGridJson="${sendGridJson} {\"content\": \"${base64_content}\",\"type\": \"text/plain\",\"filename\": \"${fileName}\"},"
	done

	sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
	sendGridJson="${sendGridJson} ]"
else
	sendGridJson=`echo ${sendGridJson} | sed 's/.$//'`
fi

sendGridJson="${sendGridJson} }"

#Generate a Random File to hole the POST data
tfile=$(mktemp /tmp/sendgrid.XXXXXXXXX)
echo $sendGridJson > $tfile

# Send the http request to SendGrid
curl --request POST \
  --url https://api.sendgrid.com/v3/mail/send \
  --header 'Authorization: Bearer '$SENDGRID_API_KEY \
  --header 'Content-Type: application/json' \
  --data @$tfile
```