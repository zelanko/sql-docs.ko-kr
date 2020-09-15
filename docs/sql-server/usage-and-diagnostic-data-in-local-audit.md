---
title: 사용량 현황 및 진단 데이터 수집의 로컬 감사
description: 사용량 현황 및 진단 데이터를 수집하고 Microsoft에 보내기 위해 SQL Server에서 사용하는 로컬 감사에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a212013d950f6a8f39816361b7f9c6209d0fa3e3
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362518"
---
# <a name="local-audit-for-sql-server-usage-and-diagnostic-data-collection-ceip"></a>SQL Server 사용 현황 및 진단 데이터 수집(CEIP)에 대한 로컬 감사

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

## <a name="introduction"></a>소개

Microsoft SQL Server에는 컴퓨터 또는 디바이스에 대한 정보를 수집하여 보낼 수 있는 인터넷 사용 기능이 포함되어 있습니다. 이를 *표준 컴퓨터 정보*라고 합니다. [SQL Server 사용 현황 및 진단 데이터 수집](usage-and-diagnostic-data-configuration-for-sql-server.md)의 로컬 감사 구성 요소는 서비스에서 수집한 데이터를 지정된 폴더에 기록하여 Microsoft로 보낼 데이터(로그)를 나타냅니다. 로컬 감사의 목적은 규정 준수 또는 개인 정보 유효성 검사를 위해 Microsoft가 이 기능을 사용하여 수집하는 모든 데이터를 고객이 확인할 수 있도록 하는 것입니다.  

SQL Server 2016 CU2 및 CU3의 경우 SQL Server 데이터베이스 엔진 및 Analysis Services(SSAS)에 대한 인스턴스 수준에서 로컬 감사를 구성할 수 있습니다. SQL Server 2016 CU4, 2016 SP1 및 이후 릴리스에서는 SSIS(SQL Server Integration Services)에도 로컬 감사를 사용할 수 있습니다. 설정 중 설치한 다른 SQL Server 구성 요소와 설정 후 다운로드하거나 설치한 SQL Server 도구에는 사용 현황 및 진단 데이터 수집에 대한 로컬 감사 기능이 포함되어 있지 않습니다.

## <a name="remarks"></a>설명

 - SQL CEIP 서비스 제거 또는 비활성화는 지원되지 않습니다. 
 - 클러스터 그룹에서 SQL CEIP 리소스를 제거하는 것은 지원되지 않습니다. 

