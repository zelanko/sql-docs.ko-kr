---
title: "dbo.slo_assignment_history (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/10/2016
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
- slo_assignment_history_TSQL
- dbo.slo_assignment_history_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_assignment_history
- slo_assignment_history
ms.assetid: 048a6fb5-2fc2-4d12-a436-4c53ecd413f3
caps.latest.revision: "9"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61bf1f0541df9085235dc00072624e1e91425cc5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="dbosloassignmenthistory-azure-sql-database"></a>dbo.slo_assignment_history(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  **이만 적용 됩니다 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 합니다.**  
>   
>  이 기능은 미리 보기 상태입니다. 이 기능은 향후 릴리스에서 변경되거나 제거될 수 있으므로 이 기능의 특정 구현에 의존하지 마세요.  
  
 다음을 포함하여 서버에서의 데이터베이스 SLO 할당 기록을 반환합니다.  
  
-   서버에서의 데이터베이스 SLO 할당 기록입니다.  
  
-   각 데이터베이스 SLO 변경 요청의 시작 및 종료 시간입니다.  
  
-   error_code 및 error_desc 열에 기록된 SLO 할당 오류입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_name|**sysname**|데이터베이스의 이름입니다.|  
|database_id|**int**|데이터베이스의 ID입니다.|  
|create_date|**(7)**|데이터베이스 생성 날짜입니다.|  
|service_objective_name|**sysname**|SLO(서비스 수준 목표)의 이름입니다.|  
|service_objective_id|**uniqueidentifier**|SLO의 ID입니다.|  
|operation_id|**uniqueidentifier**|작업의 ID입니다.|  
|operation_start_time|**(7)**|데이터베이스 SLO 변경 요청의 시작 시간입니다.|  
|operation_end_time|**(7)**|데이터베이스 SLO 변경 요청의 종료 시간입니다.|  
|error_code|**int**|데이터베이스 SLO 변경 요청의 오류 코드입니다.|  
|error_desc|**nvarchar**|데이터베이스 SLO 변경 요청의 오류에 대한 설명입니다.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰는 가상에 연결할 수 있는 권한 가진 모든 사용자 역할에 사용할 수 있는 **마스터** 데이터베이스입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 데이터베이스에 대한 데이터베이스 SLO 할당 기록을 반환합니다.  
  
```  
SELECT *  
FROM dbo.slo_assignment_history   
WHERE database_name = '<DB NAME>’   
ORDER BY operation_start_time DESC;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Premium 데이터베이스 관리](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
