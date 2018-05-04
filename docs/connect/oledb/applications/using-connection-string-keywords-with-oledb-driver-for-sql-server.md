---
title: SQL Server 용 OLE DB 드라이버 연결 문자열 키워드 사용 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버 연결 문자열 키워드 사용
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 128b31d8ed9b541d47882ace6f9898056c0c4c2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버 연결 문자열 키워드 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  일부 OLE DB Driver for SQL Server Api 연결 특성을 지정 하려면 연결 문자열을 사용 합니다. 연결 문자열은 키워드와 연관된 값의 목록이며 각 키워드는 특정 연결 특성을 식별합니다.  
  
> **참고:** 이전 버전과 호환성을 유지 하기 위해 연결 문자열에서 모호성을 허용 하는 OLE DB Driver for SQL Server (예를 들어 일부 키워드를 두 번 이상 지정할 수 있으며 충돌 하는 키워드 수 있습니다 위치에 따라 해결 또는 우선 순위)입니다. OLE DB Driver for SQL Server의 이후 릴리스에서 연결 문자열에서 모호성을 통합할 수 있습니다. OLE DB Driver for SQL Server를 사용 하 여 연결 문자열 모호성에 대 한 종속성을 제거 하려면 응용 프로그램을 수정 하는 경우에 것이 좋습니다.  
  
 다음 섹션에서는 데이터 공급자와 SQL Server 용 OLE DB Driver를 사용 하는 경우 SQL Server 및 ADO ActiveX Data Objects ()에 대 한 OLE DB 드라이버와 함께 사용할 수 있는 키워드에 설명 합니다.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 드라이버 연결 문자열 키워드  
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
|**주소**|SSPROP_INIT_NETWORKADDRESS|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서버의 네트워크 주소입니다. **주소** 는 일반적으로 서버의 네트워크 이름 이지만 파이프, IP 주소 또는 TCP/IP 포트 및 소켓 주소와 같은 다른 이름을 수 있습니다.<br /><br /> IP 주소를 지정하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서 TCP/IP 또는 명명된 파이프 프로토콜이 설정되어 있는지 확인합니다.<br /><br /> 값 **주소** 에 전달 된 값 보다 우선 **서버** SQL Server 용 OLE DB 드라이버를 사용 하는 경우 연결 문자열에 있습니다. 또한 `Address=;` 에 지정 된 서버에 연결 하는 **서버** 키워드를 반면 `Address= ;, Address=.;`, `Address=localhost;`, 및 `Address=(local);` 모든 인해 로컬 서버에 연결 합니다.<br /><br /> 전체 구문은 **주소** 키워드는 다음과 같습니다.<br /><br /> [*프로토콜 ***:**]* 주소 *[* *, * * * 포트 &#124;\pipe\pipename*]<br /><br /> *protocol* 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다. 프로토콜에 대 한 자세한 내용은 참조 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)합니다.<br /><br /> 모두 *프로토콜* 와 **네트워크** 키워드가 지정 된 경우 OLE DB Driver for SQL Server는에 지정 된 프로토콜 순서를 사용 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자.<br /><br /> *포트* 에 지정된 된 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.|   
|**APP**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 Database 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "yes" 및 "no"입니다.|  
|**데이터베이스**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
|**언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어입니다.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 가능한 값은 "yes" 및 "no"입니다. 기본값은 "no"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|항상 지정 **MultiSubnetFailover = Yes** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다. **MultiSubnetFailover = Yes** OLE DB Driver for SQL Server의 빠른 감지와 (현재) 활성 서버 연결을 제공 하도록 구성 합니다. 가능한 값은 **예** 및 **아니요**입니다. 기본값은 **아니요**합니다. 예를 들어:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**네트워크**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|"Network"에 대한 동의어입니다.|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "yes" 및 "no"를 값으로 받습니다. "no"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 이 값은 네트워크의 서버 이름(IP 주소)이거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자 별칭이어야 합니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> **주소** 키워드 재정의 **서버** 키워드입니다.<br /><br /> 다음 중 하나를 지정하여 로컬 서버에서 기본 인스턴스에 연결할 수 있습니다.<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> Localdb에 대 한 자세한 내용은 참조 [OLE DB Driver for SQL Server LocalDB에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)합니다.<br /><br /> 명명된 된 인스턴스를 지정 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 추가  **\\ ***InstanceName*합니다.<br /><br /> 지정 된 서버가 없는 경우 로컬 컴퓨터의 기본 인스턴스에 대 한 연결이 이루어집니다.<br /><br /> IP 주소를 지정 하는 경우에서 TCP/IP 또는 명명 된 파이프 프로토콜이 설정 되어 있는지 있는지 확인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자.<br /><br /> 전체 구문은 **서버** 키워드는 다음과 같습니다:<br /> <br /> **서버 =**[* 프로토콜***:**] *서버*[**, * * * 포트*]<br /><br /> *protocol* 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다.<br /><br /> 다음 예제는 명명된 파이프를 지정하는 방법입니다.<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 이 줄은 명명된 파이프 프로토콜, 로컬 시스템의 명명된 파이프(`\\.\pipe`), [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름(`MSSQL$MYINST01`) 및 명명된 파이프의 기본 이름(`sql/query`)을 지정합니다.<br /><br /> 모두는 *프로토콜* 와 **네트워크** 키워드가 지정 된 경우 OLE DB Driver for SQL Server는에 지정 된 프로토콜 순서를 사용 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자.<br /><br /> *포트* 에 지정된 된 서버에서 연결할 포트입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 포트 1433을 사용합니다.<br /><br /> 에 전달 된 값의 시작 부분에서 공백은 무시 됩니다 **서버** SQL Server 용 OLE DB 드라이버를 사용 하는 경우 연결 문자열에 있습니다.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|"Yes", SQL Server 용 OLE DB Driver 지시 로그인 유효성을 검사에 대 한 Windows 인증 모드를 사용 하도록 합니다. 그렇지 않은 경우 OLE DB 드라이버를 사용 하도록 SQL Server를 지시를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름 및 암호 로그인의 유효성을 검사 하므로 UID 및 PWD 키워드를 지정 해야 합니다.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "yes" 및 "no"를 값으로 받습니다. 기본값은 "no"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|이 키워드는 더 이상 SQL Server 용 OLE DB 드라이버에서 해당 설정이 무시 됩니다.|  
|**WSID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 사용 하 여 OLE DB 응용 프로그램에서 사용 되는 연결 문자열 **idatainitialize:: Getdatasource** 구문은:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 속성 사용은 해당 범위에 허용되는 구문을 따라야 합니다.  예를 들어 **WSID** 중괄호를 사용 하 여 (**{}**) 인용 문자 및 **응용 프로그램 이름** 사용 하 여 단일 (**'**) 또는 double (**"**) 인용 문자입니다. 문자열 속성만 따옴표로 묶을 수 있습니다. 정수나 열거 속성을 따옴표로 묶으면 "연결 문자열이 OLE DB 사양을 따르지 않습니다." 오류가 발생합니다.  
  
 특성 값을 작은따옴표나 큰따옴표로 묶을 수 있으며 그렇게 하는 것이 좋습니다. 그러면 값에 영숫자가 아닌 문자가 있을 경우 발생할 수 있는 문제를 막을 수 있습니다. 큰따옴표를 사용할 경우 값에 큰따옴표를 포함해도 됩니다.  
  
 연결 문자열 키워드에서 등호(=) 다음에 나오는 공백 문자는 값을 따옴표로 묶은 경우에도 리터럴로 해석됩니다.  
  
 연결 문자열에 다음 표에 나열된 속성이 두 개 이상 있으면 마지막 속성의 값이 사용됩니다.  
  
 다음 표에서 키워드와 함께 사용할 수 있는 설명 **idatainitialize:: Getdatasource**:  
  
|키워드|초기화 속성|Description|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**응용 프로그램 의도**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**현재 언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **서버** 이 항목의 키워드입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**장애 조치 파트너 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 DATABASE 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS 연결**|SSPROP_INIT_MARSCONNECTION|연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|항상 지정 **MultiSubnetFailover = True** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다. **MultiSubnetFailover = True** OLE DB Driver for SQL Server의 빠른 감지와 (현재) 활성 서버 연결을 제공 하도록 구성 합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 예를 들어:<br /><br /> `MultiSubnetFailover=True`<br /><br /> 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**네트워크 주소**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **주소** 이 항목의 키워드입니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**보안 정보 유지**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server에 대 한 "MSOLEDBSQL" 이어야 합니다.|  
|**서버 SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
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
|**응용 프로그램 의도**|SSPROP_INIT_APPLICATIONINTENT|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**합니다.<br /><br /> 기본값은 **ReadWrite**합니다. 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**Application Name**|SSPROP_INIT_APPNAME|응용 프로그램을 식별하는 문자열입니다.|  
|**자동 번역**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate"에 대한 동의어입니다.|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|OEM/ANSI 문자 변환을 구성합니다. 인식되는 값은 "true"와 "false"입니다.|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|데이터 원본 초기화가 완료될 때까지 기다릴 시간(초)입니다.|  
|**현재 언어**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 언어 이름입니다.|  
|**데이터 원본**|DBPROP_INIT_DATASOURCE|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름입니다.<br /><br /> 지정하지 않으면 로컬 컴퓨터의 기본 인스턴스에 연결합니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **서버** 이 항목의 키워드입니다.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|사용할 데이터 형식 처리 모드를 지정합니다. 인식되는 값은 "0"(공급자 데이터 형식) 및 "80"(SQL Server 2000 데이터 형식)입니다.|  
|**장애 조치(failover) 파트너**|SSPROP_INIT_FAILOVERPARTNER|데이터베이스 미러링에 사용되는 장애 조치(failover) 서버의 이름입니다.|  
|**장애 조치 파트너 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
|**초기 카탈로그**|DBPROP_INIT_CATALOG|데이터베이스 이름입니다.|  
|**초기 파일 이름**|SSPROP_INIT_FILENAME|연결할 수 있는 데이터베이스의 전체 경로 이름을 포함한 주 파일의 이름입니다. 사용 하도록 **AttachDBFileName**, 데이터베이스 이름 공급자 문자열 DATABASE 키워드에도 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않으며 연결된 데이터베이스를 연결 기본값으로 사용합니다.|  
|**통합 보안**|DBPROP_AUTH_INTEGRATED|Windows 인증을 위해 "SSPI" 값을 적용합니다.|  
|**MARS 연결**|SSPROP_INIT_MARSCONNECTION|서버가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전인 경우 연결에서 MARS(Multiple Active Result Sets)를 설정하거나 해제합니다. 인식되는 값은 "true"와 "false"입니다. 기본값은 "false"입니다.|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|항상 지정 **MultiSubnetFailover = True** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다. **MultiSubnetFailover = True** OLE DB Driver for SQL Server의 빠른 감지와 (현재) 활성 서버 연결을 제공 하도록 구성 합니다. 가능한 값은 **True** 및 **False**입니다. 기본값은 **False**입니다. 예를 들어:<br /><br /> `MultiSubnetFailover=True`<br /><br /> 에 대 한 SQL Server의 지원에 대 한 OLE DB Driver에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], 참조 [OLE DB Driver for SQL Server 고가용성, 재해 복구에 대 한 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.|  
|**네트워크 주소**|SSPROP_INIT_NETWORKADDRESS|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 네트워크 주소입니다.<br /><br /> 유효한 주소 구문에 대 한 자세한 내용은 참조에 대 한 설명을 **주소** 이 항목의 키워드입니다.|  
|**네트워크 라이브러리**|SSPROP_INIT_NETWORKLIBRARY|조직의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 네트워크 라이브러리입니다.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|네트워크 패킷 크기입니다. 기본값은 4096입니다.|  
|**암호**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호입니다.|  
|**보안 정보 유지**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|문자열 "true" 및 "false"를 값으로 받습니다. "false"인 경우 중요한 인증 정보를 데이터 원본 개체에 유지할 수 없습니다.|  
|**공급자**||OLE DB Driver for SQL Server에 대 한 "MSOLEDBSQL" 이어야 합니다.|  
|**서버 SPN**|SSPROP_INIT_SERVERSPN|서버의 SPN입니다. 기본값은 빈 문자열입니다. 빈 문자열에는 OLE DB Driver for SQL Server 공급자에서 생성 된 SPN 기본값을 사용 하도록 하면 됩니다.|  
|**서버 인증서 신뢰**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|문자열 "true" 및 "false"를 값으로 받습니다. 기본값은 "false"이며 서버 인증서의 유효성을 검사하는 것을 의미합니다.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|데이터를 네트워크를 통해 보내기 전에 암호화해야 하는지 여부를 지정합니다. 가능한 값은 "true" 및 "false"입니다. 기본값은 "false"입니다.|  
|**사용자 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|**워크스테이션 ID**|SSPROP_INIT_WSID|워크스테이션 식별자입니다.|  
  
 **참고** 연결 문자열에서 "이전 암호" 속성 SSPROP_AUTH_OLD_PASSWORD를 설정 공급자 문자열 속성을 통해 사용할 수 없는 현재 (만료 된) 암호입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
