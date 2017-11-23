---
title: "SQL Server Native Client 연결 문자열 키워드 사용 | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
caps.latest.revision: "81"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 03cfc5aa4dd24dc595984298710c073061bec0b7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>SQL Server Native Client에서 연결 문자열 키워드 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  일부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client API에서는 연결 문자열을 사용하여 연결 특성을 지정합니다. 연결 문자열은 키워드와 연관된 값의 목록이며 각 키워드는 특정 연결 특성을 식별합니다.  
  
> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 이전 버전과 호환성을 유지 하기 위해 연결 문자열에서 모호성을 허용 (예를 들어 일부 키워드를 두 번 이상 지정할 수 있습니다 및 위치에 따라 해결 된 충돌 하는 키워드를 사용할 수 있습니다 또는 선행)입니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 연결 문자열의 모호성을 허용하지 않을 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하도록 응용 프로그램을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 데이터 공급자로 사용할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 ADO(ActiveX Data Objects)와 함께 사용할 수 있는 키워드를 설명합니다.  
  
## <a name="odbc-driver-connection-string-keywords"></a>ODBC 드라이버 연결 문자열 키워드  
 ODBC 응용 프로그램 연결 문자열에 매개 변수로 사용 하 여는 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 및 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) 함수입니다.  
  
 ODBC에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 특성 값을 중괄호로 묶을 수도 있으며, 그렇게 하는 것이 좋습니다. 그러면 특성 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 값에서 첫 번째 닫는 중괄호는 값을 종결하는 문자로 간주되므로 값에 닫는 중괄호가 있어서는 안 됩니다.  
  
 다음 표에서는 ODBC 연결 문자열에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|**Addr**|"Address"에 대한 동의어입니다.|  
