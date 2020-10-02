# Chat Feature Design Document
## Overview
The chat feature is meant to allow insider and seeker to establish a conversation within the website. This document explains the data structure that is responsible of holding the chat data. This document also provides details of supported APIs.
## Data Structure
Each matchedcase document will have a property called conversation which will contain the chat data. A conversation should contain an array of message object. Each message object would then contain timestamp, author, and content. An example is shown below
    
    {
        _id: match case id,
        seekerId: seeker id,
        insiderId: insider id,
        matchId: match id,
        createTime: create timestamp,
        status: case status,
        referrals: referral[],
        interview: interview[],
        conversation: [
            {
                createdAt: when was this message created,
                author: who created this message,
                content: message body
            },
            {
                createdAt: when was this message created,
                author: who created this message,
                content: message body
            },
            ...
        ]
    }
## Supported APIs

* ### **POST: /conversation**

    **Request body:**

        {
            caseId: case id,
            author: who created this message? insider/seeker,
            content: message content,
            createdAt: timestamp
        }
    
    **Response:**

    201 if success, 400 if fail

    **Description:**

    This api creates a message and attach to a match case based on the case id.

* ### **GET: /conversation/caseId**

    **Request parameters:**
    * numOfMessages: number

        required, how many messages do you want
    * timeStamp: timestamp

        required, this is for pagination purpose. use "" if you just want latest messages, use a timestamp if you want messages newer than that timestamp

    **Response:**

        {
            [
                {
                    author: who created this message,
                    content: message content,
                    createdAt: timestamp,
                },
                {
                    author: who created this message,
                    content: message content,
                    createdAt: timestamp,
                },
                ...
            ]
        }
    
    **Description:**

    This api allows you to retrieve messages by caseId.

* ### **DELETE: /conversation/caseId**

    **Response:**

    200 if success, 400 if fail