---
title: 'Custom Commands concepts and definitions - Speech service'
titleSuffix: Azure Cognitive Services
description: In this article, you learn about concepts and definitions for Custom Commands applications.
services: cognitive-services
author: singhsaumya
manager: yetian
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 06/18/2020
ms.author: sausin
---

# Custom Commands concepts and definitions

This article serves as a reference for concepts and definitions for Custom Commands applications.

## Commands configuration
Commands are the basic building blocks of a Custom Commands application. A command is set of configurations required to complete a specific task defined by a user.

### Example sentences
Example utterances are the set examples the user can say to trigger a particular command. Note that you need to provide only a sample of utterances and not an exhaustive list. 

###	Parameters
Parameters are information required by the commands to complete a task. In complex scenarios, parameters can also be used to define conditions which trigger custom actions.

###	Completion rules
Series of rules to be executed once the command is ready to be fulfilled, i.e. when all the conditions of the rules are satisfied.

###	Interaction rules
Additional rules to handle more specific or complex situations. You can add additional validations or configure advanced features such as confirmations or one-step correction. You can also build your own custom interaction rules.

## Parameters configuration

Parameters are information required by commands to complete a task. In complex scenarios, parameters can also be used to define conditions which trigger custom actions.

### Name
A parameter is identified by the name property. You should always give a descriptive name to a parameter. A parameter can be referred across different sections, like - while constructing conditions, speech responses or other actions.
 
### IsGlobal
Checkbox indicating whether the scope of this parameter is shared across all the commands in the application. If a parameter is global, its value can potentially be provided from any command scope and once a value is assigned - it can be referred from any of the commands. 

### Required
Checkbox indicating whether a value for this parameter is required for command fulfillment/completion. You must configure responses to prompt user to provide value if a parameter is marked as required.

### Type
Custom Commands supports following parameters types-


* DateTime
* Geography
* Number
* String

All these parameter types support default value configuration which you can configure from the portal.

### Configuration
Configuration is a parameter property defined only for type: String. Below are the supported values
* None
* Accept full input: Enabling this option, parameter accepts any input utterance, this is useful when the user needs a parameter with the full utterance. for e.g. postal addresses.
* Accept predefined input values from external catalog: used to configure parameter which can assume a wide variety of values. e.g. sales catalog. In this case the catalog is hosted on an external web endpoint and can be configured independently.
* Accept predefined input values from internal catalog: used to configure parameter which can assume a few values. In this case values must be configured in the Speech Studio.


### Validation
Validations are constructs applicable to certain parameter types which lets you configure constraints on parameter's value. Currently, Custom Commands supports validations on following parameters types:
* DateTime
* Number

## Rules configuration
A rule in Custom Commands is defined by a set of **conditions**, that when met, will execute a set of **actions**. Rule also lets configure its **post execution state** and **expectations** for the next turn.

### Types
Custom Commands support following rule categories:
* Completion rules

    List of rules to be executed upon command fulfillment. All the rules configured in this section for which the conditions are true will be executed.
    
* Interaction rules

    Interaction rules can be used to configure additional custom validations, confirmations, one-step correction or for for accomplishing any other custom dialog logic. These rules are evaluated at each turn processing and can be used to trigger completion rules.

The different actions configured as part of a rule are executed in the order they appear in the authoring portal.
    
### Conditions
Set of conditions which must be met for a rule to execute. Rules condition can be of the following types:
* Parameter value equals: configured parameter's value equals to a specific value.
* No parameter value: configured parameters shouldn't have any value.
* Required parameters: configured parameter has a value.
* All required parameters: all the parameters which have been marked as required have a value.
* Updated parameters: one or more parameter values were updated as a result of processing the current input (utterance/activity).
* Confirmation was successful: input utterance/activity was a successful confirmation (yes).
* Confirmation was denied: input utterance/activity was a successful confirmation (no).
* Previous command needs to be updated : this condition is used in instances when you want to catch a negated confirmation along with an update. Behind the scenes, this is configured for when the dialog engine detects a negative confirmation where the intent is the same as the previous turn, and the user has responded with an update.

### Actions
* Send speech response: send a speech response back to the client.
* Update parameter value: update value of a command parameter to a specified value.
* Clear parameter value  clear off command parameter value.
* Call web endpoint: make call to a web endpoint.
* Send activity to client: send a custom activity to the client.

### Expectations
Expectations are used to configure hints for the processing of next user input. Following types are supported:
* Expecting confirmation from user: specifies that the application is expecting a confirmation (yes/no) for the next user input.
* Expecting parameter(s) input from user: specify one or more command parameters which the application is expecting from the user input.

### Post-execution state
Dialog state after processing the current input (utterance/activity). It's of the following types:
* Command completed: complete the command and no additional rules of the command will be processed.
* Execute completion rules: execute all the valid completion rules.
* Wait for user's input: wait for the next user input.

## Next steps

> [!div class="nextstepaction"]
> [See samples on GitHub](https://aka.ms/speech/cc-samples)
