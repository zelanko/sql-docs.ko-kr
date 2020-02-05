---
title: ALTER RESOURCE GOVERNOR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2372b07e45e952003f18270995b52eb0f7338c64
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982019"
---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 명령문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다음 Resource Governor 동작을 수행하는 데 사용됩니다.  
  
-   CREATE|ALTER|DROP WORKLOAD GROUP 또는 CREATE|ALTER|DROP RESOURCE POOL 또는 CREATE|ALTER|DROP EXTERNAL RESOURCE POOL 문이 발행될 때 지정된 구성 변경 내용을 적용합니다.  
  
-   리소스 관리자를 사용하거나 사용하지 않도록 설정합니다.  
  
-   들어오는 요청에 대한 분류를 구성합니다.  
  
-   작업 그룹 및 리소스 풀 통계를 다시 설정합니다.  
  
-   디스크 볼륨당 최대 I/O 작업을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 DISABLE  
 리소스 관리자를 사용하지 않습니다. 리소스 관리자를 사용하지 않도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   분류자 함수가 실행되지 않습니다.  
  
-   모든 새 연결이 자동으로 기본 그룹으로 분류됩니다.  
  
-   시스템에서 시작한 요청이 내부 작업 그룹으로 분류됩니다.  
  
-   기존의 모든 작업 그룹 및 리소스 풀 설정이 해당 기본값으로 다시 설정됩니다. 이 경우 제한에 도달해도 이벤트가 발생하지 않습니다.  
  
-   정상적인 시스템 모니터링은 영향을 받지 않습니다.  
  
-   구성을 변경할 수 있지만 리소스 관리자를 사용하도록 설정할 때까지 변경 내용이 적용되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 때 리소스 관리자는 구성을 로드하지 않고 대신 기본 및 내부 그룹과 풀만 사용합니다.  
  
 RECONFIGURE  
 리소스 관리자가 사용되지 않는 경우 RECONFIGURE가 리소스 관리자를 사용하도록 설정합니다. 리소스 관리자를 사용하도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   작업 그룹에 해당 작업을 할당할 수 있도록 새 연결에 대해 분류자 함수가 실행됩니다.  
  
-   리소스 관리자 구성에 지정된 리소스 제한이 강제로 적용됩니다.  
  
-   리소스 관리자를 사용하도록 설정하기 전부터 있던 요청이 리소스 관리자가 사용되지 않을 때 수행된 구성 변경 내용의 영향을 받습니다.  
  
 Resource Governor가 실행되고 있을 때 RECONFIGURE는 CREATE|ALTER|DROP WORKLOAD GROUP 또는 CREATE|ALTER|DROP RESOURCE POOL 또는 CREATE|ALTER|DROP EXTERNAL RESOURCE POOL 문이 실행될 때 요청된 구성 변경 내용을 적용합니다.  
  
> [!IMPORTANT]  
>  구성 변경 내용을 적용하려면 ALTER RESOURCE GOVERNOR RECONFIGURE를 실행해야 합니다.  
  
 CLASSIFIER_FUNCTION = { _schema_name_ **.** _function_name_ | NULL }  
 *schema_name.function_name*으로 지정한 분류 함수를 등록합니다. 이 함수는 모든 새 세션을 분류하고 세션 요청 및 쿼리를 작업 그룹에 할당합니다. NULL이 사용되면 새 세션이 기본 작업 그룹에 자동으로 할당됩니다.  
  
 RESET STATISTICS  
 모든 작업 그룹 및 리소스 풀에 대한 통계를 다시 설정합니다. 자세한 내용은 [sys.dm_resource_governor_workload_groups&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) 및 [sys.dm_resource_governor_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)를 참조하세요.  
  
 MAX_OUTSTANDING_IO_PER_VOLUME = *value*  
 **적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상  
  
 디스크 볼륨당 최대 지연 I/O 작업을 설정합니다. 모든 크기의 읽기 또는 쓰기가 여기에 해당합니다.  MAX_OUTSTANDING_IO_PER_VOLUME의 최대값은 100입니다. 비율이 아닙니다. 이 설정은 디스크 볼륨의 IO 특성에 맞게 IO 리소스 관리를 튜닝하도록 디자인되었습니다. 여러 가지 값을 설정해 보고 IOMeter, [DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223),     또는 SQLIO(사용되지 않음)와 같은 보정 도구를 사용하여 스토리지 하위 시스템의 최댓값을 식별하는 것이 좋습니다. 이 설정은 다른 풀의 MAX_IOPS_PER_VOLUME이 무제한으로 설정되어 있는 경우에도 SQL Server에서 리소스 풀의 최소 IOPS를 충족할 수 있도록 시스템 수준 안전 검사를 제공합니다. MAX_IOPS_PER_VOLUME에 대한 자세한 내용은 [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
 사용자 트랜잭션 내에서는 ALTER RESOURCE GOVERNOR DISABLE, ALTER RESOURCE GOVERNOR RECONFIGURE 및 ALTER RESOURCE GOVERNOR RESET STATISTICS를 사용할 수 없습니다.  
  
 RECONFIGURE 매개 변수는 Resource Governor 구문의 일부이며 별도의 DLL 문인 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md)와 혼동해서는 안 됩니다.  
  
 DDL 문을 실행하기 전에 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-starting-the-resource-governor"></a>A. 리소스 관리자 시작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 처음 설치하면 리소스 관리자를 사용할 수 없습니다. 다음 예에서는 리소스 관리자를 시작합니다. 이 문이 실행된 후에 리소스 관리자가 실행되면 미리 정의된 작업 그룹과 리소스 풀을 사용할 수 있습니다.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. 기본 그룹에 새 세션 할당  
 다음 예에서는 리소스 관리자 구성에서 기존 분류자 함수를 제거하여 기본 작업 그룹에 모든 새 세션을 할당합니다. 분류자 함수로 지정된 함수가 없으면 모든 새 세션이 기본 작업 그룹에 할당됩니다. 이 변경 내용은 새 세션에만 적용되고 기존 세션에는 적용되지 않습니다.  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. 분류자 함수 작성 및 등록  
 다음 예에서는 `dbo.rgclassifier_v1`이라는 분류자 함수를 만듭니다. 이 함수는 사용자 이름이나 애플리케이션 이름을 기반으로 모든 새 세션을 분류하고 특정 작업 그룹에 세션 요청과 쿼리를 할당합니다. 지정한 사용자 또는 애플리케이션으로 매핑되지 않는 세션은 기본 작업 그룹에 할당됩니다. 그런 다음 분류자 함수가 등록되고 구성 변경 내용이 적용됩니다.  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. 통계 다시 설정  
 다음 예에서는 모든 작업 그룹 및 리소스 풀 통계를 다시 설정합니다.  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-max_outstanding_io_per_volume-option"></a>E. MAX_OUTSTANDING_IO_PER_VOLUME 옵션 설정  
 다음 예에서는 MAX_OUTSTANDING_IO_PER_VOLUME 옵션을 20으로 설정합니다.  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.dm_resource_governor_workload_groups&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  
