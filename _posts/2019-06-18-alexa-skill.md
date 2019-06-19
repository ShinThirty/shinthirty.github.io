---
layout: post
title:  "Basic Concepts and Tools to Build an Alexa Skill"
date:   2019-06-18
categories: [note]
tags:   [alexa, alexa development]
---
<script src="https://unpkg.com/mermaid@8.0.0/dist/mermaid.min.js"></script>

## Alexa Skill Architecture

<div class="mermaid">
  graph LR
  Utterance --> Interaction_Model
  Interaction_Model --> Speechlet
  Utterance --> NLU
  NLU --> Alexa_Skill
  Utterance --> Super_Editorial
  Super_Editorial --> Alexa_Skill
  Utterance --> Understandable?
</div>

## Create an Alexa Skill

1. Create a new Alexa skill on [Amazon Developers](https://developer.amazon.com/);
2. Add an invocation name to the newly created Alexa skill;
3. Add intents to your Alexa skill;
4. Add slots to your Alexa skill;
5. You can also edit the detail information about the skill using the JSON editor;
6. Choose how you want to host the service for your Alexa skill: AWS Lambda function or a RESTful web service;

## BONES

The BONES CLI enables you to create a complete Native AWS service by answering a few questions. It does the heavy work of creating all of the resources you need and ties it together with a pipeline generated using LPT Synthesis. For more information, please check [BONES Templates and CLI](https://builderhub.corp.amazon.com/tools/bones/).

## SAMToolkit

**SAMToolkit**  is a  **community effort**  to build and maintain a set of tools and libraries for a delightful development and testing experience for serverless applications and services.
Click [here](https://w.amazon.com/bin/view/SAMToolkit/) for more details.

## How to Test Your Skill

Alexa skill can be tested on the Alexa Developer Console. Just click "Test" on the top of the webpage and start testing!
