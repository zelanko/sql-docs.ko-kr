---
title: SERVERPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/08/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SERVERPROPERTY_TSQL
- SERVERPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SERVERPROPERTY function
- server instance property information [SQL Server]
- IsHadrEnabled server property
- instances of SQL Server, property information
- server properties [SQL Server]
ms.assetid: 11e166fa-3dd2-42d8-ac4b-04f18c612c4a
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97979dbef582835c5fcb8a8e3ec04fdf99b5d205
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003663"
---
# <a name="serverproperty-transact-sql"></a>SERVERPROPERTY(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

서버 인스턴스에 대한 속성 정보를 반환합니다.  

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SERVERPROPERTY ( 'propertyname' )  
```  

> [!IMPORTANT]
> SQL Server 및 Azure SQL Database의 데이터베이스 엔진 버전 번호는 서로 비교할 수 없으며 이러한 개별 제품에 대한 내부 빌드 번호에 해당합니다. Azure SQL Database용 데이터베이스 엔진은 SQL Server 데이터베이스 엔진과 동일한 코드 베이스를 기준으로 합니다. 가장 중요한 사실은 Azure SQL Database의 데이터베이스 엔진에 항상 최신 SQL 데이터베이스 엔진 비트가 있다는 것입니다. Azure SQL Database 버전 12는 SQL Server 버전 15보다 최신 버전입니다.

## <a name="arguments"></a>인수  

*propertyname*  
반환될 서버 속성 정보가 포함된 식입니다. *propertyname*은 다음 값 중 하나일 수 있습니다.  
  
|속성|반환된 값|  
|--------------|---------------------|  
|BuildClrVersion|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 작성하는 동안 사용된 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)의 버전입니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|데이터 정렬|서버의 기본 데이터 정렬 이름입니다.<br /><br /> NULL = 입력이 유효하지 않거나 오류입니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|CollationID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 ID입니다.<br /><br /> 기본 데이터 형식: **int**|  
|ComparisonStyle|데이터 정렬의 Windows 비교 스타일입니다.<br /><br /> 기본 데이터 형식: **int**|  
|ComputerNamePhysicalNetBIOS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 현재 실행되고 있는 로컬 컴퓨터의 NetBIOS 이름입니다.<br /><br /> 장애 조치(failover) 클러스터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터형 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 장애 조치 클러스터의 다른 노드로 장애 조치되면 이 값이 변경됩니다.<br /><br /> 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이 값은 일정하게 유지되며 MachineName 속성과 같은 값을 반환합니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 장애 조치(failover) 클러스터에 있는 상태에서 장애 조치 클러스터형 인스턴스 이름을 가져오려는 경우 MachineName 속성을 사용합니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|버전|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치된 제품 버전입니다. 이 속성 값을 이용하여 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)와 같은 기능 및 제한을 확인합니다. 64비트 버전의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에는 (64비트)가 추가됩니다.<br /><br /> HRESULT = NO_ERROR를<br /><br /> 'Enterprise Edition'<br /><br /> 'Enterprise Edition: 코어 기반 라이선스’<br /><br /> 'Enterprise Evaluation Edition'<br /><br /> 'Business Intelligence Edition'<br /><br /> 'Developer Edition'<br /><br /> 'Express Edition'<br /><br /> 'Express Edition with Advanced Services'<br /><br /> 'Standard Edition'<br /><br /> 'Web Edition'<br /><br /> 'SQL Azure'는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 또는 [!INCLUDE[ssDW](../../includes/ssdw-md.md)]를 나타냅니다.<br /><br /> 'Azure SQL Edge Developer'는 Azure SQL Edge 개발 전용 버전을 나타냅니다. <br /><br /> 'Azure SQL Edge'는 Azure SQL Edge의 유료 버전을 나타냅니다. <br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|EditionID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 설치된 제품 버전을 나타내는 EditionID입니다. 이 속성 값을 이용하여 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)와 같은 기능 및 제한을 확인합니다.<br /><br /> 1804890536 = Enterprise<br /><br /> 1872460670 = Enterprise Edition: 코어 기반 라이선스<br /><br /> 610778273= Enterprise Evaluation<br /><br /> 284895786 = Business Intelligence<br /><br /> -2117995310 = Developer<br /><br /> -1592396055 = Express<br /><br /> -133711905 = Express with Advanced Services<br /><br /> -1534726760 = Standard<br /><br /> 1293598313 = Web<br /><br /> 1674378470 = SQL Database 또는 Microsoft Azure Synapse Analytics(이전의 SQL Data Warehouse)<br /><br /> -1461570097 = Azure SQL Edge Developer <br /><br /> 1994083197 = Azure SQL Edge <br /><br />기본 데이터 형식: **bigint**|  
|EngineEdition|서버에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전입니다.<br /><br /> 1 = Personal 또는 Desktop Engine([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에는 사용할 수 없음)<br /><br /> 2 = Standard(Standard, Web 및 Business Intelligence 버전인 경우 이 값이 반환됨)<br /><br /> 3 = Enterprise (Evaluation, Developer 및 Enterprise 버전인 경우 이 값이 반환됨)<br /><br /> 4 = Express(Express, Express with Tools 및 Express with Advanced Services 버전인 경우 이 값이 반환됨)<br /><br /> 5 = [!INCLUDE[ssSDS](../../includes/sssds-md.md)]<br /><br /> 6 = [!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> 8 = 관리되는 인스턴스<br /><br /> 9 = Azure SQL Edge(Azure SQL Edge 두 가지 버전 모두에 대해 반환됨)<br /><br /> 기본 데이터 형식: **int**|  
|HadrManagerStatus|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 관리자가 시작되었는지 여부를 나타냅니다.<br /><br /> 0 = 시작되지 않았습니다. 통신 보류 중입니다.<br /><br /> 1 = 시작되어 실행 중입니다.<br /><br /> 2 = 시작되지 않고 실패했습니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.|  
|InstanceDefaultDataPath|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 인스턴스 데이터 파일의 기본 경로 이름입니다.|  
|InstanceDefaultLogPath|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 인스턴스 로그 파일의 기본 경로 이름입니다.|  
|InstanceName|사용자가 연결된 인스턴스의 이름입니다.<br /><br /> 인스턴스 이름이 기본 인스턴스이거나 입력이 유효하지 않거나 오류일 경우에는 NULL을 반환합니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|IsAdvancedAnalyticsInstalled|설치 중에 Advanced Analytics 기능이 설치되어 있으면 1을, Advanced Analytics가 설치되어 있지 않으면 0을 반환합니다.|  
|IsBigDataCluster| [!INCLUDE[ssSQL2019](../../includes/sssqlv15-md.md)] CU4부터 도입되었습니다.<br /><br />인스턴스가 빅 데이터 클러스터 SQL Server이면 1을 반환하고, 그렇지 않으면 0을 반환합니다.|  
|IsClustered|서버 인스턴스가 장애 조치(failover) 클러스터에 구성되어 있습니다.<br /><br /> 1 = 클러스터형입니다.<br /><br /> 0 = 비클러스터형입니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|IsFullTextInstalled|전체 텍스트 및 의미 체계 인덱싱 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 설치되었습니다.<br /><br /> 1 = 전체 텍스트 및 의미 체계 인덱싱 구성 요소가 설치되었습니다.<br /><br /> 0 = 전체 텍스트 및 의미 체계 인덱싱 구성 요소가 설치되지 않았습니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|IsHadrEnabled|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 이 서버 인스턴스에서 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 사용합니다.<br /><br /> 0 = [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 기능을 사용하지 않습니다.<br /><br /> 1 = [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 기능을 사용합니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 가용성 복제본을 만들고 실행하려면 서버 인스턴스에서 HADR 서비스를 사용하도록 설정해야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화(SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.<br /><br /> **참고:** IsHadrEnabled 속성은 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]에만 적용됩니다. 데이터베이스 미러링 또는 로그 전달 등의 다른 고가용성 또는 재해 복구 기능은 이 서버 속성의 영향을 받지 않습니다.|  
|IsIntegratedSecurityOnly|서버가 통합 보안 모드에 있습니다.<br /><br /> 1 = 통합 보안(Windows 인증)<br /><br /> 0 = 통합 보안 모드가 아닙니다. Windows 인증 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이라는 두 가지 인증 모드를 사용할 수 있습니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|IsLocalDB|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 서버가 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] LocalDB의 인스턴스입니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.|  
|IsPolyBaseInstalled|**적용 대상**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 서버 인스턴스에 PolyBase 기능이 설치되어 있는지 여부를 반환합니다.<br /><br /> 0 = PolyBase가 설치되어 있지 않습니다.<br /><br /> 1 = PolyBase가 설치되어 있습니다.<br /><br /> 기본 데이터 형식: **int**|  
|IsSingleUser|서버가 단일 사용자 모드입니다.<br /><br /> 1 = 단일 사용자 모드입니다.<br /><br /> 0 = 단일 사용자 모드가 아닙니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|IsXTPSupported|**적용 대상**: SQL Server([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> 서버에서 메모리 OLTP를 지원합니다.<br /><br /> 1= 서버에서 메모리 OLTP를 지원합니다.<br /><br /> 0 = 서버에서 메모리 OLTP를 지원하지 않습니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|LCID|데이터 정렬의 Windows LCID(로캘 ID)입니다.<br /><br /> 기본 데이터 형식: **int**|  
|LicenseType|사용되지 않습니다. 라이선스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품에서 보존 또는 유지 관리되지 않습니다. 항상 DISABLED를 반환합니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|MachineName|서버 인스턴스가 실행 중인 Windows 컴퓨터 이름입니다.<br /><br /> Microsoft Cluster Service의 가상 서버에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터형 인스턴스인 경우에는 가상 서버의 이름을 반환합니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|NumLicenses|사용되지 않습니다. 라이선스 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품에서 보존 또는 유지 관리되지 않습니다. 항상 NULL을 반환합니다.<br /><br /> 기본 데이터 형식: **int**|  
|ProcessID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 프로세스 ID입니다. ProcessID는 인스턴스에 속하는 Sqlservr.exe를 식별하는 데 유용합니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.<br /><br /> 기본 데이터 형식: **int**|  
|ProductBuild|**적용 대상**: 2015년 10월부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 적용됩니다.<br /><br /> 빌드 번호입니다.|  
|ProductBuildType|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 현재 빌드의 빌드 형식입니다.<br /><br /> 다음 중 하나를 반환합니다.<br /><br /> OD = 요청 시 특정 고객을 릴리스합니다.<br /><br /> GDR = Windows 업데이트를 통해 릴리스된 일반 배포 릴리스입니다.<br /><br /> NULL<br />= 해당 사항이 없습니다.|  
|ProductLevel|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 버전 수준입니다.<br /><br /> 다음 중 하나를 반환합니다.<br /><br /> 'RTM' = 초기 릴리스 버전<br /><br /> 'SP*n*' = 서비스 팩 버전<br /><br /> 'CTP*n*', = Community Technology Preview 버전<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|ProductMajorVersion|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 주 버전|  
|ProductMinorVersion|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 부 버전|  
|ProductUpdateLevel|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 현재 빌드의 업데이트 수준입니다. CU는 누적 업데이트를 나타냅니다.<br /><br /> 다음 중 하나를 반환합니다.<br /><br /> CU*n* = 누적 업데이트<br /><br /> NULL<br />= 해당 사항이 없습니다.|  
|ProductUpdateReference|**적용 대상**: 2015년 후반부터 업데이트된 현재 버전을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 적용됩니다.<br /><br /> 해당 릴리스에 대한 기술 자료 문서입니다.|  
|ProductVersion|'*major.minor.build.revision*’ 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 버전입니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|ResourceLastUpdateDateTime|리소스 데이터베이스를 마지막으로 업데이트한 날짜와 시간을 반환합니다.<br /><br /> 기본 데이터 형식: **datetime**|  
|ResourceVersion|리소스 데이터베이스 버전을 반환합니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|ServerName|Windows 서버 및 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 인스턴스 정보입니다.<br /><br /> NULL = 입력이 유효하지 않거나 오류입니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|SqlCharSet|데이터 정렬 ID의 SQL 문자 집합 ID입니다.<br /><br /> 기본 데이터 형식: **tinyint**|  
|SqlCharSetName|데이터 정렬의 SQL 문자 집합 이름입니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|SqlSortOrder|데이터 정렬의 SQL 정렬 순서 ID입니다.<br /><br /> 기본 데이터 형식: **tinyint**|  
|SqlSortOrderName|데이터 정렬의 SQL 정렬 순서 이름입니다.<br /><br /> 기본 데이터 형식: **nvarchar(128)**|  
|FilestreamShareName|FILESTREAM이 사용하는 공유의 이름입니다.<br /><br /> NULL = 입력이 유효하지 않거나, 오류이거나, 적용 가능하지 않습니다.|  
|FilestreamConfiguredLevel|구성된 FILESTREAM 액세스 수준입니다. 자세한 내용은 [파일 스트림 액세스 수준](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)을 참조하세요.|  
|FilestreamEffectiveLevel|유효한 FILESTREAM 액세스 수준입니다. 수준이 변경되었고 인스턴스 다시 시작이나 컴퓨터 다시 시작이 보류 중인 경우 이 값은 FilestreamConfiguredLevel과 다를 수 있습니다. 자세한 내용은 [파일 스트림 액세스 수준](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)을 참조하세요.|  
  
## <a name="return-types"></a>반환 형식  

**sql_variant**
  
## <a name="remarks"></a>설명  
  
### <a name="servername-property"></a>ServerName 속성

`SERVERPROPERTY` 함수의 `ServerName` 속성과 [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)은 비슷한 정보를 반환합니다. `ServerName` 속성은 고유한 서버 인스턴스를 구성하는 인스턴스 이름과 Windows 서버를 제공합니다. [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)은 현재 구성된 로컬 서버 이름을 제공합니다.  
  
설치 시 기본 서버 이름이 변경되지 않은 경우 `ServerName`속성과 [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)은 같은 정보를 반환합니다. 로컬 서버 이름은 다음을 실행하여 구성할 수 있습니다.  
  
```sql
EXEC sp_dropserver 'current_server_name';  
GO  
EXEC sp_addserver 'new_server_name', 'local';  
GO  
```  
  
설치 시 로컬 서버 이름을 기본 서버 이름에서 다른 이름으로 변경한 경우 [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)은 새 이름을 반환합니다.  
  
### <a name="version-properties"></a>Version 속성

`SERVERPROPERTY` 함수는 버전 정보에 관련된 개별 속성을 반환하지만 [@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md) 함수는 출력을 하나의 문자열로 결합합니다. 애플리케이션이 개별 속성 문자열이 필요한 경우 [@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md) 결과를 구문 분석하는 대신 `SERVERPROPERTY` 함수를 사용하여 이러한 속성 문자열을 반환할 수 있습니다.  

## <a name="permissions"></a>사용 권한

모든 사용자가 서버 속성을 쿼리할 수 있습니다.
  
## <a name="examples"></a>예제

다음 예에서는 `SELECT` 문에서 `SERVERPROPERTY` 함수를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 대한 정보를 반환합니다.
  
```sql
SELECT  
  SERVERPROPERTY('MachineName') AS ComputerName,
  SERVERPROPERTY('ServerName') AS InstanceName,  
  SERVERPROPERTY('Edition') AS Edition,
  SERVERPROPERTY('ProductVersion') AS ProductVersion,  
  SERVERPROPERTY('ProductLevel') AS ProductLevel;  
GO  
```  
  
## <a name="see-also"></a>참고 항목

[SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)  
