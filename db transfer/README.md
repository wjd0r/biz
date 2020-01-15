

# db 이관

오라클 db이관

## 오라클 sid

 - 오라클 데이타베이스명을 확인하기
> SELECT NAME, DB_UNIQUE_NAME FROM v$database;

   
- 오라클 SID를 확인하기
   
> SELECT instance FROM v$thread;
   
- 기본 SID 확인
   
> ser ORACLE_SID
   
- 기본 SID 지정하기
   
> ser ORACLE_SID=orcl

## 오라클 백업

- 계정 조회하기  
> select username from dba_users order by username;  
- 디렉토리 조회하기  
> select * from dba_directories;  
- 덤프 expdp  
> expdp bizxpress/bizxpress directory=DATA_PUMP_DIR DUMPFILE=BIZXPRESS.DMP  
  

## 오라클 복원

- 계정 테이블 스페이스 생성  

     CREATE TABLESPACE BIZXPRESS DATAFILE 'C:\app\cyberi\oradata\orcl\BIZXPRESS.dbf' SIZE 500M;  

     CREATE TABLESPACE BIZXPRESS  
    DATAFILE 'C:\app\cyberi\oradata\orcl\BIZXPRESS.dbf' SIZE 100M 

    AUTOEXTEND ON NEXT 10M   
    DEFAULT STORAGE 
     (  
	     INITIAL 10K   
	     NEXT 10K  
	     MINEXTENTS 2   
	     MAXEXTENTS 50  
		 PCTINCREASE 50   
     );

└ □ 계정 테이블 스페이스 삭제  
└ □ DROP TABLESPACE BIZXPRESS  
INCLUDING CONTENTS AND DATAFILES  
CASCADE CONSTRAINTS;  
└ □ 오라클 유저 생성  
└ □ CREATE USER bizxpress  
IDENTIFIED BY bizxpress  
DEFAULT TABLESPACE bizxpress  
TEMPORARY TABLESPACE TEMP;  
└ □ 유저 권한  
└ □ GRANT connect, resource, dba TO bizxpress;  
└ □ 디렉토리 조회하기  
└ □ select * from dba_directories;  
└ □ 덤프 impdp  
└ □ impdp bizxpress/bizxpress directory=DATA_PUMP_DIR DUMPFILE=BIZXPR

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyMDU3MDEyNV19
-->