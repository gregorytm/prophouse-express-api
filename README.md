sw bucket setup
create a new s3 bucket aws.com
bucket name and aws region
default on else but remember name and local.

create .env file
DATABASE_URL=''
AWS_BUCKET_NAME=''
AWS_BUCKET_REGION=''

open IAM from amazon dashboard
Policies->create new policy
Service:s3
Actions:
Read->GetObject
Write->PutObject,DeleteObject
in Resource section->click add ARN
fill in bucket name Object name check any
click next:Tags then next:review

name policy myapp-s3-bucket-access
create plicey

now navigate to Users and click add user button
username: myapp-web-app
click Access key -Programatic access
click Next
Attach existing policies directly
search for myapp-s3-bucket-access
and click next
no tags click next
create ueser
now we need Access key Id and secret key
add them to .env
AWS_ACCESS_KEY=''
AWS_SECRET_ACCESS_KEY=''

<!-- Setting up cloudfront cdn -->
in our aws.s3 bucket lets search CloudFront
create new distriubution button
origin domina set up our s3 bucket
change Origin access to be Origin access control settings
viewer protocol policy to redirect http to https
copy Distribution domain name

go back to server.js find add
  for (let post of posts) {
    post.imageUrl = await getObjectSignedUrl(post.imageName)
  }
  to be 
  for (let post of posts) {
    post.imageUrl="Distribution domain name/"+post.imageName
  }