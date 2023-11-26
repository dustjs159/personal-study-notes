pyenv를 활용한 파이썬 개발환경 구축
=================================
* `pyenv` 와 `pyenv-virtualenv` 를 통해 개발환경 구축하기.
* github : https://github.com/pyenv

### Mac OS에서 `brew` 패키지 관리자를 통한 설치 방법
```sh
$ brew update
$ brew install pyenv
$ brew install pyenv-virtualenv
```
설치 후 현재 사용중인 zsh에 `PATH` 인식을 위해 `~/.zshrc` 편집
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/shims:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```
편집 후 `$ source ~/.zshrc`

```
$ pyenv install [사용할 버전]

# 이때 추가 설치 했던 것
$ brew install xz

# 특정 프로젝트에 버전 지정
$ cd [project name]
$ pyenv local [python version]

# pyenv-virtualenv로 가상환경 설정
$ pyenv virtualenv [venv 이름] # 가상환경 생성

$ pyenv shell [venv 이름] # 해당 디렉토리에서 가상 환경 Shell 실행
```

- 참조 : https://wikidocs.net/10936#macos-pyenv-pyenv-virtualenv