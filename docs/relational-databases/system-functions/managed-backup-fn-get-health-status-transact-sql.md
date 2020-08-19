---
description: managed_backup. fn_get_health_status (Transact-sql)
title: managed_backup. fn_get_health_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_health_status_TSQL
- smart_admin.fn_get_health_status_TSQL
- smart_admin.fn_get_health_status
- fn_get_health_status
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_health_status
- fn_get_health_status
ms.assetid: b376711d-444a-4b5e-b483-8df323b4e31f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4aa10efc95af42c7793fb37b49a72061353b0ee0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419557"
---
# <a name="managed_backupfn_get_health_status-transact-sql"></a>managed_backup. fn_get_health_status (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  지정된 기간 동안 확장 이벤트에서 보고한 집계된 오류 수의 행을 0개, 1개 또는 그 이상 포함하는 테이블을 반환합니다.  
  
 함수는 Smart Admin에서 서비스의 상태를 보고 하는 데 사용 됩니다.  현재 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 스마트 관리 파라솔에서 지원 됩니다. 따라서 반환되는 오류는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 관련이 있습니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_get_health_status([@begin_time = ] 'time_1' , [ @end_time = ] 'time_2')  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 [@begin_time]  
 집계된 오류 수가 계산되는 기간의 시작입니다.  @begin_time매개 변수가 DATETIME입니다. 기본값은 NULL입니다. 값이 NULL인 경우 함수는 현재 시간 30분 전부터 보고된 이벤트를 처리합니다.  
  
 [ @end_time]  
 집계된 오류 수가 계산되는 기간의 끝입니다. @end_time매개 변수는 DATETIME 이며 기본값은 NULL입니다. 값이 NULL인 경우 함수는 현재 시간까지의 확장 이벤트를 처리합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|number_of_storage_connectivity_errors|int|프로그램이 Azure storage 계정에 연결 하는 경우 연결 오류 횟수입니다.|  
|number_of_sql_errors|int|프로그램에서 SQL Server 엔진에 연결할 때 반환되는 오류 수입니다.|  
|number_of_invalid_credential_errors|int|프로그램에서 SQL 자격 증명을 사용하여 인증하려고 할 때 반환되는 오류 수입니다.|  
|number_of_other_errors|int|연결, SQL 또는 자격 증명 이외의 다른 범주에 속하는 오류 수입니다.|  
|number_of_corrupted_or_deleted_backups|int|삭제되거나 손상된 백업 파일 수입니다.|  
|number_of_backup_loops|int|백업 에이전트가 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하여 구성된 모든 데이터베이스를 검색하는 횟수입니다.|  
|number_of_retention_loops|int|설정된 보존 기간을 평가하기 위해 데이터베이스가 검색되는 횟수입니다.|  
  
## <a name="best-practices"></a>모범 사례  
 이 집계 수는 시스템 상태를 모니터링하는 데 사용될 수 있습니다. 예를 들어 number_of_retention_loops 열이 30분 동안 0인 경우 보존 관리가 시간이 오래 걸리고 있거나 제대로 작동하지 않고 있을 가능성이 있습니다. 0이 아닌 오류 열은 문제를 나타낼 수 있으며 문제에 대해 알아보려면 확장 이벤트 로그를 확인해야 합니다. 또는 저장 프로시저 **managed_backup sp_get_backup_diagnostics** 사용 하 여 오류에 대 한 세부 정보를 찾는 확장 이벤트 목록을 가져옵니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 함수에 대 한 **SELECT** 권한이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
-   다음 예에서는 실행된 시간 이전의 마지막 30분 동안 집계된 오류 수를 반환합니다.  
  
    ```  
    SELECT *  
    FROM managed_backup.fn_get_health_status(NULL, NULL)  
  
    ```  
  
-   다음 예에서는 현재 주에 집계된 오류 수를 반환합니다.  
  
    ```  
    Use msdb  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
    SELECT *  
    FROM managed_backup.fn_get_health_status(@startofweek, @endofweek)  
  
    ```  
  
  
