
# Jetbrains

## Configure Mermaid in Jetbrains IDE

Open Settings. 

Open Languages & Frameworks → Markdown and tick Mermaid.

![[WebDev/softwareDevFundamentals/_topics/_images/mermaidJetbrainsEnableMarkdown.png]]

---

## Create Mermaid File

Inside the project, right-click on the folder you wish to create the file, choose New→File and name the file appropriately. For instance `erd.md`.

![[WebDev/softwareDevFundamentals/_topics/_images/mermaidJetbrainsNewFile.png]]

![[WebDev/softwareDevFundamentals/_topics/_images/mermaidJetbrainsNewFileName.png]]

![[WebDev/softwareDevFundamentals/_topics/_images/mermaidJetbrainsNewFileEmpty.png]]

---

## Mermaid Entity Relationship Diagram

After creating the markdown file, indicate to the IDE that it’s the start and the end of a diagram to preview.

![[WebDev/softwareDevFundamentals/_topics/_images/mermaidJetbrainsERDDiagramStart.png]]


```text
# Mermaid Project Plan / Gantt Chart

## Resource

[Gantt diagrams | Mermaid](https://mermaid.js.org/syntax/gantt.html)

## Project Plan Development Process

Follow the steps to develop your project plan.

1. Create a list of all the jobs required to complete the task.
2. Categorise them into sections (if required)
3. Identify key dates / deadlines
    1. Importantly, the final due date
4. Identify which jobs/tasks need to be completed before others.
5. Put in start and end dates for each job / task.

## Starting Code Template

Use this code to start and configure the chart in Visual Studio Code (or whatever IDE used).


```mermaid
gantt
    title Star Invaders Project Plan
    dateFormat DD-MM-YY
    axisFormat %d-%B
    tickInterval 1week

```

# Visual Studio Code