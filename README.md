# About
This repo is just a playground to experiment Azure actions.

# Secrets
## Let's be serious
The workflow `RunOnPush` exhibits a serious risk with misuse of secrets.  
A badly written workflow can reveal a secret to anybody logged-in on GitHub.

- In my first _echo_, the secret is correctly displayed, with double quotes. So all goes well and GitHub really censors it.  
- In my second _echo_, an error happens because my secret contains a quote: there is a _parser error_, and GitHub displays my secret in clear text! You really want to be cautious about that.

## The risk with pull requests
I was initally particularly interested in understanding how a PR author could exploit secrets.

### If someone creates a pull request and modifies the workflow with some code to reveal a secret (as above), could he make my secrets public?
Fortunately, the answer is no. This is demonstrated by the workflow `RunOnPr`.  
As I understand it, secrets are only available to the repo owner, so if a PR is created by another user, the script will only obtain an empty string.  
Of course, if the PR owner is the repo owner, the secret is readable.  
I have demonstrated this with tests, but not found the piece of doc which explains that.

### The repo owner has to be watchful of course about changes done in PRs.
Particularly, a rogue developer could modify the workflow files to reveal secrets.
