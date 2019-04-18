# lambda-default-dlq

Regularly sets a Dead Letter Queue for all your lambda functions that need it.
If your functions already have one, they are skipped.

This will ensure that your failed lambda executions won't go unnoticed.
You can specify a queue name or leave the default.

After the stack is deployed to all your regions, you can subscribe a target like Lambda or SNS to these queues so that you can go it and investigate.


If you use [sceptre](https://github.com/cloudreach/sceptre), you can deploy this in all regions in one step with:

`sceptre launch -y dev`

or deploy per region with this button: 

<a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=lambda-default-dlq&templateURL=https://s3.amazonaws.com/jeshan-oss-public-files/lambda-default-dlq-template.yaml">
<img src="https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png"/>
</a>


You can choose an interval (number of hours) to periodically find your new functions and add DLQs to them.

Note:
Functions need the `sqs:SendMessage`permission before a DLQ can be attached to them. In case you have such functions, a new message will be put in the DLQ stating which functions' policies you will need to update.

Also, note that this project is still experimental. Please share your experiences with the community.
