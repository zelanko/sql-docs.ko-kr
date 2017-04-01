---
title: "Oracle 게시자 문제 해결 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Oracle 게시 [SQL Server 복제], 문제 해결"
  - "문제 해결 [SQL Server 복제], Oracle 게시"
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
caps.latest.revision: 62
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 62
---
# Oracle 게시자 문제 해결
  이 항목에서는 Oracle 게시자를 구성 및 사용할 때 발생할 수 있는 여러 가지 문제를 나열합니다.  
  
## Oracle 클라이언트 및 네트워킹 소프트웨어와 관련된 오류가 발생했습니다.  
 계정에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 실행 해야 수 부여에 읽기 및 실행 디렉터리 (및 모든 하위 디렉터리)에 대 한 권한을 Oracle 클라이언트 네트워킹 소프트웨어가 설치 되어 있습니다. 사용 권한이 부여되지 않거나 Oracle 클라이언트 구성 요소가 제대로 설치되지 않으면 다음과 같은 오류 메시지가 표시됩니다.  
  
 "[Microsoft OLE DB Provider for Oracle]로 서버에 연결하지 못했습니다. Oracle 클라이언트 및 네트워킹 구성 요소를 찾을 수 없습니다. 이러한 구성 요소는 Oracle 버전 7.3.3 이상의 클라이언트 소프트웨어 설치의 일부로 Oracle사에서 제공합니다. 이러한 구성 요소를 설치해야 공급자를 사용할 수 있습니다."  
  
 해당 Oracle 클라이언트가 배포자에 설치된 경우 클라이언트 설치가 완료된 후에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 중지되었다가 다시 시작되었는지 확인합니다. 이렇게 해야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 클라이언트 구성 요소를 인식할 수 있습니다.  
  
 권한을 부여하고 구성 요소를 올바르게 설치한 다음에도 이 오류가 계속 발생하면 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI의 레지스트리 설정이 올바른지 확인하십시오.  
  
-   Oracle 10g의 경우 올바른 설정은 다음과 같습니다.  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Oracle 9i의 경우 올바른 설정은 다음과 같습니다.  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## SQL Server 배포자가 Oracle 데이터베이스 인스턴스에 연결할 수 없습니다.  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자가 Oracle 게시자에 연결할 수 없는 경우 다음 사항을 확인하십시오.  
  
-   필요한 Oracle 소프트웨어가 배포자에 설치되어 있어야 합니다.  
  
-   Oracle 데이터베이스가 온라인 상태이고 SQL*Plus와 같은 도구를 사용하여 이 데이터베이스에 연결할 수 있어야 합니다.  
  
-   복제에서 Oracle 게시자 연결에 사용하는 로그인에 충분한 권한이 있어야 합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
-   Oracle 게시자를 구성하는 동안 정의된 TNS 이름이 tnsnames.ora 파일에 나열되어 있어야 합니다.  
  
-   올바른 Oracle 홈 및 경로를 사용해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 하나의 Oracle 바이너리 집합만 설치한 경우에도 Oracle 홈과 관련된 환경 변수를 제대로 설정해야 합니다. 환경 변수 값을 변경한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 중지하고 다시 시작하여 변경 내용을 적용해야 합니다.  
  
 구성 및 연결을 테스트 하는 방법에 대 한 자세한 내용은 참조 하십시오. "설치 및 구성에 Oracle 클라이언트 네트워킹 소프트웨어는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자"에서 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
## Oracle 게시자가 다른 배포자와 연결되어 있습니다.  
 Oracle 게시자는 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에만 연결할 수 있습니다. Oracle 게시자에 배포자가 연결되어 있는 경우 다른 배포자를 사용하려면 먼저 기존 배포자를 삭제해야 합니다. 기존 배포자를 먼저 삭제하지 않으면 다음 오류 메시지 중 하나가 표시됩니다.  
  
