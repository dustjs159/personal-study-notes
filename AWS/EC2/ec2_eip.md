💻 [AWS] EC2 Elastic IP
===================

* **Elastic IP** : 탄력적 IP 
  * AWS로 부터 할당받을 수 있는 **Public IP**
  * Elastic IP가 할당되는 단위는 Network Interface.
  * Elastic IP를 탄력적으로 다른 인스턴스에게 연결이 가능(붙였다 뗐다가 가능함)

Public IP를 자동으로 할당하는 Subnet에 배치되어 할당받은 Public IP와의 차이점은 Public IP의 유동성 차이가 있다. Elastic IP가 아닌 Public IP를 할당받은 인스턴스를 재시작하면 Public IP가 바뀔 수 있기 때문에(99% 확률로 바뀐다.) IP WhiteList 등록이 필요하거나 특정 Outbound 트래픽만 허용해야할 경우가 발생했을 때 Elastic IP를 사용하도록 한다.

![](https://images.velog.io/images/dustjs159/post/66e28f4b-f091-432b-ad5d-76b3c045a79f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-10%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.52.44.png)

(Elastic IP가 아닌 Public IP를 할당했을 때)


# Elastic IP의 비용이 발생하는 경우

할당받은 Elastic IP를 인스턴스에 연결하여 사용중이라면 비용이 발생하지 않는다. 그러나 한정된 Public IPv4 주소를 낭비 없이 효율적으로 사용하기 위해 할당받은 Elastic IP가 인스턴스의 Network Interface에 연결되어 있지 않거나 중지된 인스턴스에 연결되어 있는 경우에는 추가 비용이 발생한다.
