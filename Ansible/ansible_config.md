💻 [Ansible] Ansible config 파일 알아보기
=======================================

* Ansible이 설치된 서버의 `/etc/ansible/ansible.cfg` 파일 구조 살펴보기

```
[defaults]
inventory = /etc/ansible/hosts
...

[privilege_escalation] # root로 실행할 필요가 있을 때
#become=True
#become_method=sudo
#become_user=root
#become_ask_pass=False
```

* `become` 이란, 특정 User가 될 것(become)인지 여부를 결정
* `become_user` 는 되고자 하는 특정 User를 설정
