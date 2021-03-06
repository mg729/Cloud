# AWS Auto Scaling Group (ASG)

- [Service Auto Scailing](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-auto-scaling.html)
- [Configuring your service to use Service Auto Scaling](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-configure-auto-scaling.html)

# Predictive scaling for Amazon EC2 Auto Scaling
- [Predictive scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-predictive-scaling.html)
- In general, if you have regular patterns of traffic increases and applications that take a long time to initialize, you should consider using predictive scaling. Predictive scaling can help you scale faster by launching capacity in advance of forecasted load, compared to using only dynamic scaling, which is reactive in nature. Predictive scaling can also potentially save you money on your EC2 bill by helping you avoid the need to overprovision capacity.

# target tracking scaling policy
> To address the highly variable demand the company
has implemented Amazon EC2 Auto Scaling Management

- With target tracking scaling policies, you select a scaling metric and set a target value.
Amazon EC2 Auto Scaling creates and manages the CloudWatch alarms that trigger
the scaling policy and calculates the scaling adjustment based on the metric and the
target value.