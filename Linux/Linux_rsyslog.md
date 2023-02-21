💻 [Linux] rsyslog
=================

# rsyslog
* remote syslog
* `rsyslogd` 데몬 프로세스가 `rsyslog.conf` 설정 파일을 참조하여 지정한 로그 파일, 콘솔 또는 외부 서버 등에 로그를 기록
* 설정 파일
    * `/etc/rsyslog.conf`
    * `/etc/rsyslog.d`

## rsyslog의 template을 이용하여 로그 파일의 String을 parsing
* 로그를 수집하고, 수집한 로그를 바탕으로 모니터링(reqeust/response 간 latency 측정 등)하기 위해 로그가 저장되는 형식을 통일화 하고자 할 때 사용
* `systemd` 내에서 작동중인 app은 `/var/log/syslog` 에 쓰지 않고 특정 디렉토리에 로그를 생성하도록 한다.
    * `[Service]` 섹션 내 `SyslogIdentifier` 에 syslog tag를 붙여줌.
```vim
...
[Service]
SyslogIdentifier=app
...
```

* `/etc/rsyslog.d` 경로 내에 `app.conf` 파일을 생성하고 아래의 내용을 작성
    * 파일 이름은 상관 없다. `*.conf` 형식만 맞춰주면 된다.

```vim
$template customformat, "%msg%\n"
if $programname == '{app}' then {
  action (
      type="omfile"
      file="/data/{app}.log"
      template="customformat"
    )
    stop
}
```