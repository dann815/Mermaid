## Flowchart

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

## Sequence Diagram

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```

## Gantt Diagram

```mermaid
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
```

## Class Diagram (Experimental)

```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
```

## Git Graph (Experimental):

```mermaid
gitGraph:
options
{
    "nodeSpacing": 150,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
```

## My Sequence

```mermaid
    sequenceDiagram
      participant BFS as Bot Framework Service
      participant Your Bot

      BFS->>+Your Bot: HTTP POST ConversationUpdate - user joins
      Your Bot-->>-BFS: 200 OK

      BFS->>+Your Bot: HTTP POST ConversationUpdate - bot joins
      Your Bot-->>-BFS: 200 OK

      BFS->>+Your Bot: HTTP POST Message "hi"
      Your Bot->>BFS: HTTP POST Message "You said: hi"

      BFS-->>Your Bot: 200 OK
      Your Bot-->>-BFS: 200 OK
```
## 1

![test](./mermaid-diagram-20191125142523.svg)

```mermaid
classDiagram
    class NumberPrompt{
        +string defaultLocale
        
        #onPrompt(context, state, option, isRetry)
        #onRecognize(context, state, options)
        - getCultureFormattedForGlobalize(culture)
    }

    class Prompt{
        +beginDialog(dc, options)
        +contingueDialog(dc)
        +resumeDialog(dc, reason, result)
        +repromptDialog(context, instance)
        #onPrompt(context, state, options)
        #onRecognize(context, state, options)
        #appendChoices(prompt, channelId, choices, style, options)
    }

    class Dialog{
        +DialogTurnResult EndOfTurn
        #BotTelemetryClient _telemetryClient
        +id()
        +id(value)
        +telemetryClient()
        +telemetryClient(client)
        +beginDialog(dc, options)
        +continueDialog(dc)
        +resumeDialog(dc, reason, result)
        +repromptDialog(context, instance)
        +endDialog(context, instance, reason)
        +onDialogEvent(dc, e)
        #onPreBubbleEventAsync(dc, e)
        #onPostBubbleEventAsync(dc, e)
        #onComputerId()
        #hashedLabel(label)
    }
    <<abstract>> Dialog
    <<abstract>> Prompt
    Dialog <|-- Prompt
    Prompt <|-- NumberPrompt
    
```