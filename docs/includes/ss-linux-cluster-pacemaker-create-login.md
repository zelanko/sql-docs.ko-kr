1. **모든 SQL Server에서 Pacemaker를 위한 서버 로그인을 만듭니다**. 다음 Transact-SQL이 로그인을 만듭니다.

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   또는 더 세부적인 수준에서 권한을 설정할 수 있습니다. Pacemaker 로그인에는 가용성 그룹 관리를 위한 변경, 제어 및 보기 정의 권한을 비롯하여 로그인을 통해 sp_server_diagnostics를 실행하기 위한 서버 상태 보기가 필요합니다. 자세한 내용은 [가용성 그룹 사용 권한 부여(Transact SQL)](http://msdn.microsoft.com/library/hh968934.aspx) 및 [sp_server_diagnostic 권한](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql#permissions)을 참조하세요.

   다음 Transact-SQL은 Pacemaker 로그인에 필요한 권한을 부여합니다. 이 문에서 아래 'ag1'은 클러스터 리소스로 추가될 가용성 그룹의 이름입니다.

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   GRANT VIEW SERVER STATE TO pacemakerLogin
   ```

1. **모든 SQL Server에서 SQL Server 로그인을 위한 자격 증명을 저장합니다**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
