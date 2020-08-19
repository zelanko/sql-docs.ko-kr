---
description: sys.dm_clr_tasks(Transact-SQL)
title: sys. dm_clr_tasks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 051d8aa26cde254bb584d4c06884ac0076f7fbbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447756"
---
# <a name="sysdm_clr_tasks-transact-sql"></a>sys.dm_clr_tasks(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 실행되고 있는 각 CLR(공용 언어 런타임) 태스크에 대해 행을 반환합니다. CLR 루틴에 대한 참조를 포함하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리는 해당 일괄 처리에 있는 모든 관리 코드의 실행에 대해 별개의 태스크를 만듭니다. 관리 코드 실행이 필요한 일괄 처리의 여러 문은 같은 CLR 태스크를 사용합니다. CLR 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 공용 언어 런타임 간의 전환뿐 아니라 관리 코드 실행과 관련된 개체 및 상태의 유지 관리도 담당합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|CLR 태스크의 주소입니다.|  
|**sos_task_address**|**varbinary(8)**|기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 태스크의 주소입니다.|  
|**appdomain_address**|**varbinary(8)**|이 태스크가 실행되고 있는 애플리케이션 도메인의 주소입니다.|  
|**상태**|**nvarchar(128)**|태스크의 현재 상태입니다.|  
|**abort_state**|**nvarchar(128)**|태스크가 취소된 경우 중단의 현재 상태입니다. 작업을 중단한 동안 여러 상태가 관련되어 있습니다.|  
|**type**|**nvarchar(128)**|태스크 유형입니다.|  
|**affinity_count**|**int**|태스크의 선호도입니다.|  
|**forced_yield_count**|**int**|태스크가 강제로 생성된 횟수입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

