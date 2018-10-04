1. **모든 SQL Server에서 Pacemaker를 위한 서버 로그인을 만듭니다**. 다음 Transact-SQL이 로그인을 만듭니다.

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  가용성 그룹을 만들 당시의 pacemaker를 만든 후 하지만 모든 노드를 추가 하기 전에 가용성 그룹에 대 한 ALTER, CONTROL 및 VIEW DEFINITION 권한을 해야 합니다.

1. **모든 SQL Server에서 SQL Server 로그인을 위한 자격 증명을 저장합니다**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