-   "Oracle 서버 인스턴스 ' \<*OraclePublisherName*>'를 사용 하도록 이전에 구성 된 ' \<*SQLServerDistributorName*>' 배포자로 합니다. 사용을 시작 하려면 ' \<*NewSQLServerDistributorName*>'의 배포자로 서버 인스턴스에 있는 모든 게시를 삭제 하는 Oracle 서버 인스턴스의 현재 복제 구성을 제거 해야 합니다. "  
  
-   "Oracle 서버 ' \<*OracleServerName*>' 게시자로 이미 정의 되어 ' \<*OraclePublisherName*>' 배포자에 ' \<*SQLServerDistributorName*>.*\< DistributionDatabaseName>*'. 게시자를 삭제 하거나 공용 동의어 '*\< SynonymName>*' 다시 만들어야 합니다. "  
  
 Oracle 게시자를 삭제하면 Oracle 데이터베이스의 복제 개체가 자동으로 정리됩니다. 그러나 어떤 경우에는 Oracle 복제 개체를 수동으로 정리해야 합니다. 복제에 의해 생성된 Oracle 복제 개체를 수동으로 정리하려면 다음을 수행하십시오.  
  
1.  DBA 권한으로 Oracle 게시자에 연결합니다.  
  
2.  SQL 명령 `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`를 실행합니다.  
  
3.  SQL 명령 `DROP USER <replication_administrative_user_schema>``CASCADE;`를 실행합니다.  
  
## PRIMARY KEY 부재와 관련된 SQL Server 오류 21663이 발생했습니다.  
 트랜잭션 게시의 아티클에는 올바른 기본 키가 있어야 합니다. 아티클에 올바른 기본 키가 없으면 아티클을 추가할 때 다음 오류 메시지가 표시됩니다.  
  
 "원본 테이블에 대 한 올바른 기본 키를 찾을 [\<*TableOwner*>]. [ \<*TableName*>] "  
  
 기본 키 요구 사항에 대한 자세한 내용은 [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)항목의 "고유 인덱스 및 UNIQUE 제약 조건" 섹션을 참조하십시오.  
  
## 연결된 서버로의 중복 로그인과 관련된 SQL Server 오류 21642가 발생했습니다.  
 Oracle 게시자를 처음 구성하면 게시자와 배포자 간 연결에 대해 연결된 서버 항목이 생성됩니다. 연결된 서버의 이름은 Oracle TNS 서비스 이름과 동일합니다. 이름이 동일한 연결된 서버를 만들면 다음 오류 메시지가 표시됩니다.  
  
 "유형이 다른 게시자에는 연결된 서버가 필요합니다. 연결 된 서버 '*\< LinkedServerName>*' 이미 있습니다. 연결된 서버를 제거하거나 다른 게시자 이름을 선택하십시오."  
  
 이 오류는 연결된 서버를 직접 만들거나 이전에 삭제한 Oracle 게시자와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자 간 관계를 다시 구성하려고 하는 경우 발생할 수 있습니다. 게시자를 다시 구성 하는 동안이 오류가 나타나면와 연결 된 서버를 삭제할 [sp_dropserver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)합니다.  
  
 연결 된 서버 연결을 통해 Oracle 게시자에 연결 하려면 다른 TNS 서비스 이름을 만들고 호출할 때이 이름을 사용 하 여 [sp_addlinkedserver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)합니다. TNS 서비스 이름을 만드는 방법은 Oracle 설명서를 참조하십시오.  
  
## SQL Server 오류 21617이 발생했습니다.  
 Oracle 게시는 Oracle 응용 프로그램 SQL*PLUS를 사용하여 게시자 지원 코드 패키지를 Oracle 데이터베이스로 다운로드합니다. Oracle 게시자를 구성 하기 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 확인이 SQL\*PLUS에 배포자에서 시스템 경로로 액세스할 수 있습니다. 하는 경우 SQL\*더한 다음 오류 메시지가 표시 됩니다 로드할 수 없습니다.  
  
 "SQL*PLUS를 실행할 수 없습니다. 배포자에 최신 버전의 Oracle 클라이언트 코드가 설치되었는지 확인하십시오."  
  
 SQL을 찾으려고\*PLUS 배포자에 있습니다. Oracle 10g 클라이언트 설치의 경우 이 실행 파일의 이름은 sqlplus.exe입니다. 이 파일은 일반적으로 %ORACLE_HOME%/bin에 설치됩니다. 확인할 SQL의 경로\*표시 및 시스템 변수의 값을 검사 하는 시스템 경로에 **경로**:  
  
