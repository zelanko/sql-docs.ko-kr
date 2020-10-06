## <a name="prerequisites"></a>사전 요구 사항

가용성 그룹을 만들려면 먼저 다음을 수행해야 합니다.

- 가용성 복제본을 호스트하는 모든 서버가 통신할 수 있도록 환경을 설정합니다.
- SQL Server를 설치합니다. 자세한 내용은 [SQL Server 설치](../database-engine/install-windows/install-sql-server.md)를 참조합니다.

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>AlwaysOn 가용성 그룹을 사용하도록 설정하고 mssql-server 다시 시작

>[!NOTE]
>다음 명령은 PowerShell 갤러리에 게시되는 sqlserver 모듈에서 cmdlet을 활용합니다. Install-Module 명령을 사용하여 이 모듈을 설치할 수 있습니다.

SQL Server 인스턴스를 호스트하는 각 복제본에서 AlwaysOn 가용성 그룹을 사용하도록 설정합니다. 그런 다음, SQL Server 서비스를 다시 시작합니다. 다음 명령을 실행하여 SQL Server 서비스를 사용하도록 설정한 다음, 다시 시작합니다.

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwayson_health-event-session"></a>AlwaysOn_health 이벤트 세션을 사용하도록 설정

 가용성 그룹 문제를 해결할 때 근본적인 원인 진단에 도움을 주려면 Always On 가용성 그룹 확장 이벤트(XEvents) 세션을 사용하도록 설정하여 줄 수 있습니다. 그렇게 하려면 SQL Server의 각 인스턴스에서 다음 명령을 실행합니다.

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

이 XEvent 세션에 대한 자세한 내용은 [Always On 가용성 그룹 확장 이벤트](../database-engine/availability-groups/windows/always-on-extended-events.md)를 참조하세요.

## <a name="database-mirroring-endpoint-authentication"></a>데이터베이스 미러링 엔드포인트 인증

동기화가 제대로 작동하려면 읽기-배율 가용성 그룹에 관련된 복제본은 엔드포인트에 대한 인증이 필요합니다. 이러한 인증에 사용할 수 있는 두 가지 주요 시나리오는 다음 섹션에서 다룹니다.

### <a name="service-account"></a>서비스 계정

모든 보조 복제본이 동일한 도메인에 조인된 Active Directory 환경에서 SQL Server는 서비스 계정을 사용하여 인증할 수 있습니다. SQL Server 인스턴스 각각에서 서비스 계정에 대한 로그인을 명시적으로 만들어야 합니다.

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>SQL 로그인 인증

보조 복제본이 Active Directory 도메인에 조인될 수 없는 환경에서 SQL 인증을 활용해야 합니다. 다음 Transact-SQL 스크립트는 `dbm_login`이라는 로그인과 `dbm_user`라는 사용자를 만듭니다. 강력한 암호로 스크립트를 업데이트합니다. 데이터베이스 미러링 엔드포인트 사용자를 만들려면 모든 SQL Server 인스턴스에서 다음 명령을 실행합니다.

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>인증서 인증

SQL 인증으로 인증을 요구하는 보조 복제본을 사용하는 경우 미러링 엔드포인트 간의 인증을 위한 인증서를 사용합니다.

다음 Transact-SQL 스크립트는 마스터 키와 인증서를 만듭니다. 그런 다음, 인증서를 백업하고 프라이빗 키로 파일을 보호합니다. 강력한 암호로 스크립트를 업데이트합니다. 기본 SQL Server 인스턴스에서 스크립트를 실행하여 인증서를 만듭니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

이제 기본 SQL Server 복제본은 `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer`에 인증서, `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk`에 프라이빗 키가 있습니다. 이러한 두 파일을 가용성 복제본을 호스트할 모든 서버의 동일한 위치로 복사합니다.

각 보조 복제본에서 SQL Server에 대한 서비스 계정에 인증서에 액세스할 권한이 있는지 확인합니다.

#### <a name="create-the-certificate-on-secondary-servers"></a>보조 서버에서 인증서 만들기

다음 Transact-SQL 스크립트는 기본 SQL Server 복제본에 대해 만든 백업을 사용하여 마스터 키와 인증서를 만듭니다. 이 명령은 사용자에게 인증서에 액세스할 권한도 부여합니다. 강력한 암호로 스크립트를 업데이트합니다. 해독 암호는 이전 단계에서 *.pvk* 파일을 만들 때 사용한 암호와 동일합니다. 인증서를 만들려면 모든 보조 복제본에서 다음 스크립트를 실행합니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>모든 복제본에서 데이터베이스 미러링 엔드포인트 만들기

데이터베이스 미러링 엔드포인트는 TCP(전송 제어 프로토콜)를 사용하여 데이터베이스 미러링 세션에 참여하거나 가용성 복제본을 호스트하는 서버 인스턴스 간에 메시지를 보내고 받습니다. 데이터베이스 미러링 엔드포인트는 고유의 TCP 포트 번호에서 수신합니다.

다음 Transact-SQL 스크립트는 가용성 그룹에 대해 수신하는 엔드포인트 `Hadr_endpoint`를 만듭니다. 엔드포인트를 시작하고 이전 단계에서 만든 SQL 로그인 또는 서비스 계정에 연결 권한을 부여합니다. 스크립트를 실행하기 전에 `**< ... >**` 사이의 값을 바꿉니다. 필요에 따라 IP 주소 `LISTENER_IP = (0.0.0.0)`을 포함할 수 있습니다. 수신기 IP 주소는 IPv4 주소여야 합니다. 또한 `0.0.0.0`을 사용할 수 있습니다.

모든 SQL Server 인스턴스에서 환경에 대한 다음 Transact-SQL 스크립트를 업데이트합니다.

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

방화벽의 TCP 포트를 수신기 포트용으로 열어 두어야 합니다.

자세한 내용은 [데이터베이스 미러링 엔드포인트(SQL Server)](../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md?view=sql-server-2017)를 참조하세요.