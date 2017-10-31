---
title: OBJECT_DEFINITION (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcb2ac9e5dd80c804996d08b084b4b0068c4b618
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="objectdefinition-transact-sql"></a>OBJECT_DEFINITION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 개체의 정의에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 원본 텍스트를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>인수  
 *object_id*  
 사용할 개체의 ID입니다. *object_id* 은 **int**, 및 현재 데이터베이스 컨텍스트에 개체가 있다고 가정 합니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECT_DEFINITION과 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 있다고 가정 *object_id* 은 현재 데이터베이스 컨텍스트에서 실행 됩니다. 개체 정의의 데이터 정렬은 항상 호출하는 데이터베이스 컨텍스트의 데이터 정렬과 일치합니다.  
  
 OBJECT_DEFINITION은 다음 개체 유형에 적용됩니다.  
  
-   C = CHECK 제약 조건  
  
-   D = DEFAULT(제약 조건 또는 독립 실행형)  
  
-   P = SQL 저장 프로시저  
  
-   FN = SQL 스칼라 함수  
  
-   R = 규칙  
  
-   RF = 복제 필터 프로시저  
  
-   TR = SQL 트리거(스키마 범위 DML 트리거 또는 데이터베이스나 서버 범위 DDL 트리거)  
  
-   IF = SQL 인라인 테이블 반환 함수  
  
-   TF = SQL 테이블 반환 함수  
  
-   V = 뷰  
  
## <a name="permissions"></a>Permissions  
 시스템 개체 정의는 공개적으로 표시됩니다. 개체 소유자나 ALTER, CONTROL, TAKE OWNERSHIP 또는 VIEW DEFINITION 권한 중 하나를 부여받은 사람은 사용자 개체의 정의를 볼 수 있습니다. 이 권한은 **db_owner**, **db_ddladmin**및 **db_securityadmin** 고정 데이터베이스 역할의 멤버가 암시적으로 보유합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>1. 사용자 정의 개체의 원본 텍스트 반환  
 다음 예에서는 `uAddress` 스키마의 사용자 정의 트리거인 `Person`에 대한 정의를 반환합니다. 기본 제공 함수 `OBJECT_ID`는 트리거의 개체 ID를 `OBJECT_DEFINITION` 문에 반환하는 데 사용됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>2. 시스템 개체의 원본 텍스트 반환  
 다음 예에서는 시스템 저장 프로시저 `sys.sp_columns`의 정의를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40; Transact SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [Object_id&#40; Transact SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  

