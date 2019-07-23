---
title: Oracle 구독자 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e7ee336c9f81c8d4258e16cf09aa9ffec177e0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110950"
---
# <a name="oracle-subscribers"></a>Oracle 구독자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 Oracle에서 제공하는 Oracle OLE DB 공급자를 통해 Oracle에 밀어넣기 구독을 지원합니다.  
  
## <a name="configuring-an-oracle-subscriber"></a>Oracle 구독자 구성  
 Oracle 구독자를 구성하려면 다음 단계를 수행하십시오.  
  
1.  배포자에서 Oracle 구독자에 연결할 수 있도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 Oracle 클라이언트 네트워킹 소프트웨어 및 Oracle OLE DB 공급자를 설치하고 구성합니다. Oracle 클라이언트 네트워킹 소프트웨어는 사용 가능한 최신 버전이어야 합니다. Oracle에서는 최신 버전의 클라이언트 소프트웨어를 설치할 것을 권장합니다. 따라서 클라이언트 소프트웨어 버전이 데이터베이스 소프트웨어 버전보다 최신인 경우가 종종 있습니다. 소프트웨어를 설치하는 가장 간단한 방법은 Oracle 클라이언트 디스크에서 Oracle Universal Installer를 사용하는 것입니다. Oracle Universal Installer에서 다음 정보를 지정합니다.  
  
    |정보|설명|  
    |-----------------|-----------------|  
    |Oracle|Oracle 소프트웨어 설치를 위한 디렉터리 경로입니다. 기본값(C:\oracle\ora90 또는 유사한 경로)을 그대로 적용하거나 다른 경로를 입력합니다. Oracle 홈에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "Oracle 홈에 대한 고려 사항" 섹션을 참조하십시오.|  
    |Oracle 홈 이름|Oracle 홈 경로에 대한 별칭입니다.|  
    |설치 유형|Oracle 10g에서 **런타임** 또는 **관리자** 설치 옵션을 선택합니다.|  
  
2.  구독자의 TNS 이름을 만듭니다. TNS(Transparent Network Substrate)는 Oracle 데이터베이스에서 사용되는 통신 계층입니다. TNS 서비스 이름은 네트워크상에서 Oracle 데이터베이스 인스턴스를 식별하는 이름입니다. Oracle 데이터베이스에 대한 연결을 구성할 때 TNS 서비스 이름을 지정합니다. 복제에서는 TNS 서비스 이름을 사용하여 구독자를 식별하고 연결을 설정합니다.  
  
     Oracle Universal Installer가 작업을 완료하면 Net Configuration Assistant를 사용하여 네트워크 연결을 구성합니다. 네트워크 연결을 구성하려면 다음 4가지 정보를 입력해야 합니다. Oracle 데이터베이스 관리자는 데이터베이스와 수신기를 설정할 때 네트워크를 구성하며, 필요한 경우 이 정보를 사용자에게 제공할 수 있어야 합니다. 다음과 같은 작업을 수행해야 합니다.  
  
    |작업|설명|  
    |------------|-----------------|  
    |데이터베이스 식별|두 가지 방법으로 데이터베이스를 식별할 수 있습니다. 첫 번째 방법은 Oracle SID(시스템 식별자)를 사용하는 것으로 모든 Oracle 릴리스에서 사용할 수 있습니다. 두 번째 방법은 서비스 이름을 사용하는 것으로 Oracle 릴리스 8.0부터 사용할 수 있습니다. 두 가지 방법 모두 데이터베이스를 만들 때 구성된 값을 사용하며 클라이언트 네트워크 구성에서 데이터베이스를 위한 수신기를 구성할 때 관리자가 사용한 것과 동일한 명명 규칙을 사용하는 것이 중요합니다.|  
    |데이터베이스에 대한 네트워크 별칭 식별|Oracle 데이터베이스 액세스에 사용할 네트워크 별칭을 지정해야 합니다. 네트워크 별칭은 데이터베이스를 만들 때 구성된 원격 SID 또는 서비스 이름을 가리킵니다. 이 별칭은 다양한 Oracle 릴리스 및 제품에서 네트 서비스 이름 및 TNS 별칭 등 여러 이름으로 불립니다. SQL*Plus의 경우 로그인 시 이 별칭을 "Host String" 매개 변수로 입력하라는 메시지가 나타납니다.|  
    |네트워크 프로토콜 선택|지원할 적절한 프로토콜을 선택합니다. 대부분의 애플리케이션은 TCP를 사용합니다.|  
    |데이터베이스 수신기를 식별할 호스트 정보 지정|호스트는 Oracle 수신기가 실행 중인 컴퓨터의 이름이나 DNS 별칭이며, 일반적으로 Oracle 수신기는 데이터베이스가 상주하는 컴퓨터에서 실행됩니다. 일부 프로토콜의 경우 추가 정보를 제공해야 합니다. 예를 들어 TCP를 선택할 경우 수신기가 대상 데이터베이스에 대한 연결 요청을 수신하는 포트를 지정해야 합니다. 기본 TCP 구성은 포트 1521을 사용합니다.|  
  
