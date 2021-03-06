# Skills

## Intro to Skills Pieces

### Consuming Skills
![MultipleBotsConsumeSkills](./SkillsOverview/MultipleBotsConsumeSkills.svg "Multiple Bots Consume Skills")

* A *root bot* can consume many *skills*
* A *skill* can be consumed by many *bots*

### Manifest

![IntroToSkillsPieces](./SkillsOverview/IntroSkillsPiecesWithManifest.svg "Intro To Skills Pieces")

* A *skill consumer* does not necessarily have access to a *skill's code*
* Use a *skill manifest* to describe activities the skill can receive and generate, its input and output parameters, and the skill's endpoints

### Parent to Child Flow Overview

![ParentToChildFlowOverview](./SkillsOverview/ParentToChildFlowOverview.svg "Parent To Child Flow Overview")

___

## Diagram Sketched Drafts

Need to see if I can convert these to Mermaid diagrams or if I would need to use some other graphing source.

### Skill Client

*Skill client* sends Activities to a Skill. The Activity could be from the *user* or the *skill consumer*.
!["ClientSendsActivity"](./SkillsOverview/SketchedDrafts/ClientSendsActivity.jpg)

The *skill client* replaces the original user-root conversation reference with the root-skill converation reference.
!["ClientConvoRef"](./SkillsOverview/SketchedDrafts/ClientConvoRef.jpg "Client Conversation Reference")

The *skill client* adds the bot-to-bot auth Token.
!["ClientBotToBotAuth"](./SkillsOverview/SketchedDrafts/ClientBotToBotAuth.jpg "Client Bot-to-Bot Auth")

___

### Skill Handler

The *skill consumer* uses a *skill handler* to receive Activites from a *skill*.
!["HandlerReceivesActivity"](./SkillsOverview/SketchedDrafts/HandlerReceivesActivity.jpg "Handler Receives Activities")

The *skill handler* retrieves the original conversation reference (user-root).
!["HandlerConvoRef"](./SkillsOverview/SketchedDrafts/HandlerConvoRef.jpg "Handler Retrieves Original Convo Ref")

Handles ReplyToActivity and SendToConversation channel service API methods.
!["Handler_ReplyToAndSendTo"](./SkillsOverview/SketchedDrafts/Handler_ReplyToAndSendTo.jpg "Handler - SendToConversation and ReplyToActivity API methods")

Enforces authentication and claims validation.
!["HandlerAuthAndClaimsValidation"](./SkillsOverview/SketchedDrafts/HandlerAuthAndClaimsValidation.jpg "Handler Enforces Authentication and Claims Validation")