데이터 수집을 옵트아웃하려면 [로컬 감사 켜기 또는 끄기](#turning-local-audit-on-or-off)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항 

각 SQL Server 인스턴스에서 로컬 감사를 사용하도록 설정하는 데 필요한 사전 요구 사항은 다음과 같습니다. 

1. 인스턴스는 SQL Server 2016 RTM CU2 이상으로 패치됩니다. Integration Services의 경우 인스턴스가 SQL 2016 RTM CU4, SQL 2016 SP1 이상으로 패치됩니다.

1. 사용자는 레지스트리 키 추가 및 수정, 폴더 만들기, 폴더 보안 관리 및 Windows 서비스를 중지/시작이 가능한 액세스 권한이 부여된 시스템 관리자 또는 역할이어야 합니다.  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>로컬 감사를 켜기 전 사전 구성 단계

로컬 감사를 켜기 전에 시스템 관리자는 다음을 수행해야 합니다.

1. SQL Server 인스턴스 이름 및 SQL Server CEIP 서비스 로그온 계정을 파악합니다. 

1. 로컬 감사 파일에 사용할 새 폴더를 구성합니다.

1. SQL Server CEIP 서비스 로그온 계정에 사용 권한을 부여합니다.

1. 레지스트리 키 설정을 만들어 로컬 감사 대상 디렉터리를 구성합니다. 


### <a name="get-the-sql-server-ceip-service-logon-account"></a>SQL Server CEIP 서비스 로그온 계정 가져오기 

SQL Server CEIP 서비스 로그온 계정을 가져오려면 다음 단계를 수행합니다.
 
1. **서비스** 콘솔을 시작합니다. 이렇게 하려면 키보드에서 **Windows 키 + R**을 눌러 **실행** 대화 상자를 엽니다. 그런 다음, 텍스트 필드에 *services.msc*를 입력하고 **확인**을 선택하여 **서비스** 콘솔을 시작합니다.  

2. 적절한 서비스로 이동합니다. 예를 들어 데이터베이스 엔진의 경우 **SQL Server CEIP 서비스** **(*Your-Instance-Name*)** 를 찾습니다. Analysis Services의 경우 **SQL Server Analysis Services CEIP** **(*Your-Instance-Name*)** 를 찾습니다. Integration Services의 경우 **SQL Server Integration Services CEIP 서비스**를 찾습니다.

3. 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 

4. **로그온** 탭을 선택합니다. 로그온 계정은 **이 계정**에 나열되어 있습니다. 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>로컬 감사 파일에 사용할 새 폴더를 구성합니다.    

로컬 감사에서 로그를 기록할 새 폴더(로컬 감사 디렉터리)를 만듭니다. 예를 들어 데이터베이스 엔진의 기본 인스턴스에 대한 로컬 감사 디렉터리의 전체 경로는 다음과 같습니다. *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* . 
 
  >[!NOTE] 
  >감사 기능 및 패치 허용으로 인해 SQL Server에 문제가 발생하는 것을 방지하려면 SQL Server 설치 경로 외부에 로컬 감사 디렉터리 경로를 구성하세요.

|디자인 결정|권장|  
|-----------------|----------|  
|공간 가용성 |약 10개의 데이터베이스를 사용하는 보통의 작업에서 인스턴스당 데이터베이스별로 약 2MB의 디스크 공간을 계획합니다.|  
|개별 디렉터리 | 각 인스턴스에 대한 디렉터리를 만듭니다. 예를 들어 `MSSQLSERVER`의 SQL Server 인스턴스의 경우 *c:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*를 사용합니다. 이렇게 하면 파일 관리가 간소화됩니다.
|개별 폴더 |각 서비스에 대해 특정 폴더를 사용합니다. 예를 들어 지정된 인스턴스 이름에 대해 데이터베이스 엔진에 하나의 폴더를 설정합니다. Analysis Services 인스턴스에서 동일한 인스턴스 이름을 사용할 경우 Analysis Services에 별도 폴더를 만듭니다. 데이터베이스 엔진 및 Analysis Services 인스턴스를 모두 동일한 폴더에 구성하면 모든 로컬 감사에서 두 인스턴스를 모두 동일한 로그 파일에 기록하게 됩니다.| 
|SQL Server CEIP 서비스 로그온 계정에 사용 권한 부여|SQL Server CEIP 서비스 로그온 계정에 대해 **폴더 내용 목록**, **읽기** 및 **쓰기** 액세스를 사용하도록 설정합니다.|


### <a name="grant-permissions-to-the-sql-server-ceip-service-logon-account"></a>SQL Server CEIP 서비스 로그온 계정에 사용 권한 부여
  
1. **파일 탐색기**에서 새 폴더가 있는 위치로 이동합니다.

1. 새 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 

1. **보안 탭**에서 **편집** 관리 권한을 선택합니다.

1. **추가**를 선택하고 SQL Server CEIP 서비스의 자격 증명을 입력합니다. 예: `NT Service\SQLTELEMETRY`.

1. **이름 확인**을 선택하여 제공한 이름의 유효성을 검사한 후 **확인**을 선택합니다.

1. **사용 권한** 대화 상자에서 SQL Server CEIP 서비스 로그온 계정을 선택하고 **폴더 내용 목록**, **읽기** 및 **쓰기**를 선택합니다.

1. **확인**을 선택하여 권한 변경 내용을 즉시 적용합니다. 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>레지스트리 키 설정을 만들어 로컬 감사 대상 디렉터리 구성

1. regedit를 실행합니다.

1. 적절한 CPE 경로로 이동합니다.

   | 버전 | ***데이터베이스 엔진*** -레지스트리 키 |
   | :------ | :----------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**13**.*Your-Instance-Name*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**14**.*Your-Instance-Name*\\CPE |
   | 2019    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**15**.*Your-Instance-Name*\\CPE |
   | &nbsp; | &nbsp; |

   | 버전 | ***Analysis Services*** - 레지스트리 키 |
   | :------ | :------------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**13**.*Your-Instance-Name*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**14**.*Your-Instance-Name*\\CPE |
   | 2019    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**15**.*Your-Instance-Name*\\CPE |  
   | &nbsp; | &nbsp; |

   | 버전 | ***Integration Services*** - 레지스트리 키 |
   | :------ | :---------------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**130** |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**140** |
   | 2019    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**150** |
   | &nbsp; | &nbsp; |

1. CPE 경로를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다. **문자열 값**을 선택합니다.

1. 새 레지스트리 키의 이름을 `UserRequestedLocalAuditDirectory`로 지정합니다. 
 
## <a name="turning-local-audit-on-or-off"></a>로컬 감사 켜기 또는 끄기

사전 구성 단계를 완료한 후에 로컬 감사를 켤 수 있습니다. 이렇게 하려면 시스템 관리자 계정이나 레지스트리 키를 수정할 수 있는 액세스 권한을 가진 비슷한 역할을 사용하여 다음 단계에 따라 로컬 감사를 켜거나 끕니다. 

1. **regedit**를 실행합니다.  

1. 적절한 CPE [경로](#create-a-registry-key-setting-to-configure-local-audit-target-directory)로 이동합니다. 

1. **UserRequestedLocalAuditDirectory**를 마우스 오른쪽 단추로 클릭하고 *수정*을 선택합니다. 

1. 로컬 감사를 켜려면 로컬 감사 경로를 입력합니다(예: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* ).
 
    로컬 감사를 끄려면 **UserRequestedLocalAuditDirectory** 값을 비워 둡니다.

1. **regedit**를 닫습니다. 

서비스가 이미 실행 중인 경우 SQL Server CEIP에서는 로컬 감사 설정을 즉시 인식해야 합니다. SQL Server CEIP 서비스를 시작하기 위해 Windows 서비스 시작 또는 중지에 대한 액세스 권한이 있는 시스템 관리자 또는 사용자는 다음 단계를 수행할 수 있습니다. 

1. **서비스** 콘솔을 시작합니다. 이렇게 하려면 키보드에서 **Windows 키 + R**을 눌러 **실행** 대화 상자를 엽니다. 그런 다음, 텍스트 필드에 *services.msc*를 입력하고 **확인**을 선택하여 **서비스** 콘솔을 시작합니다.  

1. 적절한 서비스로 이동합니다. 

    - 데이터베이스 엔진의 경우 **SQL Server CEIP 서비스(*Your-Instance-Name*)** 를 사용합니다.     
    - Analysis Services의 경우 **SQL Server Analysis Services CEIP(*Your-Instance-Name*)** 를 사용합니다.
    - Integration Services의 경우 
        - SQL 2016의 경우 *SQL Server Integration Services CEIP 서비스 13.0*을 사용합니다.
        - SQL 2017의 경우 *SQL Server Integration Services CEIP 서비스 14.0*을 사용합니다.
    - SQL 2019의 경우 ‘SQL Server Integration Services CEIP 서비스 15.0’을 사용합니다.**

1. 서비스를 마우스 오른쪽 단추로 클릭하고 다시 시작을 선택합니다. 

1. 서비스의 상태가 **실행 중**인지 확인합니다. 

로컬 감사는 하루에 하나의 로그 파일을 생성합니다. 로그 파일 형식은 `<YYYY-MM-DD>.json`입니다. 예를 들면 *2016-07-12.json*입니다. 지정된 디렉터리에 해당일에 대한 기존 파일이 있으면 해당 파일에 로컬 감사가 추가됩니다. 그렇지 않으면 하루에 대해 새 파일이 만들어집니다. 

  >[!NOTE]
  > 로컬 감사를 사용하도록 설정한 후 처음 로그 파일에 기록하는 경우에는 최대 5분의 시간이 걸릴 수 있습니다. 

## <a name="maintenance"></a>유지 관리 

1. 로컬 감사에서 기록된 파일별로 디스크 공간 사용량을 제한하려면 로컬 감사 디렉터리를 정리하여 오래된 불필요한 파일을 제거하도록 정책이나 일반 작업을 설정하세요.  

2. 적절한 사람만 액세스할 수 있도록 로컬 감사 디렉터리 경로를 보호합니다. [How to configure SQL Server 2016 to send feedback to Microsoft](https://support.microsoft.com/kb/3153756)(Microsoft에 피드백을 보내도록 SQL Server 2016를 구성하는 방법)에 설명된 대로 로그 파일에 정보가 포함되어 있습니다. 이 파일에 대한 액세스 권한은 대부분의 조직 멤버는 읽을 수 없습니다.  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>로컬 감사 출력 데이터 구조의 데이터 사전 

- 로컬 감사 로그 파일은 JSON 형식이며, **emitTime**에 Microsoft로 보낸 데이터 요소를 나타내는 개체(행) 집합이 포함되어 있습니다.
- 각 행 앞에는 **schemaVersion**에서 식별한 특정 스키마가 붙습니다.
- 각 행은 **sessionID**로 식별하는 SQLCEIP 서비스 세션의 출력입니다.
- 행은 순서대로 생략되며 **시퀀스**에서 식별됩니다.
- 각 데이터 요소 행에는 **traceName**로 식별되어 T-SQL 쿼리, XE 세션 또는 추적 형식과 관련된 메시지일 수 있는 **queryIdentifier** 출력이 포함되어 있습니다.
- **queryIdentifiers** 는 **querySetVersion**과 함께 그룹화되어 버전이 지정됩니다.
- **data** 에는 **queryTimeInTicks**를 수행한 해당 쿼리 실행의 출력이 포함됩니다.
- T-SQL 쿼리에 대한**queryIdentifiers** 에는 쿼리에서 저장된 T-SQL 쿼리 정의가 있습니다.

| 논리적 로컬 감사 정보 계층 구조 | 관련 열 |
| ------ | -------|
| 헤더 | emitTime, schemaVersion 
| 컴퓨터 | operatingSystem 
| 인스턴스 | instanceUniqueID, correlationID, clientVersion 
| 세션 | sessionID, traceName 
| 쿼리 | sequence, querySetVersion, queryIdentifier, query, queryTimeInTicks 
| 데이터 |  데이터 

### <a name="namevalue-pairs-definition-and-examples"></a>이름/값 쌍 정의 및 예제 

아래 나열된 열은 로컬 감사 파일 출력 순서를 나타냅니다. SHA 256을 사용하는 단방향 해시를 통해 아래의 다양한 열이 익명 값으로 처리됩니다.  

| 이름 | 설명 | 예제 값
|-------|--------| ----------|
|instanceUniqueID| 익명화된 인스턴스 식별자 | 888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD 
|schemaVersion| SQLCEIP의 스키마 버전 |  3 
|emitTime |데이터 요소를 내보내는 시간(UTC) | 2016-09-08T17:20:22.1124269Z 
|sessionID | SQLCEIP 서비스를 제공하는 세션 식별자 | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
|correlationId | 추가 식별자에 대한 자리 표시자 | 0 
|시퀀스 | 전송 세션 내에서 데이터 요소의 시퀀스 번호 | 15 
|clientVersion | SQL Server 인스턴스 버전 | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907 1223) 
|operatingSystem | SQL Server 인스턴스가 설치되어 있는 OS 버전 | Microsoft Windows Server 2012 R2 Datacenter 
|querySetVersion | 쿼리 정의의 그룹 버전 | 1.0.0.0 
|queryIdentifier | 추적 범주: (SQLServerXeQueries, SQLServerPeriodicQueries, SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|traceName | 쿼리 식별자 | SQLServerProperties.002 
|데이터   | T-SQL 쿼리, XE 세션 또는 애플리케이션의 출력으로 queryIdentifier에서 수집된 정보 출력 |  [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
|Query| 해당하는 경우 데이터를 생성하는 queryIdentifier와 관련된 T-SQL 쿼리 정의.        이 구성 요소는 SQL Server CEIP 서비스에서 업로드되지 않습니다. 고객에 대한 참조로만 로컬 감사에 포함됩니다.| SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolyBaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolyBaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version
|queryTimeInTicks | 다음 추적 범주가 포함된 쿼리를 실행하는 데 소요되는 기간: (SQLServerXeQueries, SQLServerPeriodicQueries) |  0 
 
### <a name="trace-categories"></a>추적 범주 
현재 다음 추적 범주를 수집합니다. 

- **SQLServerXeQueries**: 확장 이벤트 세션을 통해 수집된 데이터 요소를 포함합니다.
- **SQLServerPeriodicQueries**: SQL Server 인스턴스에서 실행되는 주기적인 쿼리를 통해 수집된 데이터 요소를 포함합니다.
- **SQLServerPerDBPeriodicQueries**: SQL Server 인스턴스에서 최대 30개의 데이터베이스를 실행하는 정기 쿼리를 통해 수집된 데이터 요소를 포함합니다.
- **SQLServerOneSettingsException**: 스키마 및/또는 쿼리 집합 업데이트와 관련된 예외 메시지를 포함합니다.
- **DigitalProductID**: SQL Server 인스턴스의 익명 처리되어 해시된 디지털 제품 ID(SHA-256)를 집계하는 데 사용되는 데이터 요소를 포함합니다. 

### <a name="local-audit-file-examples"></a>로컬 감사 파일 예제



다음은 로컬 감사의 JSON 파일 출력의 일부입니다.

```JSON
[
  {
    "instanceUniqueId": "888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:27:59.7031518Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 18,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "2",
        "SqlPbInstalled": "1",
        "SqlPbNodeRole": "Head",
        "SqlVersionMajor": "14",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "3025",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU6",
        "ProductUpdateReference": "KB4101464",
        "ProductRevision": "34",
        "SQLEditionId": "1872460670",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "1",
        "PacketReceived": "422",
        "Version": "Microsoft SQL Server 2017 (RTM-CU6) (KB4101464) - 14.0.3025.34 (X64) \n\tApr  9 2018 18:00:41 \n\tCopyright (C) 2017 Microsoft Corporation\n\tEnterprise Edition: Core-based Licensing (64-bit) on Windows 10 Enterprise 10.0 <X64> (Build 16299: )\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY('Collation') AS [Collation],\n      SERVERPROPERTY('IsFullTextInstalled') AS [SqlFTinstalled],\n      SERVERPROPERTY('IsIntegratedSecurityOnly') AS [SqlIntSec],\n      SERVERPROPERTY('IsSingleUser') AS [IsSingleUser],\n      SERVERPROPERTY ('FileStreamEffectiveLevel') AS [SqlFilestreamMode],\n      SERVERPROPERTY('IsPolyBaseInstalled') AS [SqlPbInstalled],\n      SERVERPROPERTY('PolyBaseRole') AS [SqlPbNodeRole],\n      SERVERPROPERTY('ProductMajorVersion') AS [SqlVersionMajor],\n      SERVERPROPERTY('ProductMinorVersion') AS [SqlVersionMinor],\n      SERVERPROPERTY('ProductBuild') AS [SqlVersionBuild],\n      SERVERPROPERTY('ProductBuildType') AS ProductBuildType,\n      SERVERPROPERTY('ProductLevel') AS ProductLevel,\n      SERVERPROPERTY('ProductUpdateLevel') AS ProductUpdateLevel,\n      SERVERPROPERTY('ProductUpdateReference') AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)),CHARINDEX('.', REVERSE(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY('EditionID') AS SQLEditionId,\n      SERVERPROPERTY('IsClustered') AS IsClustered,\n      SERVERPROPERTY('IsHadrEnabled') AS IsHadrEnabled,\n      SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  },
  {
    "instanceUniqueId": "8884F770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:28:00.9025999Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 23,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "OsSysInfo.003",
    "data": [
      {
        "LogicalCPUCount": "8",
        "HyperthreadRatio": "8",
        "PhysicalMemoryMB": "32710.902343",
        "SQLServerStartTime": "05/04/2018 08:22:30",
        "AffinityTypeDesc": "AUTO",
        "VirtualMachineType": "0",
        "SocketCount": "1",
        "CoresPerSocket": "4",
        "NumaNodeCount": "1",
        "ContainerType": "0",
        "ContainerDescription": "NONE"
      }
    ],
    "query": "SELECT\n      cpu_count AS LogicalCPUCount,\n      hyperthread_ratio AS HyperthreadRatio,\n      physical_memory_kb/1024.0 AS PhysicalMemoryMB,\n      sqlserver_start_time AS SQLServerStartTime,\n      affinity_type_desc AS AffinityTypeDesc,\n      virtual_machine_type AS VirtualMachineType,\n      socket_count as SocketCount,\n      cores_per_socket as CoresPerSocket,\n      numa_node_count as NumaNodeCount,\n      container_type as ContainerType,\n      container_type_desc as ContainerDescription\n      FROM sys.dm_os_sys_info WITH(nolock)",
    "queryTimeInTicks": 0
  }
]
```
## <a name="frequently-asked-questions"></a>질문과 대답

**DBA는 로컬 감사 로그 파일을 어떻게 읽나요?**
이러한 로그 파일은 JSON 형식으로 기록됩니다. 각 줄은 Microsoft에 업로드되는 사용 현황/진단 데이터 부분을 나타내는 JSON 개체가 됩니다. 필드 이름은 자체로 설명 가능해야 합니다.

**DBA가 사용 현황 및 진단 데이터 수집을 사용하지 않도록 설정하면 어떻게 되나요?**
로컬 감사 파일이 기록되지 않습니다.

**인터넷에 연결되지 않았거나 컴퓨터가 방화벽으로 보호되는 경우에는 어떻게 되나요?**
SQL Server 사용 현황 및 진단 데이터를 Microsoft로 보내지 않습니다. 올바르게 구성된 경우에는 계속해서 로컬 감사 로그를 작성하려고 시도합니다.

**DBA가 로컬 감사를 사용하지 않도록 설정하려면 어떻게 해야 하나요?**
UserRequestedLocalAuditDirectory 레지스트리 키 항목을 제거합니다.

**로컬 감사 로그 파일을 읽을 수 있는 사람은 누구인가요?**
조직에서 로컬 감사 디렉터리에 액세스할 수 있는 사람은 누구나 읽을 수 있습니다.

**DBA가 지정된 디렉터리에 기록된 로그 파일을 관리하려면 어떻게 하나요?**
DBA는 디스크 공간을 너무 많이 사용하지 않도록 디렉터리에서 파일의 정리를 스스로 관리해야 합니다.

**이 JSON 출력을 읽는 데 사용하는 클라이언트 또는 도구가 있나요?**
메모장, Visual Studio 또는 어떤 JSON 판독기든지 사용자가 선택하여 출력을 읽을 수 있습니다.
또는 JSON 파일을 읽고 아래와 같이 SQL Server 인스턴스에서 데이터를 분석할 수 있습니다. SQL Server에서 JSON 파일을 읽는 방법에 대한 자세한 내용은 [Importing JSON files into SQL Server using OPENROWSET (BULK) and OPENJSON (Transact-SQL)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/10/07/bulk-importing-json-files-into-sql-server/)(OPENROWSET(BULK) 및 OPENJSON(TRANSACT-SQL)를 사용하여 SQL Server로 JSON 파일 가져오기)을 참조하세요.

```Transact-SQL
DECLARE @JSONFile AS VARCHAR(MAX)

-- Read the JSON file into variable 
SELECT @JSONFile = BulkColumn 
FROM OPENROWSET (BULK 'C:\SQLCEIPAudit\MSSQLSERVER\2016-09-08.json', SINGLE_CLOB) MyFile 

-- Check if the JSON file has been read properly and if it's in a JSON format
SELECT 
    @JSONFile LocalAuditOutput, 
    ISJSON(@JSONFile) IsFileInJSONFormat

-- Get the query identifier, query and the data (output of the query)   
SELECT 
    sequence,
    queryIdentifier,
    query,
    data
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON)
-- Get specific details about the output of "DatabaseProperties.001" query  
SELECT 
    QueryIdentifier,
    DatabaseID,
    CompatibilityLevel,
    IsQueryStoreOn
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON) 
    CROSS APPLY OPENJSON(data) 
        WITH (   DatabaseID varchar(128) '$.database_id'
                ,CompatibilityLevel varchar(128) '$.compatibility_level'
                ,IsQueryStoreOn varchar(128) '$.QS'
             )
WHERE queryIdentifier = 'DatabaseProperties.001'
```

## <a name="see-also"></a>참조
[SSMS 사용 현황 및 진단 데이터 수집에 대한 로컬 감사](../ssms/sql-server-management-studio-telemetry-ssms.md)
