# EC2 Storage
> [EBS Volume Types](#EBS_Volume_Types)  
> [EBS Encryption](#EBS_Encryption)  


## EBS_Volume_Types
- gp2 / gp3 (SSD): General purpose SSD volume
- io1 / io2 (SSD): Highest-performance SSD volume
- st1, sc1 (HDD): Low cost HDD volume
- EBS Volumes are characterized in Size | Throughput | **IOPS (I/O Ops Per Sec)**
- **Only gp2/gp3 and io1/io2 can be used as boot volumes**

## EBS_Encryption
- When you create an encrypted EBS volume, you get the following:
    - Data at rest is encrypted inside the volume