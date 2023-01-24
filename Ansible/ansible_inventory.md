💻 [Ansible] Ansible Inventory 구성하기
=========================
* Inventory는 Control Node의 작업 대상 목록
    * Control Node가 참조할 Inventory 파일의 경로는 `/etc/ansible/ansible.cfg` 에서 지정할 수 있다.
        * default는 `/etc/ansible/hosts` 파일로 설정되어 있음
* 여러 매개 변수를 통해 Inventory 내 Host의 정보(IP, private key 경로 등)를 저장할 수 있다.
    * 매개 변수의 종류
```
ansible_host : 대상 서버의 호스트명 or IP 주소
ansible_port : 대상 서버에 SSH 접속할 포트 (default는 당연히 22다.)
ansible_user : 대상 서버에 SSH 접속할 user
ansible_private_key_file : SSH 접속을 위한 마스터 서버의 Private Key 경로
```