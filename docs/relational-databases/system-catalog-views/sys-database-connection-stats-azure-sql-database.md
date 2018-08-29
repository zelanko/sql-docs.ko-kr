---
title: sys.database_connection_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0bd0c0bba93fbc01120705cccb07ff9b2dd146df
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028913"
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  에 대 한 통계를 포함 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터베이스 **연결** 데이터베이스 연결 성공 및 실패 개요를 제공 하는 이벤트입니다. 연결 이벤트에 대 한 자세한 내용은 참조에서 이벤트 유형을 [sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)합니다.  
  
|통계|형식|Description|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|데이터베이스의 이름입니다.|  
|**start_time**|**datetime2**|집계 간격 시작의 UTC 날짜 및 시간입니다. 시간은 항상 5분의 배수입니다. 예를 들어:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|집계 간격 끝의 UTC 날짜 및 시간입니다. **End_time** 정확 하 게 5 분 이상 해당 하는 것은 항상 **start_time** 같은 행에 있습니다.|  
|**success_count**|**int**|성공한 연결 수:|  
|**total_failure_count**|**int**|실패한 연결의 총 수입니다. 이 값은 합계 **connection_failure_count**를 **terminated_connection_count**, 및 **throttled_connection_count**, 교착 상태 이벤트를 포함 하지 않습니다.|  
|**connection_failure_count**|**int**|로그인 실패 횟수입니다.|  
|**terminated_connection_count**|**int**|***에 적용 됩니다 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11.***<br /><br /> 종료된 연결 수:|  
|**throttled_connection_count**|**int**|***에 적용 됩니다 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11.***<br /><br /> 정체된 연결 수입니다.|  
  
## <a name="remarks"></a>Remarks  
  
### <a name="event-aggregation"></a>이벤트 집계  
 5분 간격 이내로 이 뷰에 이벤트 정보가 수집 및 집계됩니다. 개수 열은 지정된 시간 간격 이내에 특정 데이터베이스에 대해 발생한 특정 연결 이벤트 횟수를 나타냅니다.  
  
 예를 들어, 사용자가 2012년 2월 5일 오전 11시와 11시 5분 사이에 데이터베이스 Database1에 대한 연결을 7회 실패한 경우 이 정보는 이 뷰의 단일 행에서 확인할 수 있습니다.  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>간격 start_time 및 end_time  
 이벤트가 발생할 때를 이벤트가 집계 간격에 포함 되는지 *대* 또는 *후 * * * start_time** 및 *하기 전에 * * * end_time** 해당 간격에 대 한 합니다. 예를 들어, 정확히 `2012-10-30 19:25:00.0000000`에 발생하는 이벤트는 아래에 표시된 초 간격에만 표시됩니다.  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>데이터 업데이트  
 이 뷰의 데이터는 시간의 경과에 따라 축적됩니다. 일반적으로 데이터는 집계 간격 시작 1시간 이내로 축적되지만 뷰에 모든 데이터가 나타나는 데 최대 24시간이 걸릴 수 있습니다. 그 시간 동안 단일 행 내에서 정보가 주기적으로 업데이트될 수 있습니다.  
  
### <a name="data-retention"></a>데이터 보존 기간  
 이 뷰의 데이터는 논리적 서버의 데이터베이스 수 및 각 데이터베이스가 생성하는 고유 이벤트 수에 따라 최대 30일 또는 그 이하로 유지됩니다. 이 정보를 더 오래 유지하려면 데이터를 별도의 데이터베이스에 복사합니다. 뷰의 초기 복사본을 만든 후 데이터가 축적됨에 따라 이 행이 업데이트될 수 있습니다. 데이터 복사본을 최신으로 유지하려면 행을 정기적으로 테이블 검색하여 기존 행의 이벤트 수 증가를 확인하고 (시작 및 종료 시간을 사용하여 고유한 행을 식별하여) 새 행을 식별한 다음 데이터 복사본에 변경 내용을 업데이트합니다.  
  
### <a name="errors-not-included"></a>포함되지 않은 오류  
 이 뷰에는 일부 연결 및 오류 정보가 포함되지 않을 수 있습니다.  
  
-   이 뷰에 모두 포함 되지 않습니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터베이스의 이벤트 유형에 지정 된만 발생할 수 있는 오류 [sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)합니다.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터 센터 내에서 시스템 오류가 발생할 경우 논리적 서버에 대한 소량의 데이터가 이벤트 테이블에서 누락될 수 있습니다.  
  
-   DoSGuard를 통해 IP 주소를 차단하는 경우 해당 IP 주소로부터의 연결 시도 이벤트는 수집할 수 없으며 이 뷰에 나타나지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 액세스할 수 있는 권한이 있는 사용자를 **마스터** 데이터베이스에는이 보기에 읽기 전용으로 액세스할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예의 쿼리를 보여 줍니다 **sys.database_connection_stats** 2011 년 9 월 28 / (UTC) 정오와 2011 년 9 월 25 정오 사이 발생 한 데이터베이스 연결에 대 한 요약을 반환 합니다. 기본적으로 쿼리 결과 기준으로 정렬 됩니다 **start_time** (오름차순).  
  
```  
SELECT *  
FROM sys.database_connection_stats   
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  
  
## <a name="see-also"></a>관련 항목  
 [Windows Azure SQL Database 문제 해결](http://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
