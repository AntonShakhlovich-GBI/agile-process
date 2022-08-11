---
layout: page
title: User Story Flow
permalink: /user-story-flow/
---
```mermaid!
graph TB
    PM_Creates_Draft[[PM Creates User Story Draft]]
    PM_Creates_Draft-->Draft
    subgraph "Requirements Elaboration"
      Draft(Open)
      Design(In Design)
      NeedInfo(Label with 'Need More Information')
      A_Clarify[[Clarify Requirements]]
      RemoveLabel[[Remove Need More Information Label]] 
      A_Assign_PM[[Assign to PM]]
      A_Set_Reqirements[[Set Initial Requirements and AC]]
      A_Label[[Label with Team Label: CC or CT]]
  
      Draft--> A_Set_Reqirements
      A_Set_Reqirements --> A_Label
      A_Label --> Design
    end
  
    Design --> If_Clear
  
    subgraph "Refinement"
      If_Clear{Are requirements clear?}
      Backlog(Backlog)
  
      If_Clear -.-> |No|NeedInfo
  
      If_Clear --> |Yes|Backlog
      NeedInfo --> A_Assign_PM
      A_Assign_PM --> A_Clarify
      A_Clarify --> Design
    end
  
    Backlog --> A_Estimate
  
    subgraph "Estimation"
      A_Estimate[[Set Story Points]]
    end
  
    A_Estimate --> A_Plan
  
    subgraph "Planning"
      A_Plan[[Put into Iteration Scope based on Velocity]]
    end
  
    A_Plan --> InProgress
  
    subgraph "Implementation"
      InProgress(In Progress)
      CodeReview(Code Review)
      InQA(In QA)
  
      If_Bug{Bug found?}
      If_P1-P2{P1-P2?}
      A_Bug_Sprint[[Put Bug into Sprint Backlog]]
      A_Bug_Project[[Put Bug into Porject Backlog]]
  
      InProgress --> CodeReview --> InQA --> If_Bug
      If_Bug --> |Yes| If_P1-P2
      
      If_P1-P2 --> |Yes|A_Bug_Sprint --> InProgress
      If_P1-P2 -.-> |No|A_Bug_Project
    end
      If_Bug -.-> |No| ReadyToRelease
      A_Bug_Project --> ReadyToRelease
  
    subgraph "Verification"
      ReadyToRelease(Ready To Release)
      
      If_Verified{Verification Passed?}
      Closed(Closed)
      A_Assign_PM_Release[[Assign To PM]]
      A_Assign_Reporter[[Assign To Reporter]]
      A_Reporter_Resolution[[Reporter set Resolution]]
      Resolved(Resolved)
  
      ReadyToRelease --> A_Assign_PM_Release
      A_Assign_PM_Release --> If_Verified
      If_Verified -->|Yes|Closed
      Closed --> A_Assign_Reporter
      A_Assign_Reporter --> A_Reporter_Resolution
      A_Reporter_Resolution --> Resolved
    end
  
    If_Verified -.->|No|InProgress
  
   
    classDef draft fill:#b2b2b2
    class Draft draft

    classDef notReadyStatus fill:#fbbc3d
    class Design notReadyStatus
    
    classDef action fill:#f56342, stroke-width: 4px, stroke: black
    class RemoveLabel,NeedInfo,PM_Creates_Draft,A_Estimate,A_Clarify,A_Assign_PM,A_Set_Reqirements,A_Label,A_Assign_PM_Release,A_Bug_Sprint,A_Bug_Project,A_Plan action,A_Assign_Reporter

    classDef development fill:#426cf5
    class Backlog,InProgress,CodeReview,InQA development
  
    classDef closed fill:#28ab00
    class ReadyToRelease,Closed,Resolved closed
```
