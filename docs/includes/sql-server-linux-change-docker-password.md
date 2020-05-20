**SA** 계정은 설치 중에 생성되는 SQL Server 인스턴스의 시스템 관리자입니다. SQL Server 컨테이너를 만든 후 컨테이너에서 `echo $MSSQL_SA_PASSWORD`를 실행하여 지정한 `MSSQL_SA_PASSWORD` 환경 변수를 검색할 수 있습니다. 보안을 위해 다음과 같이 SA 암호를 변경합니다.

1. SA 사용자에게 사용할 강력한 암호를 선택합니다.

1. Transact-SQL 문을 통해 암호를 변경하려면 `docker exec`을 사용하여 **sqlcmd** 유틸리티를 실행합니다. `<YourStrong!Passw0rd>` 및 `<YourNewStrong!Passw0rd>`를 사용자 고유의 암호 값으로 바꿉니다.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
