# LittleYCoin-web

Template from HTML5UP, AWS setup with cli by ChatGPT

HTML5 UP: https://html5up.net/

## Step-by-Step Guide for AWS Setup

### Create an S3 Bucket

```bash
aws s3 mb s3://your-bucket-name --region your-region
```
Replace your-bucket-name with your desired bucket name and your-region with the AWS region (e.g., us-west-2).
e.g. 
```bash
aws s3 mb s3://littleycoin-web --region us-east-2
```

### Upload Your Website Files

Make sure your website's static files are in a local directory.
Use the following command to upload your website files to the bucket:
```bash
aws s3 sync ./your-local-directory s3://your-bucket-name --region your-region
```
Replace ./your-local-directory with the path to your website files.
e.g. 
```bash
aws s3 sync ./s3 s3://littleycoin-web --region us-east-2
```

### Enable Static Website Hosting

Create a JSON file (e.g., website-configuration.json) with the following content:
```json
{
  "IndexDocument": {"Suffix": "index.html"},
  "ErrorDocument": {"Key": "error.html"}
}
```
Adjust index.html and error.html as per your filenames.
Apply this configuration to your bucket:
```bash
aws s3api put-bucket-website --bucket your-bucket-name --website-configuration file://website-configuration.json --region your-region
```
e.g.
```bash
aws s3api put-bucket-website --bucket littleycoin-web --website-configuration file://website-configuration.json --region us-east-2
```


### Update Bucket Policy to Allow Public Access

Turn Off "Block all public access":
You can use the put-public-access-block command with the AWS CLI to modify these settings. To turn off "Block all public access" for your littleycoin-web bucket, run:
```bash
aws s3api put-public-access-block \
--bucket littleycoin-web \
--public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false" \
--region us-east-2
```

Verify the Changes:
After running the command, you can verify that the changes have been made by using the get-public-access-block command:
```bash
aws s3api get-public-access-block --bucket littleycoin-web --region us-east-2 --no-cli-pager
```


Create a JSON file (e.g., bucket-policy.json) with the following policy (replace your-bucket-name):
```json
{
  "Version":"2012-10-17",
  "Statement":[{
    "Sid":"PublicReadGetObject",
    "Effect":"Allow",
    "Principal": "*",
    "Action":["s3:GetObject"],
    "Resource":["arn:aws:s3:::your-bucket-name/*"]
  }]
}
```
Apply the bucket policy:
```bash
aws s3api put-bucket-policy --bucket your-bucket-name --policy file://bucket-policy.json --region your-region
```
e.g.
```bash
aws s3api put-bucket-policy --bucket littleycoin-web --policy file://bucket-policy.json --region us-east-2
```

### Visit website 
http://littleycoin-web.s3-website.us-east-2.amazonaws.com