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

Change in container.json

      "S3Bucket": "< your s3 bucket name",
        "S3Key": "location-in-your-bucket/my-windows-2008-vm.ova"
        
Change in role-policy

           "Resource":[
           "arn:aws:s3:::<bucket-name >",
            "arn:aws:s3:::<bucket-name >/*"
         ]
       }      
3. 
