### CDN and working with image assets

If your email contains images you'll want to serve them from a CDN. This Gruntfile has support for Rackspace Cloud Files ([pricing](http://www.rackspace.com/cloud/files/pricing/)).

<img src="http://i.imgur.com/oO5gfkZ.jpg" width="500">

* Sign up for a Rackspace Cloud account (use the [Developer Discount](http://developer.rackspace.com/devtrial/) for $300 credit)
* Create a new Cloud Files container
* Open up `Gruntfile.js` or `secrets.json`
* Change 'cloudfiles' settings to your settings (you can find your Rackspace API key under your account settings)
* Make any other config changes as per [grunt-cloudfiles](https://github.com/rtgibbons/grunt-cloudfiles) instructions

Run `grunt cdnify` to run the default tasks as well as upload any images to your CDN.

Run `grunt cdnify send --template=branded.html` to send the email to yourself with the 'CDNified' images.


### Using Amazon S3 for image assets

Another option for serving images is to use Amazon S3. Basic service is free of charge. For more information on setting up an account, visit [Amazon](http://aws.amazon.com/s3/).

The Gruntfile uses [grunt-aws-s3](https://github.com/MathieuLoutre/grunt-aws-s3).

Once your AWS account is setup, create a Bucket within S3. You will need to ensure your Bucket has a policy setup under Permissions. Below is a very loose sample policy for testing purposes. You should read up on [AWS Identity and Access Management](http://aws.amazon.com/iam/) for more information.

**Sample S3 Bucket Policy**

```
{
  "Version": "2008-10-17",
  "Id": "Policy123",
  "Statement": [
    {
      "Sid": "Stmt456",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::BUCKETNAME"
    }
  ]
}
```

Run `grunt s3upload` to upload images to your S3 Bucket. This will also run a replace task to change image paths within the destination directory to use the new S3 path.

### More resources

* For more transactional email templates check out [Mailgun's collection of templates](http://github.com/mailgun/transactional-email-templates).
* [Things I've learned about sending email](http://www.leemunroe.com/sending-email-designers-developers/)
* [Things I've learned about building HTML email templates](http://www.leemunroe.com/building-html-email/)
