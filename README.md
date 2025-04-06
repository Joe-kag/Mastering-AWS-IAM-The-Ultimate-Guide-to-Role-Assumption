# Mastering-AWS-IAM-The-Ultimate-Guide-to-Role-Assumption

1\. **Introduction**\
Amazon Web Services (AWS) provides a powerful and flexible Identity and Access Management (IAM) service that enables fine-grained control over access to your AWS resources. A fundamental concept within IAM is **role assumption**, a key mechanism for delegating permissions securely and efficiently. In this technical project, we’ll dive into the process of assuming roles in AWS, offering a detailed, hands-on guide to help you gain a strong understanding of this essential security practice.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/34acedc6-e290-43e8-b1d2-0f03b31dc4a2/screenshot.jpeg?tl_px=0,0&br_px=1267,604&force_format=jpeg&q=100&width=1120.0)


2\. **Prerequisites**\
Before exploring the process of assuming roles in AWS, make sure the following prerequisites are in place:

- **AWS Account**: You’ll need an active AWS account to access both the AWS Management Console and the AWS Command Line Interface (CLI).

- **IAM Permissions**: Ensure you have the necessary IAM permissions to create, modify, and assume roles.

- **AWS CLI** *(Optional but Recommended)*: While most tasks can be completed via the AWS Management Console, having the AWS CLI installed and properly configured allows for greater flexibility and automation.


3\. **Understanding IAM Roles**\
AWS IAM roles are intended to be assumed by AWS services, resources, or external Identity Providers. Roles enable you to grant specific permissions to trusted entities without the need to expose long-term credentials like access keys. Here are the key points to understand about IAM roles:

- **Roles are defined by policies**: IAM roles are linked to policies that specify what actions the entity assuming the role is authorized to perform. For example, an IAM role with an S3 policy allows specific actions on S3 buckets or objects, such as uploading or retrieving data.

- **Temporary credentials**: When a role is assumed, it issues temporary security credentials that can be used to access AWS resources, like S3 buckets, based on the permissions defined in the associated policy.

- **Trust policy**: Each role has a trust policy that dictates which entities are permitted to assume the role. This could include AWS services like EC2 instances or even external accounts, allowing controlled access to resources like S3.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/f6fe34f6-22b8-4fcb-a831-2bb849d2a232/screenshot.jpeg?tl_px=0,0&br_px=858,538&force_format=jpeg&q=100&width=964)


4\. **Creating an IAM Role with a Trust Policy**\
To begin, sign in to the AWS Management Console and navigate to the IAM console. As part of the process, I will first create a new user account to refresh my skills and ensure a solid understanding of the foundational steps. Afterward, I will proceed to create the IAM role with the trust policy.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/11500344-e895-4ad2-8f39-f1c82c412d9c/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


5\. After entering the username, simply click "Next" since no further configuration is required for this step. In this case, I have created the user with the name "test-user."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/827af66a-b9eb-4cc1-9ff2-277d133d5842/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


6\. Great! You can now see the new user that i have created.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/ffd7925f-f6b5-40cb-9923-93c3d70d5a6c/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


7\. Next, we’ll click on the new user, then enable console access. At this stage, we’ll also need to create the user’s credentials, specifically the password. There is also an option to auto-generate the password if preferred.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/ae2d3332-77c3-4b8e-a1f7-f323b01f80c6/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


8\. After completing the previous steps, you will see a pop-up with the login credentials. Make sure to copy this information to a notepad or another secure location, as you will need it to sign in to the new user account "test-user."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/80e07188-1bdc-48ee-b3eb-21f08f9c64b1/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


9\. Next, we’ll sign in to the "test-user" account.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/20ae6457-fd15-4a64-ad16-ae1d7329ff32/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


10\. I have successfully logged into the "test-user" account, and we can see that the user has no permissions assigned.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/15d22ce0-6aab-45a2-803c-1f4923703da2/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


11\. Back to the root user, in the navigation pane, select "Roles" and then click "Create role."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/35a0cb97-2675-4452-b08b-6f9330cf8b94/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


12\. Choose “AWS account” as the trusted entity type. Be careful at this step, as you are creating a role for all users.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/ecc71b6c-eaf3-41d7-826c-09ffcb0ea966/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


13\. At this step, you can choose which account you want to use if you wish to assume the role using a different root account. However, for me, I used my parent root account, which is the default ,then click next.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/03d3203c-bf93-4feb-afd3-bfaa0ec015d3/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


14\. now you have to filter at this case i am creating s3-access , as seen below then click s3FullAccess

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/ba43c39d-df01-41db-bea8-44248bc37f4d/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


15\. Next, you will be directed to the dashboard. Edit the name of the role you're creating. For me, I used "s3-Full-Access."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/d78ef16c-d79d-493a-9254-4ac532120195/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


16\. Great! We have now successfully created the role, and we can see it added to our roles list.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/95e2a0ce-1555-4129-b92f-6b1a449adf28/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


17\. Next, we’ll create a policy. Navigate to Users, then click on "test-user." Under Add permissions, click Create inline policy.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/267ccc79-26d2-4893-bbf5-6a671e2fc47f/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


18\. I used **JSON** to edit my policy.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/b87bcbc2-8323-45ac-bfcd-71c04bdbf6e4/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


19\. And I have successfully created the policy.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/5dce7127-1040-4a0d-a549-0e06051d1b58/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


20\. We can now see that the "test-user" has been assigned the policy "s3-Full-Access-Policy."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/461b5edd-de9d-4841-90e5-f03ff39b4fd2/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


21\. Navigate to **Roles** and click on the role that we created. You’ll see a link to switch roles in the console. Copy this link and paste it into an incognito browser window where you have signed in as "test-user."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/29bd450e-61dc-49b4-a356-3b50e92604a1/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


22\. After loading that link this is the dashboard you will have  ,you can write the display- name or leave it its optional

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/f22e4a21-c543-42ce-8ede-064877fb77a7/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


23\. Hurray! We have successfully assumed the role for our "test-user." Now, the user can access the S3 bucket.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/3f39b31b-a576-4c74-a276-795f47d56532/screenshot.jpeg?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


24\. To switch back to your normal user, simply click on the user icon at the top, which will open a pop-out, then click **Switch back**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2025-04-06/9f8f19b7-a26b-4926-962b-c00a85fc9e06/user_cropped_screenshot.webp?tl_px=0,0&br_px=1920,1080&force_format=jpeg&q=100&width=1120.0)


25\. \
**Conclusion**\
In this demo, I successfully created an IAM user, role, and policy, then assigned the appropriate permissions. I  also demonstrated how to assume the role to access an S3 bucket. This process showcases the flexibility and security of AWS IAM in managing user access and delegating permissions.