1.  마우스 오른쪽 단추로 클릭 **내 컴퓨터**, 를 클릭 하 고 **속성**합니다.  
  
2.  **고급** 탭을 클릭한 다음 **환경 변수**를 클릭합니다.  
  
3.  **환경 변수** 대화 상자의 **시스템 변수** 목록에서 **Path** 변수를 선택한 다음 **편집**을 클릭합니다.  
  
4.  **시스템 변수 편집** 대화 상자에서 sqlplus.exe가 들어 있는 폴더의 경로가 **변수 값** 입력란에 나타나지 않으면 해당 문자열을 편집하여 추가합니다.  
  
5.  열려 있는 각 대화 상자에서 **확인** 을 클릭하여 변경 내용을 저장하고 종료합니다.  
  
 배포자에서 sqlplus.exe를 찾을 수 없으면 배포자에 최신 버전의 Oracle 클라이언트 소프트웨어를 설치합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
## SQL Server 오류 21620이 발생했습니다.  
 Oracle 데이터베이스 8.1 이전 버전에 연결하는 경우 Oracle 게시를 위해 배포자에 설치된 Oracle 클라이언트 소프트웨어는 버전 9여야 합니다. Oracle 데이터베이스 8.1 이후 버전에 연결하는 경우에는 버전 10 이상의 Oracle 클라이언트 소프트웨어를 사용하는 것이 좋습니다.  
  
 Oracle 게시는 Oracle 게시자를 구성하기 전에 배포자에서 시스템 경로로 액세스할 수 있는 SQL*PLUS가 버전 9 이상인지 확인합니다. 버전 9 이상이 아니면 다음 오류 메시지가 표시됩니다.  
  
 "시스템 경로 변수로 액세스할 수 있는 SQL*PLUS 버전이 최신 버전이 아니어서 Oracle 게시를 지원할 수 없습니다. 배포자에 최신 버전의 Oracle 클라이언트 코드가 설치되었는지 확인하십시오."  
  
 여러 버전의 Oracle 클라이언트 소프트웨어가 배포자에 설치되어 있을 경우 최신 버전이 버전 9 이상이며 시스템 경로 변수가 먼저 이 버전을 가리키는지 확인하십시오. 최신 버전이 먼저 표시되기만 하면 다른 버전에 대한 참조도 표시될 수 있습니다. 시스템 경로 변수를 편집하는 방법은 이 항목의 앞부분에 있는 "SQL Server 오류 21617이 발생합니다" 섹션을 참조하십시오.  
  
## SQL Server 오류 21624 또는 오류 21629가 발생했습니다.  
 64비트 배포자의 경우 Oracle 게시는 Oracle OLEDB 공급자(OraOLEDB.Oracle)를 사용합니다. 배포자에 Oracle OLEDB 공급자가 설치 및 등록되었는지 확인하십시오. 공급자가 설치 및 등록되어 있지 않으면 다음 오류 메시지 중 하나 또는 둘 다가 표시됩니다.  
  
-   "배포자 '%s'에서 Oracle OLEDB 공급자 OraOLEDB.Oracle을 찾을 수 없습니다. 배포자에 최신 버전의 Oracle OLEDB 공급자가 설치 및 등록되었는지 확인하십시오."  
  
-   "Oracle OLEDB 공급자 OraOLEDB.Oracle이 등록되었음을 나타내는 CLSID 레지스트리 키가 배포자에 없습니다. 배포자에 Oracle OLEDB 공급자가 설치 및 등록되었는지 확인하십시오."  
  
 Oracle 클라이언트 소프트웨어 버전 10g를 사용하는 경우 공급자는 OraOLEDB10.dll입니다. 버전 9i의 경우에는 OraOLEDB.dll입니다. 공급자는 %ORACLE_HOME%\BIN에 설치됩니다(예: C:\oracle\product\10.1.0\Client_1\bin). 배포자에 Oracle OLEDB 공급자가 설치되어 있지 않으면 Oracle에서 제공한 Oracle 클라이언트 소프트웨어 설치 디스크에서 설치합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
 Oracle OLEDB 공급자가 설치되어 있으면 등록되었는지 확인하십시오. 공급자 DLL을 등록하려면 DLL이 설치된 디렉터리에서 다음 명령을 실행한 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 중지했다가 다시 시작합니다.  
  
