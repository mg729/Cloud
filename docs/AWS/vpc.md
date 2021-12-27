# VPC (Virtual Private Cloud)
> [Site-to-Site VPN](#Site_to_Site_VPN)  
> [Transit Gateway](#Transit_Gateway)  
> [Cloud Hub](#Cloud_Hub)  
> [VPC Peering](#VPC_Peering)  
> [Direct Connect](#Direct_Connect)  
> [VPC Endpoint](#VPC_Endpoint)  
> [NAT Gateway](#NAT_Gateway)   
> [NAT Instance](#NAT_Instance)  


## Site_to_Site_VPN
![sts](https://docs.aws.amazon.com/ko_kr/vpn/latest/s2svpn/images/vpn-how-it-works-vgw.png)
- `Virtual Private Gateway (VGW)`
    - VPN concentrator on the AWS side of the VPN connection
- `Customer Gateway (CGW)`
    - Software application or physical device on customer side of the VPN connection
- You can attach **one virtual private gateway to a VPC at a time**. To connect the same Site-to-Site VPN connection to multiple VPCs, we recommend that you explore using a *transit gateway* instead. 
- IPSec 지원
- **인터넷 망 (보안성 떨어짐)** 
  - *--> 'constant throughput' is not possible over the internet, so site to site VPN is out for the case.*
- 서비스도입에 많은 시간이 필요하지 않음
  - *The connection set up quickly / immediately*

### How to increase Site-to-Site VPN connections 
- [Using transit gateway](https://aws.amazon.com/blogs/networking-and-content-delivery/scaling-vpn-throughput-using-aws-transit-gateway/)
- **Use a transit gateway** with equal cost multipath routing and add additional VPN tunnels.

### Using redundant Site-to-Site VPN connections to provide failover
![Site to Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/images/Multiple_Gateways_diagram.png)

- To protect against a loss of connectivity in case your customer gateway device becomes unavailable, you can set up a second Site-to-Site VPN connection to your VPC and virtual private gateway by using a second customer gateway device

## Transit_Gateway
![TransitGateway](https://d1.awsstatic.com/product-marketing/transit-gateway/tgw-after.d85d3e2cb67fd2ed1a3be645d443e9f5910409fd.png)
- *Connect multiple VPC with multiple On Premise Network*
- Use VPN and Direct Connect to establish connection
- Supports IP Multi-cast

## Cloud_Hub
![CH](https://docs.aws.amazon.com/ko_kr/vpn/latest/s2svpn/images/AWS_VPN_CloudHub-diagram.png)
- *One VPC connect with multiple On Premise Network*
- Use VPN to establish connection

## VPC_Peering
![vp](https://docs.aws.amazon.com/vpc/latest/peering/images/peering-intro-diagram.png)
- A VPC peering connection is a networking connection between *two VPCs* that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses.

## Direct_Connect
![dc](https://docs.aws.amazon.com/directconnect/latest/UserGuide/images/direct-connect-overview.png)
- Provides a dedicated **private** connection from a remote network to your VPC
- If you want to setup a Direct Connect to one or more VPC in many different regions (same account), you must use a Direct Connect Gateway
- Data in transit is **not encrypted** but is private
- **Maximum resilience is achieved** by separate connections terminating on separate devices in more than one location 
    - [#Maximum Resiliency](https://aws.amazon.com/ko/directconnect/resiliency-recommendation/)
- 전용망 (보안성 높음)
- 도입에 비교적 시간이 소요됨

## VPC_Endpoint
- Every AWS service is publicly exposed (public URL)
- VPC Endpoints (powered by AWS PrivateLink) **allows you to connect to AWS services using a private network** instead of using the public Internet

## NAT_Instance
  - **NAT Instances** 
      - gives Internet access to EC2 instances in private subnets. Old, must be setup in a public subnet, disable Source / Destination check flag
  - **Managed by you**
  - **You must manage Security Groups**
  - **Use as Bastion Host**
  - *Support port fowarding*
  - **Must be launched in a public subnet**

## NAT_Gateway
- **Managed by AWS**
- **NAT Gateway**는 Newtwork Address Transition 네트워크 주소변환서비스
  - NAT 게이트웨이: 프라이빗 서브넷에 있는 리소스가 인터넷에 액세스할 수 있게 해주는 고가용성 관리형 네트워크 주소 변환 (NAT) 서비스입니다.
  -  Subnet 을 Public 과 Private 으로 구분하여, Public subnet은 Internet Gateway 를 이용하여 외부와 통신이 가능하도록 설정하였다. 하지만, Private Subnet 의 경우는 외부와의 통신이 단절된 환경이다.
    - Private Subnet에 위치한 instance가 다른 AWS 서비스에 연결해야 하는 경우. 
    - 인터넷에서 Private instance 에 접근 불가 조건은 유지하면서 반대로 instance 에서 외부 인터넷으로 연결이 필요한 경우. 
  -  위와 같은 이유로 Private Subnet에 배포된 instance 라도 외부와의 통신이 필요한 경우가 있다. 이런 경우 가장 간단히 해결 할 수 있는 방법은 NAT 서버를 구축하는 것이다.
  - *NAT Gateway : managed by AWS, provides scalable Internet access to private EC2 instances, IPv4 only*
  - **No Security Groups to manage / required**

## NAT - VPC with public and private subnets (NAT)
> [NAT](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html)
- The configuration for this scenario includes a virtual private cloud **(VPC) with a public subnet and a private subnet.** We recommend this scenario if you want to run a public-facing web application, while maintaining back-end servers that aren't publicly accessible. 

- A common example is a multi- tier website, with the web servers in a public subnet and the database servers in a private subnet. You can set up security and routing so that the web servers can communicate with the database servers.
The instances in the public subnet can send outbound traffic directly to the Internet, whereas the instances in the private subnet can't. 
- Instead, **the instances in the private subnet can access the Internet by using a network address translation (NAT) gateway that resides in the public subnet.**
- The database servers can connect to the Internet for software updates using the NAT gateway, but the Internet cannot establish connections to the database servers.

## Test Tips
- NAT instance/GW is used to give internet access to EC2 in private subnets.
- NAT instance/GW is always in Public Subnet.
- RT of private subnet contains a route to NAT GW/NAT instance.

  - **Choose NAT GW (AWS Managed)over NAT instance if above is satisfied.**
