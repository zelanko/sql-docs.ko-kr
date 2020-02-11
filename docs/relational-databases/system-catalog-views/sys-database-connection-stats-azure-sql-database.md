---
title: sys.database_connection_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7eb05640fbc702d5c9b01081d462e2c9f0204457
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73844466"
---
# <a name="sysdatabase_connection_stats-azure-sql-database"></a>sys.database_connection_stats(Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **데이터베이스 연결 이벤트에** 대 한 통계를 포함 하 여 데이터베이스 연결 성공 및 실패에 대 한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 개요를 제공 합니다. 연결 이벤트에 대 한 자세한 내용은 [event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)에서 이벤트 유형을 참조 하세요.  
  
|통계|Type|Description|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|데이터베이스 이름|  
|**start_time**|**datetime2**|집계 간격 시작의 UTC 날짜 및 시간입니다. 시간은 항상 5분의 배수입니다. 다음은 그 예입니다.<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|집계 간격 끝의 UTC 날짜 및 시간입니다. **End_time** 은 항상 같은 행에 있는 해당 **start_time** 보다 정확히 5 분 후입니다.|  
|**success_count**|**int**|성공한 연결 수:|  
|**total_failure_count**|**int**|실패한 연결의 총 수입니다. **Connection_failure_count**, **terminated_connection_count**및 **throttled_connection_count**의 합계 이며, 교착 상태 이벤트를 포함 하지 않습니다.|  
|**connection_failure_count**|**int**|로그인 실패 횟수입니다.|  
|**terminated_connection_count**|**int**|**_V11에 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 만 적용 됩니다._**<br /><br /> 종료된 연결 수:|  
|**throttled_connection_count**|**int**|**_V11에 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 만 적용 됩니다._**<br /><br /> 정체된 연결 수입니다.|  
  
## <a name="remarks"></a>설명  
  
### <a name="event-aggregation"></a>이벤트 집계

 5분 간격 이내로 이 뷰에 이벤트 정보가 수집 및 집계됩니다. 개수 열은 지정된 시간 간격 이내에 특정 데이터베이스에 대해 발생한 특정 연결 이벤트 횟수를 나타냅니다.  
  
 예를 들어, 사용자가 2012년 2월 5일 오전 11시와 11시 5분 사이에 데이터베이스 Database1에 대한 연결을 7회 실패한 경우 이 정보는 이 뷰의 단일 행에서 확인할 수 있습니다.  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-start_time-and-end_time"></a>간격 start_time 및 end_time

 이벤트는 *이벤트가 발생 하거나* **start_time** 된 _후_또는 해당 간격에 대해**end_time** _되기 전에_집계 간격에 포함 됩니다. 예를 들어, 정확히 `2012-10-30 19:25:00.0000000`에 발생하는 이벤트는 아래에 표시된 초 간격에만 표시됩니다.  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>데이터 업데이트

 이 뷰의 데이터는 시간의 경과에 따라 축적됩니다. 일반적으로 데이터는 집계 간격 시작 1시간 이내로 축적되지만 뷰에 모든 데이터가 나타나는 데 최대 24시간이 걸릴 수 있습니다. 그 시간 동안 단일 행 내에서 정보가 주기적으로 업데이트될 수 있습니다.  
  
### <a name="data-retention"></a>데이터 보존

 이 뷰의 데이터는 최대 30 일 동안 보존 됩니다. 데이터베이스 수와 각 데이터베이스가 생성 하는 고유 이벤트의 수에 따라 더 적을 수 있습니다. 이 정보를 더 오래 유지하려면 데이터를 별도의 데이터베이스에 복사합니다. 뷰의 초기 복사본을 만든 후 데이터가 축적됨에 따라 이 행이 업데이트될 수 있습니다. 데이터 복사본을 최신으로 유지하려면 행을 정기적으로 테이블 검색하여 기존 행의 이벤트 수 증가를 확인하고 (시작 및 종료 시간을 사용하여 고유한 행을 식별하여) 새 행을 식별한 다음 데이터 복사본에 변경 내용을 업데이트합니다.  
  
### <a name="errors-not-included"></a>포함되지 않은 오류

 이 뷰에는 일부 연결 및 오류 정보가 포함되지 않을 수 있습니다.  
  
- 이 뷰에는 발생할 수 있는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 모든 데이터베이스 오류가 포함 되어 있지 않습니다. Event_log의 이벤트 유형에 지정 된 오류 [&#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
- 데이터 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 센터 내에 컴퓨터 오류가 발생 하면 이벤트 테이블에서 소량의 데이터가 누락 될 수 있습니다.  
  
- DoSGuard를 통해 IP 주소를 차단하는 경우 해당 IP 주소로부터의 연결 시도 이벤트는 수집할 수 없으며 이 뷰에 나타나지 않습니다.  
  
## <a name="permissions"></a>사용 권한

 **Master** 데이터베이스에 액세스할 수 있는 권한이 있는 사용자에 게는이 뷰에 대 한 읽기 전용 액세스 권한이 있습니다.  
  
## <a name="example"></a>예제

 다음 예에서는 **database_connection_stats** 의 쿼리를 보여 줍니다 .이 쿼리는 정오 9/25/2011 및 정오 9/28/2011 (UTC) 사이에 발생 한 데이터베이스 연결의 요약을 반환 합니다. 기본적으로 쿼리 결과는 **start_time** (오름차순) 순으로 정렬 됩니다.  
  
```sql
SELECT *  
FROM sys.database_connection_stats
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  

## <a name="see-also"></a>참고 항목

 [Azure SQL Database에 대한 연결 문제 해결](/azure/sql-database/sql-database-troubleshoot-common-connection-issues)  
  
  
