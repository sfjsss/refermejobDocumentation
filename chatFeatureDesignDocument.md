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
    * numOfmessages: number

        optional, how many messages do you want, if not included, give a default number of messages starting from the newest message
    * timeStamp: timestamp

        optional, this is for pagination purpose, if not included, give messages starting from the newest message, if included, give messages from this timestamp provided

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