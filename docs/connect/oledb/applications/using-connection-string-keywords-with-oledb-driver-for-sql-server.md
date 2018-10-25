---
title: SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: c96a65c3935e91204d562933ba4f5f0de932f3e0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838309"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  일부 OLE DB Driver for SQL Server Api는 연결 특성을 지정 하려면 연결 문자열을 사용 합니다. 연결 문자열은 키워드와 연관된 값의 목록이며 각 키워드는 특정 연결 특성을 식별합니다.  
  
> [!NOTE]
> SQL Server용 OLE DB 드라이버는 이전 버전과의 호환성을 유지하기 위해 연결 문자열에서 모호성을 허용합니다. 예를 들어 일부 키워드를 여러 번 지정할 수 있으며 위치나 우선 순위에 따라 충돌하는 키워드를 해결할 수 있습니다. OLE DB Driver for SQL Server의 향후 릴리스에 연결 문자열에서 모호성을 허용 하지 않을 수 있습니다. SQL Server용 OLE DB 드라이버를 사용하도록 응용 프로그램을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  
  
 다음 섹션에서는 사용할 수 있는 OLE DB 드라이버를 사용 하 여 SQL Server 및 데이터 개체 (ADO (ActiveX)에 대 한 데이터 공급자와 SQL Server 용 OLE DB 드라이버를 사용 하는 경우 키워드에 설명 합니다.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 드라이버 연결 문자열 키워드  
 OLE DB 응용 프로그램에서는 데이터 원본 개체를 다음 두 가지 방법으로 초기화할 수 있습니다.  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 첫 번째 경우에는 DBPROPSET_DBINIT 속성 집합의 DBPROP_INIT_PROVIDERSTRING 속성을 설정하는 방법을 통해 공급자 문자열을 사용하여 연결 속성을 초기화할 수 있습니다. 두 번째 경우에는 초기화 문자열을 **IDataInitialize::GetDataSource** 메서드에 전달하여 연결 속성을 초기화할 수 있습니다. 두 방법 모두 동일한 OLE DB 연결 속성을 초기화하지만 서로 다른 키워드 집합을 사용합니다. **IDataInitialize::GetDataSource**에서 사용되는 키워드 집합은 적어도 초기화 속성 그룹 내의 속성에 대한 설명입니다.  
  
 일부 기본값으로 관련 OLE DB 속성 집합을 소유하거나 명시적인 값으로 설정된 임의 공급자 문자열 설정, OLE DB 속성 값은 공급자 문자열에서 설정을 재정의합니다.  
  
 공급자 문자열에서 DBPROP_INIT_PROVIDERSTRING 값을 통해 설정되는 부울 속성은 "yes" 및 "no" 값을 사용하여 설정됩니다. 초기화 문자열에서 **IDataInitialize::GetDataSource**를 사용하여 설정되는 부울 속성은 “true” 및 “false” 값을 사용하여 설정됩니다.  
  
 **IDataInitialize::GetDataSource**를 사용하는 응용 프로그램에서는 **IDBInitialize::Initialize**에 사용되는 키워드도 사용할 수 있지만 이러한 키워드는 기본값이 없는 속성에서만 사용할 수 있습니다. 응용 프로그램이 초기화 문자열에서 **IDataInitialize::GetDataSource** 키워드와 **IDBInitialize::Initialize** 키워드를 모두 사용하는 경우에는 **IDataInitialize::GetDataSource** 키워드 설정이 사용됩니다. **IDataInitialize:GetDataSource** 연결 문자열에서 **IDBInitialize::Initialize** 키워드를 사용할 수 있는 동작은 이후 버전에서 유지되지 않을 수 있으므로 응용 프로그램에서 이와 같이 사용하지 않는 것이 좋습니다.  
  
> [!NOTE]  
>  **IDataInitialize::GetDataSource**를 통해 전달된 연결 문자열은 속성으로 변환된 후 **IDBProperties::SetProperties**를 통해 적용됩니다. 구성 요소 서비스가 **IDBProperties::GetPropertyInfo**에서 속성 설명을 찾으면 이 속성이 독립 실행형 속성으로 적용됩니다. 그렇지 않으면 DBPROP_PROVIDERSTRING 속성을 통해 속성이 적용됩니다. 예를 들어, 연결 문자열을 지정 하는 경우 **데이터 원본 = server1; 서버 = server2**, **데이터 원본** 속성으로 설정 됩니다 있지만 **Server** 는 공급자 문자열로 전달 됩니다.  
  
 같은 공급자별 속성의 인스턴스를 여러 개 지정하면 첫 번째 속성의 첫 번째 값이 사용됩니다.  
  
 **IDBInitialize::Initialize**에 DBPROP_INIT_PROVIDERSTRING을 지정하는 OLE DB 응용 프로그램에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 특성 값을 중괄호로 묶을 수도 있으며, 그렇게 하는 것이 좋습니다. 그러면 특성 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 값에서 첫 번째 닫는 중괄호는 값을 종결하는 문자로 간주되므로 값에 닫는 중괄호가 있어서는 안 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 다음 표에서는 DBPROP_INIT_PROVIDERSTRING에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|설명|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|"Address"에 대한 동의어입니다.|  
|**주소**|SSPROP_INIT_NETWORKADDRESS|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서버의 네트워크 주소입니다. **Address**는 일반적으로 서버의 네트워크 이름이지만 파이프, IP 주소나 TCP/IP 포트 및 소켓 주소와 같은 다른 이름일 수도 있습니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> 값 **주소** 에 전달 된 값 보다 우선 **Server** SQL Server 용 OLE DB 드라이버를 사용 하는 경우 연결 문자열에서입니다. 또한 `Address=;`이면 **Server** 키워드에 지정된 서버에 연결하지만 `Address= ;, Address=.;`, `Address=localhost;` 및 `Address=(local);`이면 항상 로컬 서버에 연결합니다.<br /><br /> **Address** 키워드에 대한 전체 구문은 다음과 같습니다.<br /><br /> [_프로토콜_**:**]_주소_[**하십시오**_포트 &#124;\pipe\pipename_]<br /><br /> _protocol_ 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다. 프로토콜에 대 한 자세한 내용은 참조 하세요. [Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)합니다.<br /><br /> 모두 _프로토콜_ 또는 **Network** 키워드를 지정한 경우 OLE DB Driver for SQL Server에 지정 된 프로토콜 순서를 사용할지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager입니다.<br /><br /> *port*는 지정한 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.|   
|**APP**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**합니다. SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 Database 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**자동 변환**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "yes" 및 "no"입니다.|  
|**데이터베이스 백업**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어입니다.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=Yes**를 지정합니다. **MultiSubnetFailover=Yes**는 현재 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **예** 및 **아니요**입니다. 기본값은 **No**입니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "yes" 및 "no"를 값으로 받습니다. "no"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 이 값은 네트워크의 서버 이름(IP 주소)이거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 별칭이어야 합니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 합니다 **주소** 키워드를 재정의 합니다 **Server** 키워드입니다.<br /><br /> 다음 중 하나를 지정하여 로컬 서버에서 기본 인스턴스에 연결할 수 있습니다.<br /><br /> **Server =;**<br /><br /> **Server =.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\**  *instancename* **;**<br /><br /> Localdb에 대 한 자세한 내용은 참조 하세요. [OLE DB Driver for SQL Server LocalDB에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)합니다.<br /><br /> 명명된 된 인스턴스를 지정 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 추가 **\\** _InstanceName_합니다.<br /><br /> 서버를 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> **Server** 키워드에 대한 전체 구문은 다음과 같습니다.<br /><br /> **Server =**[_프로토콜_**:**]*Server*[**하십시오**_포트_]<br /><br /> _protocol_ 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다.<br /><br /> 다음 예제는 명명된 파이프를 지정하는 방법입니다.<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 이 줄은 명명된 파이프 프로토콜, 로컬 시스템의 명명된 파이프(`\\.\pipe`), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름(`MSSQL$MYINST01`) 및 명명된 파이프의 기본 이름(`sql/query`)을 지정합니다.<br /><br /> 모두를 *프로토콜* 또는 **Network** 키워드를 지정한 경우 OLE DB Driver for SQL Server에 지정 된 프로토콜 순서를 사용할지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager입니다.<br /><br /> *port*는 지정한 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.<br /><br /> 전달 되는 값의 시작 부분에 있는 공백은 무시 됩니다 **Server** SQL Server 용 OLE DB 드라이버를 사용 하는 경우 연결 문자열에서입니다.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|경우는 OLE DB Driver for SQL Server 로그인 유효성 검사에 대 한 Windows 인증 모드를 사용 하도록 "yes" 인 지시 합니다. 그렇지 않으면 SQL Server용 OLE DB 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 사용하여 로그인 유효성을 검사하도록 지시하므로 UID 및 PWD 키워드를 지정해야 합니다.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "yes" 및 "no"를 값으로 받습니다. 기본값은 "no"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**UseFMTONLY**|SSPROP_INIT_USEFMTONLY|메타 데이터에 연결할 때 검색 되는 방법을 제어 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.<br /><br />OLE DB Driver for SQL Server는 기본적으로 다음을 사용 합니다. [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 하 고 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저 메타 데이터를 검색 합니다. 이러한 저장된 프로시저에는 몇 가지 제한 사항이 (예: 실패 임시 테이블에서 작동 하는 경우). 설정 **UseFMTONLY** "yes"로 사용 하도록 드라이버에 지시 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) 메타 데이터 검색에 대 한 대신 합니다.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|이 키워드는 않으며, SQL Server 용 OLE DB 드라이버에서 해당 설정이 무시 됩니다.|  
|**WSID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **IDataInitialize::GetDataSource**를 사용하는 OLE DB 응용 프로그램에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 속성 사용은 해당 범위에 허용되는 구문을 따라야 합니다.  예를 들어 **WSID**는 따옴표 대신 중괄호(**{}**)를 사용하고 **응용 프로그램 이름**은 작은따옴표(**'**) 또는 큰따옴표(**"**)를 사용합니다. 문자열 속성만 따옴표로 묶을 수 있습니다. 정수나 열거 속성을 따옴표로 묶으면 "연결 문자열이 OLE DB 사양을 따르지 않습니다." 오류가 발생합니다.  
  
 특성 값을 작은따옴표나 큰따옴표로 묶을 수 있으며 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 큰따옴표를 사용할 경우 값에 큰따옴표를 포함해도 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 연결 문자열에 다음 표에 나열된 속성이 두 개 이상 있으면 마지막 속성의 값이 사용됩니다.  
  
 다음 표에서는 **IDataInitialize::GetDataSource**에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|설명|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**합니다. SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**자동 변환**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Server** 키워드에 대한 설명을 참조하십시오.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 DATABASE 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정합니다. **MultiSubnetFailover=True**는 (현재) 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> `MultiSubnetFailover=True`<br /><br /> SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Address** 키워드에 대한 설명을 참조하십시오.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server, "MSOLEDBSQL" 여야 합니다.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**서버 인증서 신뢰**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|메타 데이터에 연결할 때 검색 되는 방법을 제어 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.<br /><br />OLE DB Driver for SQL Server는 기본적으로 다음을 사용 합니다. [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 하 고 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저 메타 데이터를 검색 합니다. 이러한 저장된 프로시저에는 몇 가지 제한 사항이 (예: 실패 임시 테이블에서 작동 하는 경우). 설정 **사용 하 여 FMTONLY** "true"를 사용 하 여 드라이버를 지시 하 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) 메타 데이터 검색에 대 한 대신 합니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**Workstation ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **참고** 연결 문자열에서 “이전 암호” 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ADO(ActiveX Data Objects) 연결 문자열 키워드  
 ADO 응용 프로그램에서는 **ADODBConnection** 개체의 **ConnectionString** 속성을 설정하거나 **ADODBConnection** 개체의 **Open** 메서드에 대한 매개 변수로 연결 문자열을 제공합니다.  
  
 ADO 응용 프로그램에서는 OLE DB **IDBInitialize::Initialize** 메서드에 사용되는 키워드도 사용할 수 있지만 이러한 키워드는 기본값이 없는 속성에만 사용할 수 있습니다. 응용 프로그램이 초기화 문자열에 ADO 키워드와 **IDBInitialize::Initialize** 키워드를 모두 사용하는 경우에는 ADO 키워드 설정이 사용됩니다. 응용 프로그램에서 ADO 연결 문자열 키워드만 사용하는 것이 좋습니다.  
  
 ADO에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 특성 값을 큰따옴표로 묶을 수도 있으며, 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 특성 값에는 큰따옴표가 있으면 안 됩니다.  
  
 다음 표에서는 ADO 연결 문자열에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|설명|  
|-------------|-----------------------------|-----------------|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**합니다. SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**자동 변환**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Server** 키워드에 대한 설명을 참조하십시오.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 DATABASE 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정합니다. **MultiSubnetFailover=True**는 (현재) 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> `MultiSubnetFailover=True`<br /><br /> SQL Server의 지원에 대 한 OLE DB 드라이버에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [OLE DB Driver for SQL Server High Availability, Disaster Recovery에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Address** 키워드에 대한 설명을 참조하십시오.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server, "MSOLEDBSQL" 여야 합니다.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server에서 기본적으로 공급자에서 생성 된 SPN을 사용 하면 됩니다.|  
|**서버 인증서 신뢰**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|메타 데이터에 연결할 때 검색 되는 방법을 제어 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.<br /><br />OLE DB Driver for SQL Server는 기본적으로 다음을 사용 합니다. [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 하 고 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저 메타 데이터를 검색 합니다. 이러한 저장된 프로시저에는 몇 가지 제한 사항이 (예: 실패 임시 테이블에서 작동 하는 경우). 설정 **사용 하 여 FMTONLY** "true"를 사용 하 여 드라이버를 지시 하 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) 메타 데이터 검색에 대 한 대신 합니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**Workstation ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **참고** 연결 문자열에서 “이전 암호” 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