3.  스냅샷 또는 트랜잭션 게시를 만든 후[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자에 대해 설정한 다음 구독자에 대한 밀어넣기 구독을 만듭니다. 자세한 내용은 [SQL Server 이외 구독자에 대한 구독 만들기](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)을 참조하세요.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="setting-directory-permissions"></a>디렉터리 사용 권한 설정  
 배포자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 Oracle 클라이언트 네트워킹 소프트웨어가 설치된 디렉터리 및 모든 하위 디렉터리에 대한 읽기 및 실행 권한을 부여해야 합니다.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>SQL Server 배포자와 Oracle 게시자 간 연결 테스트  
 Net Configuration Assistant의 끝 부분에는 Oracle 구독자에 대한 연결을 테스트하는 옵션이 있습니다. 연결을 테스트하기 전에 Oracle 데이터베이스 인스턴스가 온라인 상태인지 Oracle 수신기가 실행 중인지 확인합니다. 테스트가 실패하면 연결하려는 데이터베이스를 담당하는 Oracle DBA에게 문의하십시오.  
  
 Oracle 구독자에 성공적으로 연결되면 구독에 대한 배포 에이전트를 구성할 때와 동일한 계정 및 암호를 사용하여 데이터베이스에 로그인합니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  `cmd` 를 입력한 다음 **확인**을 클릭합니다.  
  
3.  명령 프롬프트에서 다음을 입력합니다.  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     예: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  네트워크 구성이 성공했다면 로그인하여 `SQL` 프롬프트를 볼 수 있습니다.  
  
### <a name="considerations-for-oracle-home"></a>Oracle 홈에 대한 고려 사항  
 Oracle은 애플리케이션 이진 파일을 함께 설치하도록 지원하지만 복제에서는 특정 시간에 하나의 이진 파일 집합만 사용할 수 있습니다. 각 이진 파일 집합은 Oracle 홈과 연결되어 있으며 이진 파일은 %ORACLE_HOME%\bin 디렉터리에 있습니다. 복제에서 Oracle 구독자에 연결할 때 올바른 이진 집합(특히 최신 버전의 클라이언트 네트워킹 소프트웨어)을 사용해야 합니다.  
  
 배포자에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스에서 사용하는 계정으로 로그인하여 적절한 환경 변수를 설정합니다. %ORACLE_HOME% 변수는 클라이언트 네트워킹 소프트웨어 설치 시 지정한 설치 지점을 참조할 수 있도록 설정되어야 합니다. %PATH%는 %ORACLE_HOME% \bin 디렉터리를 처음 검색되는 Oracle 항목으로 포함해야 합니다. 환경 변수 설정 방법은 Windows 설명서를 참조하십시오.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 Oracle 홈이 두 개 이상 있는 경우 배포 에이전트에서 최신 Oracle OLE DB 공급자를 사용 중인지 확인합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자의 클라이언트 구성 요소를 업데이트했을 때 Oracle에서 OLE DB 공급자를 기본적으로 업데이트하지 않는 경우가 있습니다. 이 경우 이전 OLE DB 공급자를 제거하고 최신 OLE DB 공급자를 설치합니다. 공급자 설치 및 제거 방법은 Oracle 설명서를 참조하십시오.  
  
## <a name="considerations-for-oracle-subscribers"></a>Oracle 구독자에 대한 고려 사항  
 Oracle 구독자로 복제하는 경우 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)항목에서 다루는 고려 사항 외에 다음 문제도 고려해 보십시오.  
  
-   Oracle에서는 빈 문자열과 NULL 값을 모두 NULL로 처리합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열을 NOT NULL로 정의한 다음 해당 열을 Oracle 구독자로 복제하는 경우 이것은 중요한 문제입니다. 변경 내용을 Oracle 구독자에 적용할 때 오류가 발생하지 않게 하려면 다음 중 하나를 수행해야 합니다.  
  
    -   빈 문자열이 게시된 테이블에 열 값으로 삽입되지 않았는지 확인합니다.  
  
    -   오류에 대한 알림을 배포 에이전트 기록 로그에 받은 다음, 계속 처리하도록 허용되는 경우 배포 에이전트에 **–SkipErrors** 매개 변수를 사용합니다. Oracle 오류 코드 1400( **-SkipErrors1400**)을 지정합니다.  
  
    -   빈 문자열과 연결된 가능성이 있는 모든 문자 열에서 NOT NULL 특성을 제거하여 생성된 테이블 생성 스크립트를 수정하고 @creation_script sp_addarticle [의](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)매개 변수를 사용하여 수정된 스크립트를 아티클에 대한 사용자 지정 생성 스크립트로 제공합니다.  
  
-   Oracle 구독자에서는 0x4071 스키마 옵션을 지원합니다. 스키마 옵션에 대한 자세한 내용은 [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 참조하세요.  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>SQL Server에서 Oracle로 데이터 형식 매핑  
 다음 표에서는 Oracle을 실행 중인 구독자로 데이터를 복제할 때 사용되는 데이터 형식 매핑을 보여 줍니다.  
  
|SQL Server 데이터 형식|Oracle 데이터 형식|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**binary(1-2000)**|RAW(1-2000)|  
|**binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**char(2001-4000)**|VARCHAR2(2001-4000)|  
|**char(4001-8000)**|CLOB|  
|**date**|DATE|  
|**datetime**|DATE|  
|**datetime2(0-7)**|TIMESTAMP(7)(Oracle 9 및 Oracle 10), VARCHAR(27)(Oracle 8)|  
|**datetimeoffset(0-7)**|TIMESTAMP(7) WITH TIME ZONE(Oracle 9 및 Oracle 10), VARCHAR(34)(Oracle 8)|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|FLOAT|  
|**float**|FLOAT|  
|**geography**|BLOB|  
|**geometry**|BLOB|  
|**hierarchyid**|BLOB|  
|**image**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**nchar(1-1000)**|CHAR(1-1000)|  
|**nchar(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**numeric(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**nvarchar(1-1000)**|VARCHAR2(1-2000)|  
|**nvarchar(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|real|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|해당 사항 없음|  
|**sysname**|VARCHAR2(128)|  
|**text**|CLOB|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW (8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR (38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**varchar(1-4000)**|VARCHAR2(1-4000)|  
|**varchar(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**varchar(max)**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>참고 항목  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