1.  `regsvr32 OraOLEDB10.dll` 또는 `regsvr32 OraOLEDB.dll`입니다.  
  
## SQL Server 오류 21626 또는 오류 21627이 발생했습니다.  
 Oracle 게시 환경이 올바로 구성되었는지 확인하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 구성 중에 지정한 로그인 자격 증명을 사용하여 Oracle 게시자에 연결합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자가 Oracle 게시자에 연결할 수 없는 경우 다음 오류 메시지가 표시됩니다.  
  
-   "Oracle OLEDB 공급자 OraOLEDB.Oracle을 사용하여 Oracle 데이터베이스 서버 '%s'에 연결할 수 없습니다."  
  
 이 오류 메시지가 표시되면 Oracle 게시자 구성 중에 지정한 로그인 및 암호로 직접 SQL*PLUS를 실행하여 Oracle 데이터베이스에 대한 연결을 확인합니다. 자세한 내용은 이 항목의 앞부분에 있는 "SQL Server 배포자가 Oracle 데이터베이스 인스턴스에 연결할 수 없습니다" 섹션을 참조하십시오.  
  
## SQL Server 오류 21628이 발생했습니다.  
 64비트 배포자의 경우 Oracle 게시는 Oracle OLEDB 공급자(OraOLEDB.Oracle)를 사용합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 Oracle 공급자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]프로세스에서 실행되도록 허용하기 위해 레지스트리 항목을 만듭니다. 이 레지스트리 항목을 읽거나 쓰는 데 문제가 있으면 다음 오류 메시지가 표시됩니다.  
  
 "Oracle OLEDB 공급자 OraOLEDB.Oracle이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]프로세스에서 실행되도록 허용하기 위해 배포자 '%s'의 레지스트리를 업데이트할 수 없습니다. 현재 로그인에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 소유 레지스트리 키를 수정할 권한이 부여되었는지 확인하십시오."  
  
 Oracle 게시는 레지스트리 항목이 있어야 하며 64비트 배포자의 경우 **1** 로 설정되어야 합니다. 항목이 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 항목을 만듭니다. 항목이 있지만 **0**으로 설정된 경우에는 설정이 변경되지 않으며 Oracle 게시자 구성이 실패합니다.  
  
 레지스트리 설정을 보고 수정하려면  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **실행** 대화 상자에 **regedit**를 입력한 다음 **확인**을 클릭합니다.  
  
3.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server로 이동할\\*\< 인스턴스 이름>*\Providers 합니다.  
  
     Providers 아래에는 OraOLEDB.Oracle 폴더가 있어야 하며 이 폴더 내에 이름이 **AllowInProcess**이고 값이 **1**인 DWORD 값이 있어야 합니다.  
  
4.  **AllowInProcess** 가 **0**으로 설정되어 있으면 레지스트리 항목을 **1**로 업데이트합니다.  
  
    1.  항목을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **수정**합니다.  
  
    2.  **문자열 편집** 대화 상자의 **값 데이터** 필드에 **1** 을 입력합니다.  
  
