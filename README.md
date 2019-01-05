### **IMPORTING OVA-to-AMI**
-------------------------
[Refference!](https://docs.aws.amazon.com/vm-import/latest/userguide/vmimport-image-import.html#import-vm-image)

**1**. **Create S3 bucket**

  **To create an S3 bucket**
Open the Amazon S3 console at https://console.aws.amazon.com/s3/.
Choose Create Bucket.
  In the Create a Bucket dialog box, do the following:
  - For Bucket Name, type a name for your bucket. This name must be unique across all existing bucket names in Amazon S3. In some regions, there might be additional restrictions on bucket names. For more information, see Bucket Restrictions and Limitations in the Amazon Simple Storage Service Developer Guide.
  - For Region, select the region that you want for your AMI.
  - Choose Create.

**2.  Access and security**
        
Change in role-policy

           "Resource":[
           "arn:aws:s3:::<bucket-name >",
            "arn:aws:s3:::<bucket-name >/*"
         ]
       }    
 Command : 
        aws iam create-role --role-name vmimport --assume-role-policy-document file://trust-policy.json
      
** 3.   Converting to AMI **
  
  Change in container.json

      "S3Bucket": "< your s3 bucket name>",
        "S3Key": "location-in-your-bucket/my-windows-2008-vm.ova"
        
  Make sure you have copied the OVA file to S3 and completed the location in the above step. 
  
        Command :
        Windows
        - aws ec2 import-image --description "Windows 2008 OVA" --license-type <value> --disk-containers file://containers.json
        Linux 
        - aws ec2 import-image --description "Centos7 OVA" --disk-containers file://containers.json
 
** 4.   Checking the status of AMI   **

        aws ec2 describe-import-image-tasks --import-task-ids import-ami-abcd1234
        Wait till the status is completed.
