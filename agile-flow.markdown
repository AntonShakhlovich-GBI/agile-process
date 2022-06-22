---
layout: page
title: Agile Flow
permalink: /agile-flow/
---
```mermaid!
graph TB
    subgraph "Requirements Elaboration"
      Draft(Open)
      Design(In Design)
      NeedInfo(Need More Information)
      A_Clarify[[Clarify Requirements]]
      A_Assign_PM[[Assign to PM]]
      A_Set_Reqirements[[Set Initial Requirements and AC]]
      A_Label[[Label with Team Label]]
  
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
  
      ReadyToRelease --> A_Assign_PM_Release
      A_Assign_PM_Release --> If_Verified
      If_Verified -->|Yes|Closed
    end
  
    If_Verified -.->|No|InProgress
  
    style Draft fill:#b2b2b2
    style Design fill:#fbbc3d
    style NeedInfo fill:#fbbc3d
    
    style A_Estimate fill:#f56342, stroke-width: 4px, stroke: black
    style A_Clarify fill:#f56342, stroke-width: 4px, stroke: black
    style A_Assign_PM fill:#f56342, stroke-width: 4px, stroke: black
    style A_Set_Reqirements fill:#f56342, stroke-width: 4px, stroke: black
    style A_Label fill:#f56342, stroke-width: 4px, stroke: black
    style A_Assign_PM_Release fill:#f56342, stroke-width: 4px, stroke: black
    style A_Bug_Sprint fill:#f56342, stroke-width: 4px, stroke: black
    style A_Bug_Project fill:#f56342, stroke-width: 4px, stroke: black
    style A_Plan fill:#f56342, stroke-width: 4px, stroke: black
    
    style Backlog fill:#426cf5
    style InProgress fill:#426cf5
    style CodeReview fill:#426cf5
    style InQA fill:#426cf5
  
    style ReadyToRelease fill:#28ab00
    style Closed fill:#28ab00
```
