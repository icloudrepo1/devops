## Gitlab-runner AWS fargate


### Requirements :-

AWS account

GitLab account (with access to a project)

GitLab Runner registration token (from GitLab)

AWS CLI + Docker installed locally

### steps :-


#### Step 1 - Get GitLab Runner Registration Token

Log in to your GitLab account and open your project.

In the left sidebar, go to:

  - Settings > CI/CD
  - Scroll down to the Runners section.
  - Under Set up a specific Runner manually, click to expand the section.
  - You’ll see a field labeled: Registration token
  - Copy this token — you'll use it to register your runner.
    

