`2020.01.22`
`wjd0r@naver.com`

<select>
  <option value="">home</option>
</select>&nbsp;&nbsp;
<select>
  <option value="">mysql</option>
  <option value="">java</option>
</select>&nbsp;&nbsp;
<select>
  <option value="">mysql 설치</option>
</select>

# MySQL 설치

- version : 5.7.28

## IntelliJ IDEA 에서 database 연결

timezone의 설정문제로 연결이 되지 않는 현상이 발생
```
Server returns invalid timezone. Go to 'Advanced' tab and 'serverTimezone' property manually.
```
time zone 확인 쿼리
```
SELECT @@global.time_zone, @@session.time_zone;
```
또 다른 에러 메시지가 발생
```
ERROR 2013 (HY000) : Lost connection to MySQL server during query
```
워크벤치에서 아래 설정을 통해 애러 해결
```
Edit → Preferences → SQL Editor → DBMS connection read time out (in seconds): 600
```
하지만 timezone 이 system으로 되어 있으며,
이 상태에서는 여전히 IntelliJ IDEA에서는 연결이 되지 않음

다만 아래와 같이 연결설정을 하면 연결이 됨
```
Data Sources and Drivers > Advanced > serverTimezone : UTC
```

다만 근본적인 timezone을 변경하기 위해서는 아래와 같은 설정이 필요
```
set time_zone="Asia/Seoul"
ERROR 1298 (HY000): Unknown or incorrect time zone: 'Asia/Seoul'
```
애러가 뜨는 경우 아래의 링크에서 Non POSIX with leap seconds 다운
```
https://dev.mysql.com/downloads/timezones.html
```
압출풀어 mysql 스키마에서 실행 후

mysql 경로의 my.ini 파일의 마지막 부분에 아래 문장 추가
```
default-time-zone=Asia/Seoul
```
서버를 재시작 후

time zone 확인 쿼리를 실행해보면 정상적으로 변경된 것을 확인 가능


타 pc에서 똑같은 설치를 하는데 my.ini이 없어서 아래와 같이 명령어를 날려줘도 같은 세팅이 가능했음
```
set time_zone="Asia/Seoul"
set global time_zone="Asia/Seoul"
```

위의 time_zone까지 세팅이 되면
IntelliJ IDEA에서 접속해도 접속 가능


## 사용자 추가
```
create user 'bizadmin'@'localhost' identified by 'bizadmin';
```

## db 권한 부여
```
grant all privileges on *.* to 'bizadmin'@'localhost';
```

## databse 생성
```
CREATE DATABASE biztest;
```
