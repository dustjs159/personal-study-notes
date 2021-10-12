AWS EC2 Auto Scaling 
====================================
## Summary
- Last Updated : 21.10.05 Tue   
- Updated by : YEONSUN YOON
-----------------------------------

# AWS EC2 Auto Scaling
   
<img width="313" alt="스크린샷 2021-09-23 오후 1 05 32" src="https://user-images.githubusercontent.com/57285121/134453158-68a1ba22-a90e-4f70-9f5b-3b1ba696bc44.png">
   
- 클라이언트의 요청이 증가하게 되면 서버의 대수를 늘리고(Scale-Out) 감소하게 되면 서버의 대수를 줄이는(Scale-Down) 기능
- 인스턴스로 들어오는 트래픽에 따라 **유연한 인스턴스 구성이 가능**
- **Auto Scaling Group(인스턴스의 집합)** 을 생성하고 그룹에 인스턴스의 최소 및 최대 대수를 설정
- Auto Scaling Group내 인스턴스들의 대수는 그룹에 설정된 최소 대수(Minimum Size)값 밑으로 내려가지 않고 최대 대수(Maximum Size)값을 넘지 않음(위 그림에서는 최소 대수가 1, 최대 대수가 4)
- 
