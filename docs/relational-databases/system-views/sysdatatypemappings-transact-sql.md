---
title: msdb.dbo.sysdatatypemappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a60a558b94b80ac09c752ca6ae2f2afd5b0ef05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758598"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **Msdb.dbo.sysdatatypemappings** 뷰는 SQL SERVER 아닌 DBMS (데이터베이스 관리 시스템)의 데이터 형식과 SQL Server 데이터 형식 간의 매핑을 표시 하는 데 사용 됩니다. 이 뷰는 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|데이터 형식 매핑의 ID입니다.|  
|**source_dbms**|**sysname**|데이터 형식이 매핑된 DBMS의 이름을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **MSSQLSERVER** = 원본이 SQL Server 데이터베이스입니다.<br /><br /> **Oracle** = 원본이 ORACLE 데이터베이스입니다.|  
|**source_version**|**sysname**|원본 DBMS의 제품 버전을 나타냅니다.|  
|**source_type**|**sysname**|원본 DBMS에 나열된 데이터 형식을 나타냅니다.|  
|**source_length_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**source_length_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**source_precision_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**source_precision_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**source_scale_min**|**int**|원본 DBMS에서 해당 데이터 형식의 최소 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**source_scale_max**|**int**|원본 DBMS에서 해당 데이터 형식의 최대 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**source_nullable**|**bit**|대상 데이터 형식이 Null 값을 허용하는지 여부를 나타냅니다.|  
|**source_createparams**|**int**|내부적으로만 사용됩니다.|  
|**destination_dbms**|**sysname**|대상 DBMS의 이름을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **MSSQLSERVER** = 대상이 SQL Server 데이터베이스입니다.<br /><br /> **Oracle** = 대상이 ORACLE 데이터베이스입니다.<br /><br /> **DB2** = 대상이 IBM DB2 데이터베이스입니다.<br /><br /> **Sybase** = 대상이 SYBASE 데이터베이스입니다.|  
|**destination_version**|**sysname**|대상 DBMS의 제품 버전입니다.|  
|**destination_type**|**sysname**|대상 DBMS의 데이터 형식입니다.|  
|**destination_length**|**bigint**|대상 DBMS에 있는 데이터 형식의 길이입니다.|  
|**destination_precision**|**bigint**|대상 DBMS에 있는 데이터 형식의 전체 자릿수입니다.|  
|**destination_scale**|**int**|대상 DBMS에 있는 데이터 형식의 소수 자릿수입니다.|  
|**destination_nullable**|**bit**|대상 DBMS에 있는 데이터 형식이 Null 값을 허용하는지 여부를 나타냅니다.|  
|**destination_createparams**|**int**|내부적으로만 사용됩니다.|  
|**데이터 손실을**|**bit**|원본 및 대상 DBMS 간에 데이터 형식을 매핑할 때 데이터 손실이 발생하는지 여부를 나타냅니다.|  
|**is_default**|**bit**|이 데이터 형식 매핑이 기본값으로 사용되는지 여부를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_helpdatatypemap &#40;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
