---
layout: page
title: Attachments, Cards and Actions
permalink: /connector/message-actions/
weight: 206
parent1: Bot Connector
parent2: Messages
---

* TOC
{:toc}

Many messaging channels provide the ability to attach richer objects.  In the Bot Connector we map 
our attachment data structure to media attachments and rich cards on each channel.

# Image and File Attachments
To pass a simple attachment to a piece of content you add a simple attachment data structure with a link to the 
content. 

| Property | Description |
|-----|------|
| ContentType | mimetype/contenttype of the url |
| ContentUrl  | a link to the actual file |

If the content type is a image or media content type then it will be passed to the channel in a way that 
allows the image to be displayed.  If it is a file then it will simply come through as a link.

# Rich card attachments
We also have the ability to render rich cards as attachments.  

| Property | Description |
|-----|------|
| Title | Title of card|
| TitleLink | Link for the title |
| Text | Text of the card |
| ThumbnailUrl | image to put on the card|

You can send multiple rich card attachments in a single message.  On most channels they will be sent
as multiple rich cards, but some channels (like Facebook) will render them as a carosel of rich cards.

# Actions on attachments
An action is a representation of information that a user can use to take action.  On many channels
actions get mapped to buttons, while on other channels they simply become a list of options
displayed to the user.

Regardless, a user can perform the action by clicking on a button or typing in the content as a response.

> The Actions field requires you to upgrade to latest published Nuget package.

Action object:

| Property | Description |
|-----|------|
| title | label of the action (button) |
| message | message which will be sent for the user when they click the button |
| url | instead of a message when someone clicks on a button it should take them to a Url |
| image  | url to an image to put on the card (Not all channels will show an image) |

Channel support

| Channel | Behavior |
|-----|------|
| Facebook | turned into buttons. If more than 3 buttons multiple cards will be issued |
| Telegram | Turned into buttons |
| Kik | Turned into buttons |
| All others | Displayed as list of options |

# Example

{% highlight json %}
    {
        "type": "Message",
        "id": "LQR6NUF4kwv",
        "conversationId": "BlgBB8EPV4729VPDri3bHCCTFpdEN3CWB3Bn2kwAAA8fxA9Q",
        "created": "2016-05-03T21:46:18.8338576Z",
        "language": "en",
        "text": "Pick one:",
        "attachments": [
            {
                "actions": [
                    {
                        "title": "Willy's Cheeseburger",
                        "message": "CB"
                    },
                    {
                        "title": "Curley Fries",
                        "message": "F"
                    },
                    {
                        "title": "Chocolate Shake",
                        "message": "S"
                    }
                ]
            }
        ],
        "from": {... },
        "to": {...},
        "replyToMessageId": "5a6L8DCxLpH",
        "participants": [ ... ]
        "totalParticipants": 2,
        "mentions": [],
        "channelConversationId": "TestBot",
    }
{% endhighlight %}

![Example on facebook](/images/action_buttons.png)