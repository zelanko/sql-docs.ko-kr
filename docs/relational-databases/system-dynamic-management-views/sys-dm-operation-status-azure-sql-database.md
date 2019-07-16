---
title: sys.dm_operation_status (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d9ce81a0d7aad6b41945b1564076004db80cd5e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900275"
---
# <a name="sysdmoperationstatus-azure-sql-database"></a>sys.dm_operation_status(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버의 데이터베이스에 대해 수행된 작업 정보를 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|작업의 ID입니다. Null이 아닙니다.|  
|resource_type|**int**|작업이 수행된 리소스의 유형을 나타냅니다. Null이 아닙니다. 현재 릴리스에서 이 뷰는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 수행된 작업을 추적하며 해당 정수 값은 0입니다.|  
|resource_type_desc|**nvarchar(2048)**|작업이 수행된 리소스 유형에 대한 설명입니다. 현재 릴리스에서 이 뷰는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서만 수행된 작업을 추적합니다.|  
|major_resource_id|**sql_variant**|작업이 수행된 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 이름입니다. Null이 아닙니다.|  
|minor_resource_id|**sql_variant**|내부 전용입니다. Null이 아닙니다.|  
|operation(작업)|**nvarchar(60)**|CREATE 또는 ALTER와 같이 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 수행된 작업입니다.|  
|state|**tinyint**|작업의 상태입니다.<br /><br /> 0 = 보류 중<br />1 = 진행 중<br />2 = 완료됨<br />3 = 실패<br />4 = 취소됨|  
|state_desc|**nvarchar(120)**|PENDING = 작업이 리소스나 할당량을 사용할 수 있을 때까지 대기 중입니다.<br /><br /> IN_PROGRESS = 작업이 시작되었고 진행 중입니다.<br /><br /> COMPLETED = 작업이 성공적으로 완료되었습니다.<br /><br /> FAILED = 작업이 실패했습니다. 참조 된 **error_desc** 세부 정보에 대 한 열입니다.<br /><br /> CANCELLED = 작업이 사용자 요청으로 중지되었습니다.|  
|percent_complete|**int**|완료된 작업의 백분율입니다. 값 연속 되지 않으며 유효한 값은 아래 나열 됩니다. NULL이 아닙니다.<br/><br/>0 = 작업이 시작 되지 않음<br/>50 = 작업이 진행 중<br/>100 = 작업 완료|  
|error_code|**int**|실패한 작업 중에 발생한 오류를 나타내는 코드입니다. 값이 0이면 작업이 성공적으로 완료되었음을 나타냅니다.|  
|error_desc|**nvarchar(2048)**|실패한 작업 중에 발생한 오류에 대한 설명입니다.|  
|error_severity|**int**|실패한 작업 중에 발생한 오류의 심각도 수준입니다. 오류 심각도 대 한 자세한 내용은 참조 하세요. [데이터베이스 엔진 오류 심각도](https://go.microsoft.com/fwlink/?LinkId=251052)합니다.|  
|error_state|**int**|나중에 사용하도록 예약되어 있습니다. 향후 호환성은 보장되지 않습니다.|  
|start_time|**datetime**|작업이 시작된 타임스탬프입니다.|  
|last_modify_time|**datetime**|장기 실행 작업에 대해 레코드가 마지막으로 수정된 타임스탬프입니다. 완료된 작업의 경우 이 필드에는 작업 완료 시간의 타임스탬프가 표시됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 보기는 에서만 사용할 수는 **마스터** 데이터베이스 서버 수준 보안 주체 로그인 합니다.  
  
## <a name="remarks"></a>설명  
 이 뷰를 사용 하려면 연결 해야 하는 **마스터** 데이터베이스입니다. 사용 하 여는 `sys.dm_operation_status` 에서 볼를 **마스터** 데이터베이스를 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에서 수행 된 다음 작업의 상태를 추적 하는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]:  
  
-   데이터베이스 만들기  
  
-   데이터베이스 복사. 데이터베이스 복사는 원본 서버와 대상 서버 모두에서 이 뷰에 레코드를 만듭니다.  
  
-   데이터베이스 변경  
  
-   서비스 계층의 성능 수준 변경  
  
-   데이터베이스의 서비스 계층을 변경합니다(예: Basic에서 Standard로 변경).  
  
-   지역 복제 관계 설정  
  
-   지역 복제 관계 종료  
  
-   대화 상자의  
  
-   데이터베이스 삭제  
  
## <a name="example"></a>예제  
 데이터베이스 'mydb'를 사용 하 여 연결 하는 가장 최근의 지역에서 복제 작업을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_ operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>관련 항목  
 [지리적 복제 동적 관리 뷰 및 함수 &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
