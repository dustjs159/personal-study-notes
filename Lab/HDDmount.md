Add HDD + Mount 

# 하드디스크 추가하기
* Virtual Machine Settings   
![hdd1](https://user-images.githubusercontent.com/57285121/115817984-caa60800-a436-11eb-9720-d2c4ccea66df.png)   

![hdd2](https://user-images.githubusercontent.com/57285121/115818072-ef9a7b00-a436-11eb-96c5-52b97a9301b8.PNG)   

![hdd3](https://user-images.githubusercontent.com/57285121/115818103-004af100-a437-11eb-86e2-3d25164d3175.png)

![hdd4](https://user-images.githubusercontent.com/57285121/115818132-135dc100-a437-11eb-8e6d-ae91c20a30a4.PNG)

# 하드디스크 마운트하기
* 마운트 전 파티션 먼저 진행
> * ```fdisk /dev/sdb```   
> > * Command : n   
> > * Partition number : 1   
> > * First sector : enter   
> > * Last sector : enter   
> > * Command : p   
> > * Command : w   

* 파티션 후 파일시스템 생성(포맷)
> * ```mkfs -t <filesystem name> <disk>```   
![hdd5](https://user-images.githubusercontent.com/57285121/115819141-3a1cf700-a439-11eb-9792-fe1c348ac18b.PNG)

* 디렉토리에 마운트 하기
> * ```mount <disk> <mount path>```   
![hdd6](https://user-images.githubusercontent.com/57285121/115820447-c9c3a500-a43b-11eb-93fe-ff2e4c4d28b8.png)   

# 사용자 추가 후 권한 변경
* 사용자 추가
> * ```useradd <username>```   
* User정보들은 /etc/passwd에 있음   
![useradd](https://user-images.githubusercontent.com/57285121/115821767-5d967080-a43e-11eb-9c3c-55cd97e57659.PNG)

* 소유권 변경 및 부여
> * ```chown <username> <directory/file name>```   
![cho1](https://user-images.githubusercontent.com/57285121/115821907-9a626780-a43e-11eb-8317-7f7164e73afe.PNG)   

* 소유자와 그룹은 모든 권한 나머지는 읽기 권한 부여
> * ```chmod 774 <directory/filename>```   
![chm1](https://user-images.githubusercontent.com/57285121/115822244-2aa0ac80-a43f-11eb-9fa9-ab9c02ae32c8.PNG)







