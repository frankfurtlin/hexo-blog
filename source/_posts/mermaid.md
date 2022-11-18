---
title: mermaid
date: 2022-11-16 09:16:48
tags:
    - 教程
    - 工具
categories: 教程
cover: /assets/img/cover/fire.jpg
---

使用mermaid标签可以绘制Flowchart（流程图）、Sequence diagram（时序图）、Class Diagram（类别图）、State Diagram（状态图）、Gantt（甘特图）和Pie Chart（圆形图），具体可以查看[mermaid文档](https://mermaid-js.github.io/mermaid/#/)

# 示例

### 流程图
``` markdown
{% mermaid %}
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
{% endmermaid %}
```
{% mermaid %}
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
{% endmermaid %}

### 时序图
``` markdown
{% mermaid %}
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
{% endmermaid %}
```
{% mermaid %}
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
{% endmermaid %}

### 甘特图
```
{% mermaid %}
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
{% endmermaid %}
```
{% mermaid %}
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
{% endmermaid %}

### 类图
```
{% mermaid %}
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
{% endmermaid %}
```
{% mermaid %}
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
{% endmermaid %}

### Git图
```
{% mermaid %}
gitGraph
    commit
    commit
    branch develop
    commit
    commit
    commit
    checkout main
    commit
    commit
{% endmermaid %}
```
{% mermaid %}
gitGraph
    commit
    commit
    branch develop
    commit
    commit
    commit
    checkout main
    commit
    commit
{% endmermaid %}

### 实体关系图
```
{% mermaid %}
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
{% endmermaid %}
```
{% mermaid %}
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
{% endmermaid %}

### 用户流程图
```
{% mermaid %}
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
{% endmermaid %}
```
{% mermaid %}
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
{% endmermaid %}