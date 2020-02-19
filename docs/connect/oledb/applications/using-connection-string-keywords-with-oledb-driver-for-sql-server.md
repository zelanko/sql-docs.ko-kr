---
title: SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용
ms.custom: ''
ms.date: 10/11/2019
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
ms.openlocfilehash: cf754729c99d8826072b6b97acfc99a9986a9abc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381881"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  일부 OLE DB Driver for SQL Server API는 연결 문자열을 사용하여 연결 특성을 지정합니다. 연결 문자열은 키워드와 연관된 값의 목록이며 각 키워드는 특정 연결 특성을 식별합니다.  
  
> [!NOTE]
> SQL Server용 OLE DB 드라이버는 이전 버전과의 호환성을 유지하기 위해 연결 문자열에서 모호성을 허용합니다. 예를 들어 일부 키워드를 여러 번 지정할 수 있으며 위치나 우선 순위에 따라 충돌하는 키워드를 해결할 수 있습니다. 이후 릴리스의 OLE DB Driver for SQL Server에서는 연결 문자열의 모호성을 허용하지 않을 수 있습니다. SQL Server용 OLE DB 드라이버를 사용하도록 애플리케이션을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  
  
 다음 섹션에서는 OLE DB Driver for SQL Server를 데이터 공급자로 사용할 때 OLE DB Driver for SQL Server 및 ADO(ActiveX Data Objects)에서 사용할 수 있는 키워드에 대해 설명합니다.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 드라이버 연결 문자열 키워드  
 OLE DB 애플리케이션에서는 데이터 원본 개체를 다음 두 가지 방법으로 초기화할 수 있습니다.  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 첫 번째 경우에는 DBPROPSET_DBINIT 속성 집합의 DBPROP_INIT_PROVIDERSTRING 속성을 설정하는 방법을 통해 공급자 문자열을 사용하여 연결 속성을 초기화할 수 있습니다. 두 번째 경우에는 초기화 문자열을 **IDataInitialize::GetDataSource** 메서드에 전달하여 연결 속성을 초기화할 수 있습니다. 두 방법 모두 동일한 OLE DB 연결 속성을 초기화하지만 서로 다른 키워드 집합을 사용합니다. **IDataInitialize::GetDataSource**에서 사용되는 키워드 집합은 적어도 초기화 속성 그룹 내의 속성에 대한 설명입니다.  
  
 일부 기본값으로 관련 OLE DB 속성 집합을 소유하거나 명시적인 값으로 설정된 임의 공급자 문자열 설정, OLE DB 속성 값은 공급자 문자열에서 설정을 재정의합니다.  
  
 공급자 문자열에서 DBPROP_INIT_PROVIDERSTRING 값을 통해 설정되는 부울 속성은 "yes" 및 "no" 값을 사용하여 설정됩니다. 초기화 문자열에서 **IDataInitialize::GetDataSource**를 사용하여 설정되는 부울 속성은 “true” 및 “false” 값을 사용하여 설정됩니다.  
  
 **IDataInitialize::GetDataSource**를 사용하는 애플리케이션에서는 **IDBInitialize::Initialize**에 사용되는 키워드도 사용할 수 있지만 이러한 키워드는 기본값이 없는 속성에서만 사용할 수 있습니다. 애플리케이션이 초기화 문자열에서 **IDataInitialize::GetDataSource** 키워드와 **IDBInitialize::Initialize** 키워드를 모두 사용하는 경우에는 **IDataInitialize::GetDataSource** 키워드 설정이 사용됩니다. **IDataInitialize:GetDataSource** 연결 문자열에서 **IDBInitialize::Initialize** 키워드를 사용할 수 있는 동작은 이후 버전에서 유지되지 않을 수 있으므로 애플리케이션에서 이와 같이 사용하지 않는 것이 좋습니다.  
  