## SQL Server 오류 21684가 발생했습니다.  
 관리 사용자 계정에 충분한 권한이 없으면 다음 오류 메시지가 표시됩니다.  
  
 “Oracle 게시자 '%s'의 관리자 로그인과 연관된 사용 권한이 충분하지 않습니다.”  
  
 사용자에게 부여된 사용 권한을 확인하려면 `SELECT * from session_privs`쿼리를 실행합니다. 출력은 다음과 같은 형태가 됩니다.  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## 복제 사용자 스키마에 대한 사용 권한 문제가 발생했습니다.  
 복제 사용자 스키마에서 "만들기 수동으로 사용자 스키마"에 설명 된 권한이 있어야 합니다. [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
## Oracle 오류 ORA-01000  
 복제는 게시에 아티클을 추가할 때 Oracle 게시자에 커서를 사용합니다. 이때 게시자에서 사용할 수 있는 최대 커서 수가 초과되어 다음 오류가 발생할 수 있습니다.  
  
 "ORA-01000: maximum open cursors exceeded"  
  
 이 문제를 방지 하려면는 **max_open_cursors** Oracle 데이터베이스에서 설정을 충분히 높은 수 (최소 1000)로 설정 합니다. 이 설정에 대한 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
## Oracle 오류 ORA-01555  
 다음 Oracle 데이터베이스 오류는 스냅숏 복제와는 관계가 없으며 Oracle에서 일관된 읽기를 수행할 수 있는 데이터 뷰를 생성하는 방식과 관련되어 있습니다.  
  
 "ORA-01555: 너무 오래된 스냅숏"  
  
 Oracle에서는 롤백 세그먼트라는 개체를 사용하여 SQL 문이 실행된 시점에서 일관된 읽기를 수행할 수 있는 데이터 뷰를 생성합니다. 다른 동시 세션에서 롤백 정보를 덮어쓰는 경우 "snapshot too old" 오류가 발생할 수 있습니다. Oracle 9i 이전에서는 이 오류의 발생 빈도를 줄이기 위해 롤백 세그먼트의 크기 및/또는 수를 늘리고 큰 트랜잭션을 특정 롤백 세그먼트에 할당하는 방법이 권장되었습니다.  
  
 Oracle 9i에서는 롤백 세그먼트를 대체하는 UNDO 테이블스페이스 개념을 도입했습니다. Oracle 9i에서 "snapshot too old" 오류를 방지하려면 다음을 수행하십시오.  
  
-   사용 가능한 공간을 적절히 지정한 다음 UNDO 테이블스페이스를 만듭니다.  
  
-   테이블스페이스에 보존이 보장되는 기간을 설정합니다(Oracle 10G 이상).  
  
-   Oracle 초기화 매개 변수인 UNDO_MANAGEMENT 및 UNDO_RETENTION을 구성합니다.  
  
 "snapshot too old" 오류 방지 방법에 대한 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
## Oracle 오류 ORA-22285  
 테이블에 BFILE 열이 포함되어 있는 경우에는 이 열의 데이터가 파일 시스템에 저장됩니다. 다음 구문을 사용하여 복제 관리 사용자 계정에 데이터가 저장되어 있는 디렉터리에 대한 액세스 권한을 부여해야 합니다.  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 액세스 권한을 부여하지 않으면 로그 판독기 에이전트에서 다음 오류를 표시합니다.  
  
 "ORA-22285: non-existent directory or file for FILEOPEN operation"  
  
## 게시자를 다시 구성해야 하는 변경 내용이 적용되었습니다.  
 복제 메타데이터 테이블 또는 프로시저를 변경하면 게시자를 삭제하고 다시 구성해야 합니다. 게시자를 다시 구성하려면 게시자를 삭제하고 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL 또는 RMO를 사용하여 다시 구성해야 합니다. 게시자를 구성 하는 방법에 대 한 정보를 참조 하십시오. [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
 **Oracle 게시자를 삭제 하려면 (**SQL Server Management Studio**)**  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 에서 Oracle 게시자에 대한 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **복제**, 를 클릭 하 고 **배포자 속성**합니다.  
  
3.  **배포자 속성** 대화 상자의 **게시자** 페이지에서 Oracle 게시자에 대한 확인란의 선택을 취소합니다.  
  
4.  **확인**을 클릭합니다.  
  
 **Transact-SQL을 사용하여 Oracle 게시자를 삭제하려면**  
  
-   실행 **sp_dropdistpublisher**합니다. 자세한 내용은 참조 [sp_dropdistpublisher (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)합니다.  
  
## 참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  