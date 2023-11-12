pyenv를 활용한 파이썬 버전 관리
=================================

* github : https://github.com/pyenv

Mac OS
```sh
$ brew update
$ brew install pyenv
$ brew install pyenv-virtualenv

$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

$ source ~/.zshrc

$ pyenv install {사용할 버전}

# 이때 추가 설치 했던 것
$ brew install xz

# 특정 디렉토리에 버전 지정
$ pyenv local {python version}

# pyenv-virtualenv로 가상환경 설정
$ pyenv virtualenv venv # 가상환경 생성

$ pyenv shell venv # 해당 디렉토리에서 가상 환경 설정
```

