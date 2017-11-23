---
title: "삭제 유형을 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f19e21b60429d04e4af8c615db79302519e5a507
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-type-transact-sql"></a>DROP TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 별칭 데이터 형식 또는 CLR(공용 언어 런타임) 사용자 정의 형식을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 형식을 삭제 합니다.  
  
 *schema_name*  
 별칭 또는 사용자 정의 형식이 속한 스키마의 이름입니다.  
  
 *type_name*  
 삭제하려는 별칭 데이터 형식 또는 사용자 정의 형식의 이름입니다.  
  
## <a name="remarks"></a>주의  
 다음 사항 중 하나라도 해당하는 경우 DROP TYPE 문은 실행되지 않습니다.  
  
-   데이터베이스에 별칭 데이터 형식 또는 사용자 정의 형식의 열을 포함하는 테이블이 있는 경우. 쿼리하여 별칭 또는 사용자 정의 형식 열에 대 한 정보를 가져올 수 있습니다는 [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 또는 [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md) 카탈로그 뷰.  
  
-   정의에서 별칭이나 사용자 정의 형식을 참조하는 계산 열, CHECK 제약 조건, 스키마 바운드 뷰 및 스키마 바운드 함수가 있는 경우. 쿼리하여 이러한 참조에 대 한 정보를 가져올 수 있습니다는 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
-   데이터베이스에 함수, 저장 프로시저 또는 생성된 트리거가 있고 이러한 루틴에서 별칭 또는 사용자 정의 형식의 변수 및 매개 변수를 사용하는 경우. 별칭 또는 사용자 정의 형식 매개 변수에 대 한 정보를 쿼리하여 얻을 수 있습니다는 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) 또는 [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md) 카탈로그 뷰.  
  
## <a name="permissions"></a>Permissions  
 에 대 한 CONTROL 권한 중 하나가 필요 *type_name* 에 대 한 ALTER 권한 또는 *schema_name*합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ssn` 형식이 이미 현재 데이터베이스에서 생성된 것으로 가정합니다.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