|**주소**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서버의 네트워크 주소입니다. **주소** 는 일반적으로 서버의 네트워크 이름 이지만 파이프, IP 주소 또는 TCP/IP 포트 및 소켓 주소와 같은 다른 이름을 수 있습니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> 값 **주소** 에 전달 된 값 보다 우선 **서버** 사용할 때 ODBC 연결 문자열에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다. 또한 `Address=;` 에 지정 된 서버에 연결 하는 **서버** 키워드를 반면 `Address= ;, Address=.;`, `Address=localhost;`, 및 `Address=(local);` 모든 인해 로컬 서버에 연결 합니다.<br /><br /> 전체 구문은 **주소** 키워드는 다음과 같습니다.<br /><br /> [*프로토콜***:**]*주소*[**,***포트 &#124; \pipe\pipename*]<br /><br /> *protocol* 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다. 프로토콜에 대 한 자세한 내용은 참조 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)합니다.<br /><br /> 모두 *프로토콜* 와 **네트워크** 키워드를 지정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는에 지정 된 프로토콜 순서를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자.<br /><br /> *포트* 에 지정된 된 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.|  
|**AnsiNPW**|"yes"인 경우 드라이버는 NULL 비교, 문자 데이터 패딩, 경고 및 NULL 연결 처리에 ANSI 정의 동작을 사용합니다. "no"인 경우 ANSI 정의 동작이 표시되지 않습니다. ANSI NPW 동작에 대 한 자세한 내용은 참조 [ISO 옵션의 효과](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)합니다.|  
|**응용 프로그램**|호출 하는 응용 프로그램의 이름 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) (선택 사항). 를 지정 하는 경우이 값은 **master.dbo.sysprocesses** 열 **program_name** 에서 반환 되 고 [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 및 [APP_NAME](../../../t-sql/functions/app-name-transact-sql.md) 함수입니다.|  
|**ApplicationIntent**|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다. 기본값은 **ReadWrite**합니다.  예를 들어<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지 원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [SQL Server 네이티브 클라이언트 지원 고가용성, 재해 복구에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.|  
|**AttachDBFileName**|연결할 수 있는 데이터베이스에 대한 주 파일의 이름입니다. 전체 경로를 포함하여 C 문자열 변수를 사용할 경우 다음과 같이 모든 \ 문자를 이스케이프합니다.<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> 이 데이터베이스는 연결되어 해당 연결에 대한 기본 데이터베이스가 됩니다. 사용 하도록 **AttachDBFileName** 에서 데이터베이스 이름을 지정도 해야는 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) DATABASE 매개 변수 또는 SQL_COPT_CURRENT_CATALOG 연결 특성입니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**AutoTranslate**|"yes"인 경우 클라이언트와 서버 간에 전송된 ANSI 문자열을 유니코드를 통한 변환으로 변환하여 클라이언트와 서버 코드 페이지 간의 확장 문자 일치에서 문제를 최소화합니다.<br /><br /> 로 전송 된 클라이언트 SQL_C_CHAR 데이터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, 또는 **텍스트** 변수, 매개 변수 또는 열이는 클라이언트 코드 ACP (ANSI 페이지)를 사용 하 여 유니코드로 후 변환 서버의 ACP를 사용 하 여 문자를 유니코드에서 변환 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**char**, **varchar**, 또는 **텍스트** 클라이언트 SQL_C_CHAR 변수로 전송 된 데이터에서에서 클라이언트 ACP를 사용 하 여 문자를 유니코드로 변환 된 후 서버 ACP를 사용 하 여 유니코드로 변환 됩니다.<br /><br /> 이러한 변환은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 의해 클라이언트에서 수행됩니다. 이를 위해서는 서버에 사용된 것과 동일한 ACP(ANSI 코드 페이지)를 클라이언트에서 사용할 수 있어야 합니다.<br /><br /> 이러한 설정은 다음 전송에 대해 발생하는 변환에는 영향을 미치지 않습니다.<br /><br /> \*로 전송 된 유니코드 SQL_C_WCHAR 클라이언트 데이터 **char**, **varchar**, 또는 **텍스트** 서버에 있습니다.<br /><br /> \***char**, **varchar**, 또는 **텍스트** 서버 데이터를 클라이언트에서 유니코드 SQL_C_WCHAR 변수로 전송 합니다.<br /><br /> \*유니코드에 전송 된 ANSI SQL_C_CHAR 클라이언트 데이터 **nchar**, **nvarchar**, 또는 **ntext** 서버에 있습니다.<br /><br /> \*유니코드 **nchar**, **nvarchar**, 또는 **ntext** 서버 데이터를 클라이언트에서 ANSI SQL_C_CHAR 변수로 전송 합니다.<br /><br /> "no"인 경우 문자 변환이 수행되지 않습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 전송 하는 클라이언트 ANSI 문자 SQL_C_CHAR 데이터를 변환 하지 않습니다 **char**, **varchar**, 또는 **텍스트** 변수, 매개 변수 또는 서버에는 열입니다. 변환에서 수행 됩니다 **char**, **varchar**, 또는 **텍스트** 서버에서 클라이언트의 SQL_C_CHAR 변수로 전송 된 데이터입니다.<br /><br /> 클라이언트와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 서로 다른 ACP를 사용하는 경우 확장 문자가 잘못 해석될 수 있습니다.|  
|**데이터베이스**|연결에 사용되는 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 이름입니다. 경우 **데이터베이스** 를 지정 하지 않으면 로그인에 대해 정의 된 기본 데이터베이스가 사용 됩니다. ODBC 데이터 원본의 기본 데이터베이스가 로그인에 지정된 기본 데이터베이스를 재지정합니다. 하지 않는 한 데이터베이스는 기존 데이터베이스 여야 **AttachDBFileName** 도 지정 합니다. 경우 **AttachDBFileName** 도 지정 되어 가리키는 주 파일이 연결 되 고 지정 된 데이터베이스 이름이 제공 **데이터베이스**합니다.|  
|**드라이버**|반환 되는 드라이버의 이름 [SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md)합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 키워드 값은 "{SQL Server Native Client 11.0}"입니다. **서버** 키워드를 사용 하는 경우 **드라이버** 지정 및 **DriverCompletion** SQL_DRIVER_NOPROMPT로 설정 합니다.<br /><br /> 드라이버 이름에 대 한 자세한 내용은 참조 [SQL Server Native Client 헤더 및 라이브러리 파일을 사용 하 여](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)합니다.|  
|**DSN**|기존 ODBC 사용자 또는 시스템 데이터 원본의 이름입니다. 에 지정할 수 있는 모든 값을 재정의 하는이 키워드는 **서버**, **네트워크**, 및 **주소** 키워드입니다.|  
|**암호화**|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**대체 (fallback)**|이 키워드는 더 이상 사용되지 않으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이 설정을 무시합니다.|  
|**Failover_Partner**|주 서버에 연결할 수 없는 경우 사용할 장애 조치(failover) 파트너 서버의 이름입니다.|  
|**FailoverPartnerSPN**|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 드라이버가 생성한 기본 SPN을 사용합니다.|  
|**FileDSN**|기존 ODBC 파일 데이터 원본의 이름입니다.|  
|**언어**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]언어 이름입니다(옵션). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 여러 언어에 대 한 메시지를 저장할 수 **sysmessages**합니다. 에 연결 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 여러 언어로 **언어** 메시지 집합을 연결에 사용 됩니다.|  
|**MARS_Connection**|연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**MultiSubnetFailover**|항상 지정 **multiSubnetFailover = Yes** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다. **multiSubnetFailover = Yes** 구성 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 빠른 감지와 (현재) 활성 서버 연결을 제공 합니다. 가능한 값은 **예** 및 **아니요**입니다. 기본값은 **아니요**합니다. 예를 들어<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지 원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [SQL Server 네이티브 클라이언트 지원 고가용성, 재해 복구에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Net**|"Network"에 대한 동의어입니다.|  
|**네트워크**|유효한 값은 **dbnmpntw** (명명 된 파이프) 및 **dbmssocn** (TCP/IP).<br /><br /> 오류가 발생에 대 한 값을 지정 하는 **네트워크** 키워드 한 프로토콜 접두사에 **서버** 키워드입니다.|  
|**PWD**|UID 매개 변수에 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 계정의 암호입니다. **PWD** 지정할 필요가 없습니다 로그인 암호가 NULL 또는 Windows 인증을 사용 하는 경우 (`Trusted_Connection = yes`).|  
|**QueryLog_On**|"yes"인 경우 연결에서 장기 실행 쿼리 데이터 기록이 사용됩니다. "no"인 경우 장기 실행 쿼리 데이터가 기록되지 않습니다.|  
|**QueryLogFile**|장기 실행 쿼리의 데이터를 기록하는 데 사용할 파일의 전체 경로 및 파일 이름입니다.|  
|**QueryLogTime**|장기 실행 쿼리 기록을 위한 임계값(밀리초)을 지정하는 숫자 문자열입니다. 지정된 시간 내에 응답을 받지 못한 쿼리가 장기 실행 쿼리 로그 파일에 기록됩니다.|  
|**QuotedId**|"yes"인 경우 QUOTED_IDENTIFIERS가 연결에 대해 ON으로 설정되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 SQL 문에서 ISO 규칙에 따라 따옴표를 사용합니다. "no"인 경우 QUOTED_IDENTIFIERS가 연결에 대해 OFF로 설정되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 SQL 문에서 레거시 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 규칙에 따라 따옴표를 사용합니다. 자세한 내용은 참조 [ISO 옵션의 효과](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)합니다.|  
|**지역**|"yes"인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 통화, 날짜 및 시간 데이터를 문자 데이터로 변환할 때 클라이언트 설정을 사용합니다. 변환이 한쪽 방향으로만 이루어지므로 드라이버는 INSERT 또는 UPDATE 문에 사용된 매개 변수 등에서 ODBC 표준 형식이 아닌 날짜 문자열이나 통화 값을 인식하지 못합니다. "no"인 경우 드라이버는 ODBC 표준 문자열을 사용하여 문자 데이터로 변환된 통화, 날짜 및 시간을 나타냅니다.|  
|**SaveFile**|연결에 성공하면 현재 연결에 대한 특성이 저장되는 ODBC 데이터 원본 파일의 이름입니다.|  
|**Server**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 이 값은 네트워크의 서버 이름(IP 주소)이거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 별칭이어야 합니다.<br /><br /> **주소** 키워드 재정의 **서버** 키워드입니다.<br /><br /> 다음 중 하나를 지정하여 로컬 서버에서 기본 인스턴스에 연결할 수 있습니다.<br /><br /> **Server =;**<br /><br /> **Server =.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\**  *instancename* **;**<br /><br /> Localdb에 대 한 자세한 내용은 참조 [SQL Server Native Client 지원 LocalDB에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)합니다.<br /><br /> 명명된 된 인스턴스를 지정 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 추가  **\\**  *InstanceName*합니다.<br /><br /> 서버를 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> 전체 구문은 **서버** 키워드는 다음과 같습니다.<br /><br /> **Server =**[*프로토콜***:**]*서버*[**,***포트*]<br /><br /> *protocol* 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다.<br /><br /> 다음 예제는 명명된 파이프를 지정하는 방법입니다.<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 이 줄은 명명된 파이프 프로토콜, 로컬 시스템의 명명된 파이프(`\\.\pipe`), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름(`MSSQL$MYINST01`) 및 명명된 파이프의 기본 이름(`sql/query`)을 지정합니다.<br /><br /> 모두는 *프로토콜* 와 **네트워크** 키워드를 지정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는에 지정 된 프로토콜 순서를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager입니다.<br /><br /> *포트* 에 지정된 된 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.<br /><br /> 에 전달 된 값의 시작 부분에서 공백은 무시 됩니다 **서버** 사용할 때 ODBC 연결 문자열에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다.|  
|**ServerSPN**|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 드라이버가 생성한 기본 SPN을 사용합니다.|  
|**StatsLog_On**|"yes"인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 성능 데이터 캡처를 사용합니다. "no"인 경우 연결에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 성능 데이터를 사용할 수 없습니다.|  
|**StatsLogFile**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 성능 통계를 기록하는 데 사용되는 파일의 전체 경로와 파일 이름입니다.|  
|**Trusted_Connection**|"yes"인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 Windows 인증 모드를 사용하여 로그인의 유효성을 검사하도록 지시합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 사용하여 로그인 유효성을 검사하도록 지시하므로 UID 및 PWD 키워드를 지정해야 합니다.|  
|**TrustServerCertificate**|와 함께 사용할 경우 **Encrypt**를 자체 서명한 서버 인증서를 사용 하 여 암호화를 사용 합니다.|  
|**UID**|유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 계정입니다. Windows 인증을 사용할 경우 UID를 지정할 필요가 없습니다.|  
|**UseProcForPrepare**|이 키워드는 더 이상 사용되지 않으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이 설정을 무시합니다.|  
|**WSID**|워크스테이션 ID로, 일반적으로 응용 프로그램이 있는 컴퓨터의 네트워크 이름입니다(옵션). 를 지정 하는 경우이 값은 **master.dbo.sysprocesses** 열 **hostname** 에서 반환 되 고 [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 및 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 함수.|  
  
> **참고:** 국가별 변환 설정이 통화, 숫자, 날짜 및 시간 데이터 형식에 적용 합니다. 변환 설정은 통화, 숫자, 날짜 또는 시간 값을 문자열로 변환한 경우에만 볼 수 있고 출력 변환에 적용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 현재 사용자의 로캘 레지스트리 설정을 사용합니다. 응용 프로그램 설정에서 연결 이후에 예를 들어 호출 하는 경우 드라이버는 현재 스레드의 로캘을 인식 하지 **SetThreadLocale**합니다.  
  
 데이터 원본의 국가별 동작을 변경하면 응용 프로그램에서 오류가 발생할 수 있습니다. 날짜 문자열을 구문 분석하며 날짜 문자열이 ODBC에 정의된 대로 표시될 것으로 예상하는 응용 프로그램에서 이 값을 변경하면 부정적인 영향을 줄 수 있습니다.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>OLE DB 공급자 연결 문자열 키워드  
 OLE DB 응용 프로그램에서는 데이터 원본 개체를 다음 두 가지 방법으로 초기화할 수 있습니다.  
  
-   **Idbinitialize:: Initialize**  
  
-   **Idatainitialize:: Getdatasource**  
  
 첫 번째 경우에는 DBPROPSET_DBINIT 속성 집합의 DBPROP_INIT_PROVIDERSTRING 속성을 설정하는 방법을 통해 공급자 문자열을 사용하여 연결 속성을 초기화할 수 있습니다. 두 번째 경우에는 초기화 문자열에 전달할 수 **idatainitialize:: Getdatasource** 메서드 연결 속성을 초기화 합니다. 두 방법 모두 동일한 OLE DB 연결 속성을 초기화하지만 서로 다른 키워드 집합을 사용합니다. 사용 되는 키워드 집합 **idatainitialize:: Getdatasource** 은 적어도 초기화 속성 그룹 내의 속성에 대해 설명 합니다.  
  
 일부 기본값으로 관련 OLE DB 속성 집합을 소유하거나 명시적인 값으로 설정된 임의 공급자 문자열 설정, OLE DB 속성 값은 공급자 문자열에서 설정을 재정의합니다.  
  
 공급자 문자열에서 DBPROP_INIT_PROVIDERSTRING 값을 통해 설정되는 부울 속성은 "yes" 및 "no" 값을 사용하여 설정됩니다. 사용 하 여 초기화 문자열에서 설정 하는 부울 속성 **idatainitialize:: Getdatasource** 값 "true" 및 "false"를 사용 하 여 설정 됩니다.  
  
 응용 프로그램을 사용 하 여 **idatainitialize:: Getdatasource** 에서 사용 하는 키워드 צ ְ ײ도 **idbinitialize:: Initialize** 기본값을 갖지 않는 속성에 대해서만 합니다. 응용 프로그램 모두를 사용 하는 경우는 **idatainitialize:: Getdatasource** 키워드 및 **idbinitialize:: Initialize** 초기화 문자열 키워드는 **idatainitialize:: Getdatasource** 키워드 설정이 사용 됩니다. 응용 프로그램 사용 하지 않는 것이 좋습니다 **idbinitialize:: Initialize** 키워드 **idatainitialize:** 이 동작은 유지 되지 않을 수 이후 버전으로 연결 문자열입니다.  
  
> [!NOTE]  
>  연결 문자열을 통해 전달 **idatainitialize:: Getdatasource** 속성으로 변환 되 고 통해 적용 **idbproperties:: Setproperties**합니다. 구성 요소 서비스에서 속성 설명을 찾으면 **idbproperties:: Getpropertyinfo**,이 속성이 독립 실행형 속성으로 적용 됩니다. 그렇지 않으면 DBPROP_PROVIDERSTRING 속성을 통해 속성이 적용됩니다. 예를 들어, 연결 문자열을 지정 하는 경우 **데이터 원본 = server1; Server = server2**, **데이터 소스** 을 속성으로 설정 됩니다 하지만 **서버** 공급자 문자열로 전달 됩니다.  
  
 같은 공급자별 속성의 인스턴스를 여러 개 지정하면 첫 번째 속성의 첫 번째 값이 사용됩니다.  
  
 Dbprop_init_providerstring을 지정 하는 OLE DB 응용 프로그램에서 사용 되는 연결 문자열 **idbinitialize:: Initialize** 구문은:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 특성 값을 중괄호로 묶을 수도 있으며, 그렇게 하는 것이 좋습니다. 그러면 특성 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 값에서 첫 번째 닫는 중괄호는 값을 종결하는 문자로 간주되므로 값에 닫는 중괄호가 있어서는 안 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 다음 표에서는 DBPROP_INIT_PROVIDERSTRING에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|Description|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|"Address"에 대한 동의어입니다.|  
|**주소**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **주소** ODBC 키워드에이 항목의 뒷부분에 나오는 합니다.|  
|**응용 프로그램**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지 원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [SQL Server 네이티브 클라이언트 지원 고가용성, 재해 복구에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 Database 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "yes" 및 "no"입니다.|  
|**데이터베이스**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**암호화**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어입니다.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**네트워크**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**패킷 크기**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "yes" 및 "no"를 값으로 받습니다. "no"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Server**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **서버** ODBC 키워드에이 항목의 합니다.|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|"yes"인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 Windows 인증 모드를 사용하여 로그인 유효성을 검사하도록 지시합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 사용하여 로그인 유효성을 검사하도록 지시하므로 UID 및 PWD 키워드를 지정해야 합니다.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "yes" 및 "no"를 값으로 받습니다. 기본값은 "no"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|이 키워드는 더 이상 사용되지 않으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 이 설정을 무시합니다.|  
|**WSID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 사용 하 여 OLE DB 응용 프로그램에서 사용 되는 연결 문자열 **idatainitialize:: Getdatasource** 구문은:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 속성 사용은 해당 범위에 허용되는 구문을 따라야 합니다.  예를 들어 **WSID** 중괄호를 사용 하 여 (**{}**) 인용 문자 및 **응용 프로그램 이름** 사용 하 여 단일 (**'**) 또는 큰따옴표 (**"**) 인용 문자입니다. 문자열 속성만 따옴표로 묶을 수 있습니다. 정수나 열거 속성을 따옴표로 묶으면 "연결 문자열이 OLE DB 사양을 따르지 않습니다." 오류가 발생합니다.  
  
 특성 값을 작은따옴표나 큰따옴표로 묶을 수 있으며 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 큰따옴표를 사용할 경우 값에 큰따옴표를 포함해도 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 연결 문자열에 다음 표에 나열된 속성이 두 개 이상 있으면 마지막 속성의 값이 사용됩니다.  
  
 다음 표에서 키워드와 함께 사용할 수 있는 설명 **idatainitialize:: Getdatasource**:  
  
|키워드|초기화 속성|Description|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**응용 프로그램 의도**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지 원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [SQL Server 네이티브 클라이언트 지원 고가용성, 재해 복구에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**현재 언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **서버** ODBC 키워드에이 항목의 뒷부분에 나오는 합니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**장애 조치 파트너 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 DATABASE 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS 연결**|SSPROP_INIT_MARSCONNECTION|연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**네트워크 주소**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **주소** ODBC 키워드에이 항목의 뒷부분에 나오는 합니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 경우 "SQLNCLI11"이어야 합니다.|  
|**서버 SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**서버 인증서 신뢰**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**워크스테이션 ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **참고** 연결 문자열에서 "이전 암호" 속성 SSPROP_AUTH_OLD_PASSWORD를 설정 공급자 문자열 속성을 통해 사용할 수 없는 현재 (만료 된) 암호입니다.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ADO(ActiveX Data Objects) 연결 문자열 키워드  
 ADO 응용 프로그램 집합의 **ConnectionString** 속성의 **ADODBConnection** 개체 또는 연결 문자열에 대 한 매개 변수로 제공는 **열려** 메서드 **ADODBConnection** 개체입니다.  
  
 ADO 응용 프로그램에서는 OLE DB에서 사용 하는 키워드를 사용할 수도 수 **idbinitialize:: Initialize** 기본값을 갖지 않는 속성에 대해서만 메서드. 응용 프로그램에서 ADO 키워드를 사용 하는 경우와 **idbinitialize:: Initialize** 키워드는 ADO 키워드 설정이 초기화 문자열에 사용 됩니다. 응용 프로그램에서 ADO 연결 문자열 키워드만 사용하는 것이 좋습니다.  
  
 ADO에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 특성 값을 큰따옴표로 묶을 수도 있으며, 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 특성 값에는 큰따옴표가 있으면 안 됩니다.  
  
 다음 표에서는 ADO 연결 문자열에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|Description|  
|-------------|-----------------------------|-----------------|  
|**응용 프로그램 의도**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지 원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [SQL Server 네이티브 클라이언트 지원 고가용성, 재해 복구에 대 한](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**현재 언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **서버** ODBC 키워드에이 항목의 합니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**장애 조치 파트너 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 DATABASE 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS 연결**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**네트워크 주소**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **주소** ODBC 키워드에이 항목의 합니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 경우 "SQLNCLI11"이어야 합니다.|  
|**서버 SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**서버 인증서 신뢰**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**워크스테이션 ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **참고** 연결 문자열에서 "이전 암호" 속성 SSPROP_AUTH_OLD_PASSWORD를 설정 공급자 문자열 속성을 통해 사용할 수 없는 현재 (만료 된) 암호입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 응용 프로그램 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
