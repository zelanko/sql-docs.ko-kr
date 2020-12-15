---
description: sp_helptrigger(Transact-SQL)
title: sp_helptrigger (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b03afedd01095ddfc233eca9722e9eecde8f840
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468364"
---
# <a name="sp_helptrigger-transact-sql"></a>sp_helptrigger(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스의 지정된 테이블에 정의된 DML 트리거의 유형을 반환합니다. sp_helptrigger은 DDL 트리거와 함께 사용할 수 없습니다. 대신 [시스템 저장 프로시저](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 카탈로그 뷰를 쿼리 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tabname = ] 'table'` 트리거 정보를 반환할 현재 데이터베이스의 테이블 이름입니다. *테이블* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @triggertype = ] 'type'` 정보를 반환할 DML 트리거의 유형입니다. *type* 은 **char (6)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**DELETE**|DELETE 트리거 정보를 반환합니다.|  
|**INSERT**|INSERT 트리거 정보를 반환합니다.|  
|**UPDATE**|UPDATE 트리거 정보를 반환합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 결과 집합에 포함된 정보를 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|트리거의 이름입니다.|  
|**trigger_owner**|**sysname**|트리거가 정의된 테이블의 소유자 이름입니다.|  
|**isupdate**|**int**|1=UPDATE 트리거입니다.<br /><br /> 0=UPDATE 트리거가 아닙니다.|  
|**isdelete**|**int**|1=DELETE 트리거입니다.<br /><br /> 0=DELETE 트리거가 아닙니다.|  
|**isinsert**|**int**|1=INSERT 트리거입니다.<br /><br /> 0=INSERT 트리거가 아닙니다.|  
|**isafter**|**int**|1=AFTER 트리거입니다.<br /><br /> 0=AFTER 트리거가 아닙니다.|  
|**isinsteadof**|**int**|1=INSTEAD OF 트리거입니다.<br /><br /> 0=INSTEAD OF 트리거가 아닙니다.|  
|**trigger_schema**|**sysname**|트리거가 속한 스키마의 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 테이블에 대 한 [메타 데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md) 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_helptrigger`를 실행하여 `Person.Person` 테이블의 트리거에 대한 정보를 출력합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
