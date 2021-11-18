# Automated-assign-labeler

This repository is a collection of numerous existing actions on marketplace bunched together to function ultra-efficiently.  
All links to marketplace & usage here have been provided.
This helps keep the repo clean, concise & out of chaos moderating the process right from the beginning (issue creation) to the end (PR merge/close)

## Special Custom Action
  ### [Issue Watcher](https://github.com/Suvraneel/Issue_Watcher)
  
--- 

## Features
- ### Issue/PR Creation Actions
  - Greeting Action greets contributor
      - **Find the workflow file [here](.github/workflows/greetings.yml)**  

  - Self-assign using `/assign`
  - Preventing rogue issue spammers by limiting number of self-assigns (by default, 3)  
    
    - **Find the workflow file [here](.github/workflows/issue-assign.yml)**
    
- ### Issue/PR Auto Labeler  
  #### *Note* - There are numerous labelers present in the marketplace. So, maintainers are requested to choose in accordance to project requirements. Consequently, a combination has been used here, in order to capture the best of both worlds.
  Types :
    - Labels issues based on keywords found in Issue/PR
      - Action deprecated, so [Bot here](https://github.com/marketplace/keywordlabeler) *(Recommended)*
      - Configuration file [here](.github/keylabeler.yml)
    - Labels PRs based on extension of file changed
      - [Action here](https://github.com/marketplace/actions/auto-label-action)  
      - **Find the workflow file [here](.github/workflows/greetings.yml)**  
      - Configuration file [here](.github/auto-label.json)
  - Labels PRs based on branch  
    - [Action here](https://github.com/marketplace/actions/label-mastermind)
    
- ### On PR close
  - Finds & closes any linked issues to the PR
      - **Find the workflow file [here](.github/workflows/Auto_Issue_Closer.yml)**
      
- ### Close Stale Issues
  - Marks & closes stale issue after a pre-stipulated time.
      - [Action here](https://github.com/marketplace/actions/close-stale-issues)
      - [Bot here](https://github.com/marketplace/stale) *(Recommended)*
    
    
### Note-  Issue Form (Beta) has been utilised here for keylabeler to work super-efficently 