> [!NOTE]  
>  **IDataInitialize::GetDataSource**를 통해 전달된 연결 문자열은 속성으로 변환된 후 **IDBProperties::SetProperties**를 통해 적용됩니다. 구성 요소 서비스가 **IDBProperties::GetPropertyInfo**에서 속성 설명을 찾으면 이 속성이 독립 실행형 속성으로 적용됩니다. 그렇지 않으면 DBPROP_PROVIDERSTRING 속성을 통해 속성이 적용됩니다. 예를 들어 연결 문자열 **Data Source=server1;Server=server2**를 지정하는 경 **Data Source**는 속성으로 설정되지만 **Server**는 공급자 문자열로 이동합니다.  
  
 같은 공급자별 속성의 인스턴스를 여러 개 지정하면 첫 번째 속성의 첫 번째 값이 사용됩니다.  
  
 **IDBInitialize::Initialize**에 DBPROP_INIT_PROVIDERSTRING을 지정하는 OLE DB 애플리케이션에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
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
|**주소**|SSPROP_INIT_NETWORKADDRESS|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서버의 네트워크 주소입니다. **Address**는 일반적으로 서버의 네트워크 이름이지만 파이프, IP 주소나 TCP/IP 포트 및 소켓 주소와 같은 다른 이름일 수도 있습니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> OLE DB Driver for SQL Server를 사용하는 경우 **Address**의 값이 연결 문자열에서 **Server**에 전달된 값보다 우선하여 적용됩니다. 또한 `Address=;`이면 **Server** 키워드에 지정된 서버에 연결하지만 `Address= ;, Address=.;`, `Address=localhost;` 및 `Address=(local);`이면 항상 로컬 서버에 연결합니다.<br /><br /> **Address** 키워드에 대한 전체 구문은 다음과 같습니다.<br /><br /> [_protocol_ **:** ]_Address_[ **,** _port &#124;\pipe\pipename_]<br /><br /> _protocol_ 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다. 프로토콜에 대한 자세한 내용은 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)을 참조하세요.<br /><br /> _protocol_ 및 **Network** 키워드를 모두 지정하지 않은 경우 OLE DB Driver for SQL Server는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 지정한 프로토콜 순서를 사용합니다.<br /><br /> *port*는 지정한 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.|   
|**APP**|SSPROP_INIT_APPNAME|애플리케이션을 식별하는 문자열입니다.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**입니다. OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 Database 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**인증**<a href="#table1_1"><sup id="table1_authmode">**1**</sup></a>|SSPROP_AUTH_MODE|사용되는 SQL 또는 Active Directory 인증을 지정합니다. 유효한 값은 다음과 같습니다.<br/><ul><li>`(not set)`: 다른 키워드에 의해 결정되는 인증 모드입니다.</li><li>`ActiveDirectoryPassword:` Azure Active Directory ID를 사용하는 사용자 ID 및 암호 인증입니다.</li><li>`ActiveDirectoryIntegrated:` Azure Active Directory ID를 사용하는 통합 인증입니다.</li><br/>**참고:** `ActiveDirectoryIntegrated` 키워드는 SQL Server에 대한 Windows 인증에도 사용할 수 있습니다. `Integrated Security`(또는 `Trusted_Connection`) 인증 키워드를 대체합니다. `Integrated Security`(또는 `Trusted_Connection`) 키워드 또는 해당 속성을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `ActiveDirectoryIntegrated`로 설정하여 새 암호화 및 인증서 유효성 검사 동작을 사용할 것을 **권장**합니다.<br/><br/><li>`ActiveDirectoryInteractive:` Azure Active Directory ID를 사용하는 대화형 인증입니다. 이 방법은 Azure MFA(다단계 인증)를 지원합니다. </li><li>`ActiveDirectoryMSI:` [MSI(관리 서비스 ID)](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) 인증입니다. 사용자 할당 ID의 경우 사용자 ID를 사용자 ID의 개체 ID로 설정해야 합니다.</li><li>`SqlPassword:` 사용자 ID 및 암호를 사용하는 인증입니다.</li><br/>**참고:** `SQL Server` 인증을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `SqlPassword`로 설정하여 [새 암호화 및 인증서 유효성 검사 동작](../features/using-azure-active-directory.md#encryption-and-certificate-validation)을 사용할 것을 **권장**합니다.</ul>|
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "yes" 및 "no"입니다.|  
|**Database**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**Encrypt**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어입니다.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=Yes**를 지정합니다. **MultiSubnetFailover=Yes**는 현재 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **예** 및 **아니요**입니다. 기본값은 **No**입니다. 다음은 그 예입니다.<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "yes" 및 "no"를 값으로 받습니다. "no"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 이 값은 네트워크의 서버 이름(IP 주소)이거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 별칭이어야 합니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> **Address** 키워드는 **Server** 키워드를 재정의합니다.<br /><br /> 다음 중 하나를 지정하여 로컬 서버에서 기본 인스턴스에 연결할 수 있습니다.<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> LocalDB 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 LocalDB 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)을 참조하세요.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 명명된 인스턴스를 지정하려면 **\\** _InstanceName_을 추가합니다.<br /><br /> 서버를 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> **Server** 키워드에 대한 전체 구문은 다음과 같습니다.<br /><br /> **Server=** [_protocol_ **:** ]*Server*[ **,** _port_]<br /><br /> _protocol_ 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다.<br /><br /> 다음 예제는 명명된 파이프를 지정하는 방법입니다.<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 이 줄은 명명된 파이프 프로토콜, 로컬 시스템의 명명된 파이프(`\\.\pipe`), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름(`MSSQL$MYINST01`) 및 명명된 파이프의 기본 이름(`sql/query`)을 지정합니다.<br /><br /> *protocol* 및 **Network** 키워드를 모두 지정하지 않은 경우 OLE DB Driver for SQL Server는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 지정한 프로토콜 순서를 사용합니다.<br /><br /> *port*는 지정한 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.<br /><br /> OLE DB Driver for SQL Server를 사용하는 경우 연결 문자열에서 **Server**에 전달된 값의 시작 부분에서 공백이 무시됩니다.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|"yes"인 경우 OLE DB Driver for SQL Server가 Windows 인증 모드를 사용하여 로그인의 유효성을 검사하도록 지시합니다. 그렇지 않으면 SQL Server용 OLE DB 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 사용하여 로그인 유효성을 검사하도록 지시하므로 UID 및 PWD 키워드를 지정해야 합니다.|  
|**TrustServerCertificate**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "yes" 및 "no"를 값으로 받습니다. 기본값은 "no"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**UseFMTONLY**|SSPROP_INIT_USEFMTONLY|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상에 연결할 때 메타데이터를 검색하는 방법을 제어합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.<br /><br />기본적으로 OLE DB Driver for SQL Server는 [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 및 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저를 사용하여 메타데이터를 검색합니다. 이러한 저장 프로시저에는 몇 가지 제한 사항이 있습니다(예: 임시 테이블에서 작동하는 경우 실패함). **UseFMTONLY**를 "yes"로 설정하면 드라이버가 메타데이터 검색을 위해 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)를 대신 사용합니다.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|이 키워드는 더 이상 사용되지 않으며 OLE DB Driver for SQL Server는 이 설정을 무시합니다.|  
|**WSID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
<b id="table1_1">[1]:</b> 보안을 개선하기 위해 인증/액세스 토큰 초기화 속성 또는 해당 연결 문자열 키워드를 사용하는 경우 암호화 및 인증서 유효성 검사 동작이 수정됩니다. 자세한 내용은 [암호화 및 인증서 유효성 검사](../features/using-azure-active-directory.md#encryption-and-certificate-validation)를 참조하세요.

 **IDataInitialize::GetDataSource**를 사용하는 OLE DB 애플리케이션에서 사용하는 연결 문자열의 구문은 다음과 같습니다.  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 속성 사용은 해당 범위에 허용되는 구문을 따라야 합니다.  예를 들어 **WSID**는 따옴표 대신 중괄호( **{}** )를 사용하고 **애플리케이션 이름**은 작은따옴표( **'** ) 또는 큰따옴표( **"** )를 사용합니다. 문자열 속성만 따옴표로 묶을 수 있습니다. 정수나 열거 속성을 따옴표로 묶으면 "연결 문자열이 OLE DB 사양을 따르지 않습니다." 오류가 발생합니다.  
  
 특성 값을 작은따옴표나 큰따옴표로 묶을 수 있으며 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 큰따옴표를 사용할 경우 값에 큰따옴표를 포함해도 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 연결 문자열에 다음 표에 나열된 속성이 두 개 이상 있으면 마지막 속성의 값이 사용됩니다.  
  
 다음 표에서는 **IDataInitialize::GetDataSource**에서 사용할 수 있는 키워드에 대해 설명합니다.  
  
|키워드|초기화 속성|Description|  
|-------------|-----------------------------|-----------------|  
|**액세스 토큰**<a href="#table2_1"><sup id="table2_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory에서 인증을 받는 데 사용하는 액세스 토큰입니다. <br/><br/>**참고:** 이 키워드를 지정하면 오류가 발생하고 `UID`, `PWD`, `Trusted_Connection` 또는 `Authentication` 연결 문자열 키워드 또는 해당 속성/키워드를 지정해도 오류가 발생합니다.|
|**애플리케이션 이름**|SSPROP_INIT_APPNAME|애플리케이션을 식별하는 문자열입니다.|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**입니다. OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**인증**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|사용되는 SQL 또는 Active Directory 인증을 지정합니다. 유효한 값은 다음과 같습니다.<br/><ul><li>`(not set)`: 다른 키워드에 의해 결정되는 인증 모드입니다.</li><li>`ActiveDirectoryPassword:` Azure Active Directory ID를 사용하는 사용자 ID 및 암호 인증입니다.</li><li>`ActiveDirectoryIntegrated:` Azure Active Directory ID를 사용하는 통합 인증입니다.</li><br/>**참고:** `ActiveDirectoryIntegrated` 키워드는 SQL Server에 대한 Windows 인증에도 사용할 수 있습니다. `Integrated Security`(또는 `Trusted_Connection`) 인증 키워드를 대체합니다. `Integrated Security`(또는 `Trusted_Connection`) 키워드 또는 해당 속성을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `ActiveDirectoryIntegrated`로 설정하여 새 암호화 및 인증서 유효성 검사 동작을 사용할 것을 **권장**합니다.<br/><br/><li>`ActiveDirectoryInteractive:` Azure Active Directory ID를 사용하는 대화형 인증입니다. 이 방법은 Azure MFA(다단계 인증)를 지원합니다. </li><li>`ActiveDirectoryMSI:` [MSI(관리 서비스 ID)](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) 인증입니다. 사용자 할당 ID의 경우 사용자 ID를 사용자 ID의 개체 ID로 설정해야 합니다.</li><li>`SqlPassword:` 사용자 ID 및 암호를 사용하는 인증입니다.</li><br/>**참고:** `SQL Server` 인증을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `SqlPassword`로 설정하여 [새 암호화 및 인증서 유효성 검사 동작](../features/using-azure-active-directory.md#encryption-and-certificate-validation)을 사용할 것을 **권장**합니다.</ul>|
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Server** 키워드에 대한 설명을 참조하십시오.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 DATABASE 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정합니다. **MultiSubnetFailover=True**는 (현재) 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 다음은 그 예입니다.<br /><br /> `MultiSubnetFailover=True`<br /><br /> OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Address** 키워드에 대한 설명을 참조하십시오.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server의 경우 "MSOLEDBSQL"이어야 합니다.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**서버 인증서 신뢰**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**데이터에 대해 암호화 사용**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상에 연결할 때 메타데이터를 검색하는 방법을 제어합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.<br /><br />기본적으로 OLE DB Driver for SQL Server는 [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 및 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저를 사용하여 메타데이터를 검색합니다. 이러한 저장 프로시저에는 몇 가지 제한 사항이 있습니다(예: 임시 테이블에서 작동하는 경우 실패함). **Use FMTONLY**를 "true"로 설정하면 드라이버가 메타데이터 검색을 위해 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)를 대신 사용합니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**Workstation ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
<b id="table2_1">[1]:</b> 보안을 개선하기 위해 인증/액세스 토큰 초기화 속성 또는 해당 연결 문자열 키워드를 사용하는 경우 암호화 및 인증서 유효성 검사 동작이 수정됩니다. 자세한 내용은 [암호화 및 인증서 유효성 검사](../features/using-azure-active-directory.md#encryption-and-certificate-validation)를 참조하세요.

 **참고** 연결 문자열에서 “이전 암호” 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ADO(ActiveX Data Objects) 연결 문자열 키워드  
 ADO 애플리케이션에서는 **ADODBConnection** 개체의 **ConnectionString** 속성을 설정하거나 **ADODBConnection** 개체의 **Open** 메서드에 대한 매개 변수로 연결 문자열을 제공합니다.  
  
 ADO 애플리케이션에서는 OLE DB **IDBInitialize::Initialize** 메서드에 사용되는 키워드도 사용할 수 있지만 이러한 키워드는 기본값이 없는 속성에만 사용할 수 있습니다. 애플리케이션이 초기화 문자열에 ADO 키워드와 **IDBInitialize::Initialize** 키워드를 모두 사용하는 경우에는 ADO 키워드 설정이 사용됩니다. 애플리케이션에서 ADO 연결 문자열 키워드만 사용하는 것이 좋습니다.  
  
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
|**액세스 토큰**<a href="#table3_1"><sup id="table3_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|Azure Active Directory에서 인증을 받는 데 사용하는 액세스 토큰입니다.<br/><br/>**참고:** 이 키워드를 지정하면 오류가 발생하고 `UID`, `PWD`, `Trusted_Connection` 또는 `Authentication` 연결 문자열 키워드 또는 해당 속성/키워드를 지정해도 오류가 발생합니다.|
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br /> 기본값은 **ReadWrite**입니다. OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**애플리케이션 이름**|SSPROP_INIT_APPNAME|애플리케이션을 식별하는 문자열입니다.|  
|**인증**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|사용되는 SQL 또는 Active Directory 인증을 지정합니다. 유효한 값은 다음과 같습니다.<br/><ul><li>`(not set)`: 다른 키워드에 의해 결정되는 인증 모드입니다.</li><li>`ActiveDirectoryPassword:` Azure Active Directory ID를 사용하는 사용자 ID 및 암호 인증입니다.</li><li>`ActiveDirectoryIntegrated:` Azure Active Directory ID를 사용하는 통합 인증입니다.</li><br/>**참고:** `ActiveDirectoryIntegrated` 키워드는 SQL Server에 대한 Windows 인증에도 사용할 수 있습니다. `Integrated Security`(또는 `Trusted_Connection`) 인증 키워드를 대체합니다. `Integrated Security`(또는 `Trusted_Connection`) 키워드 또는 해당 속성을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `ActiveDirectoryIntegrated`로 설정하여 새 암호화 및 인증서 유효성 검사 동작을 사용할 것을 **권장**합니다.<br/><br/><li>`ActiveDirectoryInteractive:` Azure Active Directory ID를 사용하는 대화형 인증입니다. 이 방법은 Azure MFA(다단계 인증)를 지원합니다. </li><li>`ActiveDirectoryMSI:` [MSI(관리 서비스 ID)](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) 인증입니다. 사용자 할당 ID의 경우 사용자 ID를 사용자 ID의 개체 ID로 설정해야 합니다.</li><li>`SqlPassword:` 사용자 ID 및 암호를 사용하는 인증입니다.</li><br/>**참고:** `SQL Server` 인증을 사용하는 애플리케이션은 `Authentication` 키워드(또는 해당 속성)의 값을 `SqlPassword`로 설정하여 [새 암호화 및 인증서 유효성 검사 동작](../features/using-azure-active-directory.md#encryption-and-certificate-validation)을 사용할 것을 **권장**합니다.</ul>|
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Server** 키워드에 대한 설명을 참조하십시오.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. **AttachDBFileName**을 사용하려면 공급자 문자열 DATABASE 키워드에도 데이터베이스 이름을 지정해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정합니다. **MultiSubnetFailover=True**는 (현재) 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 SQL Server용 OLE DB 드라이버를 구성합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 다음은 그 예입니다.<br /><br /> `MultiSubnetFailover=True`<br /><br /> OLE DB Driver for SQL Server의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대한 자세한 내용은 [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대한 자세한 내용은 이 항목에 있는 **Address** 키워드에 대한 설명을 참조하십시오.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server의 경우 "MSOLEDBSQL"이어야 합니다.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열을 지정하면 OLE DB Driver for SQL Server는 공급자가 생성한 기본 SPN을 사용합니다.|  
|**서버 인증서 신뢰**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**데이터에 대해 암호화 사용**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상에 연결할 때 메타데이터를 검색하는 방법을 제어합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.<br /><br />기본적으로 OLE DB Driver for SQL Server는 [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 및 [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) 저장 프로시저를 사용하여 메타데이터를 검색합니다. 이러한 저장 프로시저에는 몇 가지 제한 사항이 있습니다(예: 임시 테이블에서 작동하는 경우 실패함). **Use FMTONLY**를 "true"로 설정하면 드라이버가 메타데이터 검색을 위해 [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)를 대신 사용합니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**Workstation ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
<b id="table3_1">[1]:</b> 보안을 개선하기 위해 인증/액세스 토큰 초기화 속성 또는 해당 연결 문자열 키워드를 사용하는 경우 암호화 및 인증서 유효성 검사 동작이 수정됩니다. 자세한 내용은 [암호화 및 인증서 유효성 검사](../features/using-azure-active-directory.md#encryption-and-certificate-validation)를 참조하세요.

 **참고** 연결 문자열에서 “이전 암호” 속성은 공급자 문자열 속성을 통해 사용할 수 없는 현재(만료된) 암호인 SSPROP_AUTH_OLD_PASSWORD를 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
