---
title: DROP AGGREGATE (TRANSACT-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a9fcab3dc576f15110bed8c1c82271731f326280
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 사용자 정의 집계 함수를 제거합니다. 사용자 정의 집계 함수를 사용 하 여 만들어진 [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 집계를 삭제 합니다.  
  
 *schema_name*  
 사용자 정의 집계 함수가 속한 스키마의 이름입니다.  
  
 *aggregate_name*  
 삭제할 사용자 정의 집계 함수의 이름입니다.  
  
## <a name="remarks"></a>주의  
 DROP AGGREGATE는 삭제할 사용자 정의 집계 함수를 참조하는 스키마 바인딩으로 생성된 뷰, 함수 또는 저장 프로시저가 있는 경우에는 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 DROP AGGREGATE를 실행하려면 최소한 사용자 정의 집계가 속한 스키마에 대한 ALTER 권한이나 집계에 대한 CONTROL 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 집계 `Concatenate`를 삭제합니다.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [집계 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [사용자 정의 집계 만들기](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  

