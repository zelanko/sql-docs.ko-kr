---
title: core.sp_add_collector_type (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_collector_type
- sp_add_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_add_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_add_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 1d981037-2147-464e-a456-7d8e479bce89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7bc16db334b6b8f6538a7ee221beb5fd3ccf2a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727601"
---
# <a name="corespaddcollectortype-transact-sql"></a>core.sp_add_collector_type(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  관리 데이터 웨어하우스 데이터베이스의 core.supported_collector_types 뷰에 새 항목을 추가합니다. 이 프로시저는 관리 데이터 웨어하우스 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
core.sp_add_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>인수  
 [ @collector_type_uid =] '*collector_type_uid*'  
 수집기 유형의 GUID입니다. *collector_type_uid* 됩니다 **uniqueidentifier**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **mdw_admin** (사용 하 여 EXECUTE 권한 있음) 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
 다음 예에서는 core.supported_collector_types 뷰에 일반 T-SQL 쿼리 수집기 유형을 추가합니다. 기본적으로 일반 T-SQL 쿼리 수집기 형식은 이미 있으므로 기본 설치에서 이 코드를 실행하면 수집기 형식이 이미 있다는 메시지가 나타납니다.  
  
 일반 T-SQL 쿼리 수집기 유형을 core.sp_remove_collector_type 저장 프로시저를 사용하여 제거한 다음 관리 데이터 웨어하우스에 데이터를 업로드할 수 있는 등록된 수집기 유형으로 다시 추가하려는 경우 이 코드가 성공적으로 실행됩니다.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_add_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [관리 데이터 웨어하우스](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
