+++
title = "How Webhooks are tested"
date = "2024-05-13"
author = "Rahul"
+++

## Introduction

If you've ever developed a webhook then you'd know what a pain they are to test, redeploying every time you make a change hardly seems efficient or fun so how would you test it?.

To test a webhook you would want to use a tool known as a webhook tester (shocking, I know) but have you ever wondered how they work? if you have, this is the post for you.

## How it's actually done

{{<figure src="/img/WebhookTesterArchitecture.png" alt="Whoops" position="center" style="border-radius: 8px;" caption="General Webhook Tester Architecture" captionPosition="center" captionStyle="color: black;" >}}

As you can see from the diagram the tester consists of two main components:

1. The Client CLI
2. The Server Component

The way these two work together is as follows:

1. The user sets up the webhook to be tested and gives the CLI it's port number as an argument.
2. The CLI sends a websocket request to the server asking it to generate a random subdomain.
3. The server sends over the new subdomain link to the CLI which is used as the webhook link which is provided to the platform the webhook is being developed for.
4. The external platform sends a request to the link provided which is recieved by the server.
5. The server then forwards this request to the CLI over the open websocket.
6. The CLI forwards this request to the webhook being tested.

And voila! just like that we've successfully set up a test platform for our webhook.

## Tools to test webhooks

There are several different tools to test webhooks the most popular of which is ngrok and possibly postman as well. That said I've made my own tool as well which you can find [**here**](https://github.com/nznznz42/Captain-Hook).

I've written this tool so you don't really need to deploy a server component if you don't want to, as long as you have an example payload from the platform you're building the webhook for you can test it completely locally and it randomises the payload values if you so wish. However if you'd Like to do it the usual way and deploy the server component you can find it [**here**](https://github.com/nznznz42/Captain-Hook-Server)
