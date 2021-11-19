# Automated-assign-labeler

This repository is a collection of numerous existing actions on marketplace bunched together to function ultra-efficiently.  
All links to marketplace & usage here have been provided.
This helps keep the repo clean, concise & out of chaos moderating the process right from the beginning (issue creation) to the end (PR merge/close)

## Special Custom Action
  > ### [Issue Watcher](https://github.com/Suvraneel/Issue_Watcher)
  > #### ***Avoids misuse of self-assigns by limiting the no. of issues that can be claimed by assignees***

--- 

## Features
- ### Issue/PR Creation Actions
  - Greeting Action greets contributor  
      - *Example Workflow :*  
      **Find the workflow file [here](.github/workflows/greetings.yml)**  

  - Self-assign using `/assign`
  - Preventing rogue issue spammers by limiting number of self-assigns (by default, 3)  
    - *Example Workflow :*  
    **Find the workflow file [here](.github/workflows/issue-assign.yml)**
    
- ### Issue/PR Auto Labeler  
  #### *Note* - There are numerous labelers present in the marketplace. So, maintainers are requested to choose in accordance to project requirements. Consequently, a combination has been used here, in order to capture the best of both worlds.
  Types :
    - Labels issues based on keywords found in Issue/PR
      - Action deprecated, so [Bot here](https://github.com/marketplace/keywordlabeler) *(Recommended)*
      - Configuration file [here](.github/keylabeler.yml)
    - Labels PRs based on extension of file changed
      - [Action here](https://github.com/marketplace/actions/auto-label-action)  
      - *Example Workflow :*  
        **Find the workflow file [here](.github/workflows/greetings.yml)**  
        Configuration file [here](.github/auto-label.json)
  - Labels PRs based on branch  
    - [Action here](https://github.com/marketplace/actions/label-mastermind)
    
- ### On PR close
  - Finds & closes any linked issues to the PR
      - Example Workflow :  
      **Find the workflow file [here](.github/workflows/Auto_Issue_Closer.yml)**
      
- ### Close Stale Issues
  - Marks & closes stale issue after a pre-stipulated time.
      - [Action here](https://github.com/marketplace/actions/close-stale-issues)
        or
      - [Bot here](https://github.com/marketplace/stale) *(Recommended)*

- ### Auto-updates Contributors list
  - Fetches top contributors & adds them to `CONTRIBUTORS.md`
      - Example Workflow :  
      **Find the workflow file [here](.github/workflows/update-contributors.yml)**  
        or
      - [Bot here](https://allcontributors.org/docs/en/bot/installation) *(Recommended)*
      - Configuration file [here](.github/keylabeler.yml)
    
### Note-  Issue Form (Beta) has been utilised here for keylabeler to work super-efficently  
  
---

## Featured Workflow Example for [Issue Watcher](https://github.com/Suvraneel/Issue_Watcher)
```yaml
name: Assigner

on:
  issue_comment:
    types: [created]

jobs:
  slash_assign:
    # If the acton was triggered by a new comment that starts with `/assign`
    # or a on a schedule
    if: >
      (github.event_name == 'issue_comment' && startsWith(github.event.comment.body, '/assign')) || github.event_name == 'workflow_dispatch'
    runs-on: ubuntu-latest
    steps:
      - name: Assign the user or unassign stale assignments
        uses: JasonEtco/slash-assign-action@v0.0.3
        with:
          assigned_label: Assigned
          days_until_warning: 5
          days_until_unassign: 7
          stale_assignment_label: Stale
          assigned_comment: "This issue [has been assigned]({{ comment.html_url }}) to {{ comment.user.login }}!\nIt will become unassigned if it is nott closed within {{ totalDays }} days. A maintainer can also add the **{{ inputs.pin_label }}** label to prevent it from being unassigned."
          fail_comment: "This issue is already assigned to a contributor."

      - name: Message failure
        if: ${{ failure() }}
        uses: actions/github-script@v4
        with:
          script: |
            github.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: 'The issue is already assigned!\nPlease find/create a new issue to contribute to.\nYou can safely disregard the failed workflow notification for this issue. ❌',
            });          
      - name: Checkout code
        uses: actions/checkout@main
      - name: Run Action
        uses: Suvraneel/Issue_Watcher@main
        with:
          token: "${{ secrets.GITHUB_TOKEN }}"
          author: "${{github.actor}}"
          repo: Suvraneel/Automated-assign-labeler #Change the Repo name
          maxIssue: 3
```
