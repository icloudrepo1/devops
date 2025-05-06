## Gitlab runner on aws-fargate setup
==========================================

#### Prerequisites :-

GitLab project or self-managed GitLab instance

AWS account with permission to create ECS, IAM roles, and VPC resources

AWS CLI configured

Docker installed (for building your GitLab Runner container image)


#### Step-by-Step Setup :-

##### 1. create a gitlab personal access token

goto gitlab  ->  profile  ->  Edit Profile  ->  access tokens  ->  Add new token ( name , Select scopes = api, read_repository )

save the token

## gitlab runner on aws ec2 instance setup
================================================
