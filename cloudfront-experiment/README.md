# cloudfront-experiment

* Expose S3 bucket contents as a website
* Secure this website with HTTP basic authentication (lambda@edge)
* Show how lambda@edge can be used to handle some requests programmatically.

## How to deploy and undeploy

* `envTag=dev ./tool.sh deploy` to deploy. When deploying an update that involves changes to `LambdaFunction`, do manually change its name. Note that `LambdaFunction` updates don't delete its existing physical resources ([because](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-delete-replicas.html)), so after a few updates you'll end up having `...-edge-lambda1`, `...-edge-lambda2`, etc. It's your responsibility to manually delete them later.
      
* `envTag=dev ./tool.sh undeploy` to undeploy. This will not delete all the `LambdaFunction` instances. It's your responsibility to manually delete them later.

See the `WebsiteUrl` stack output for the website root. 

* Go to the website and see it's asking for credentials. Try invalid credentials like `uuu`/`ppp` and see you can't get it. Try valid credentials: `user1`/`secret` and see it shows you the home page.
* Try `/api/test` for a dummy greeting message generated by the lambda function.