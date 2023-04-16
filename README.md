AWS Lambda is a server less solutions to run some code without care about resources. You focus only on a logic of the function you want to run, the rest is on the AWS side. It’s possible to run function in periodic fashion or based on external events (CloudWatch).


Server less solutions are popular now because includes a lot of advantages. We don’t care about servers, operating systems etc. There is also cost savings aspect, you pay only for resources (like Memory) and time the function run. And what is most important, you pay only when function is executed.


So how it works. For every few minutes Lambda verifies, if http code 200 is returned. In the next step the result is send to CloudWatch as custom metric. For simplifying, this custom metric can have this values:


If http respond code is 200 or 304, metric is set to 200.
If there is impossible to connect to website (for ex. httpd is death), metric is set to 100.
In any other case metric is set to 50.
In the next, there is an Alarm configured for this metric. If the metric value is lower than 200, the email notification will be send.
For simplicity and flexibility this solution is based on two Lambda functions:
WebsiteCheck – this functions is trying to connect to specified URL and, check http code and send the value to the second function.
SendMetric- this function sets CloudWatch metric based on received parameters: custom metric name and the metric value
![csc project pic 1](https://user-images.githubusercontent.com/100797488/232280531-e54e260d-23b3-4fa2-9f2c-3c5e0d181c25.jpg)
![csc project pic 2](https://user-images.githubusercontent.com/100797488/232280539-6a075604-9e86-4a40-a02a-b0f82a33d472.jpg)
![csc pic 5](https://user-images.githubusercontent.com/100797488/232280541-2c556c69-115a-4d30-856a-3845f0bdd82b.jpg)
![csc project pic 3](https://user-images.githubusercontent.com/100797488/232280543-2c214485-b019-44e3-b354-5ad1eb59e27c.jpg)
![csc pic 4](https://user-images.githubusercontent.com/100797488/232280548-53c8429e-9bd9-49c6-87ad-772821eef02d.jpg)
