---
title: DROP TYPE (Transact-SQL)| Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 84df28edf6187a53e54edd3f3fcc2283bcaa3e7a
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635129"
---
# <a name="drop-type-transact-sql"></a>DROP TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 별칭 데이터 형식 또는 CLR(공용 언어 런타임) 사용자 정의 형식을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 형식을 조건부로 삭제합니다.  
  
 *schema_name*  
 별칭 또는 사용자 정의 형식이 속한 스키마의 이름입니다.  
  
 *type_name*  
 삭제하려는 별칭 데이터 형식 또는 사용자 정의 형식의 이름입니다.  
  
## <a name="remarks"></a>설명  
 다음 사항 중 하나라도 해당하는 경우 DROP TYPE 문은 실행되지 않습니다.  
  
-   데이터베이스에 별칭 데이터 형식 또는 사용자 정의 형식의 열을 포함하는 테이블이 있는 경우. 별칭 또는 사용자 정의 형식 열에 관한 정보는 [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 또는 [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md) 카탈로그 뷰를 쿼리하여 얻을 수 있습니다.  
  
-   정의에서 별칭이나 사용자 정의 형식을 참조하는 계산 열, CHECK 제약 조건, 스키마 바운드 뷰 및 스키마 바운드 함수가 있는 경우. 이러한 참조에 대한 정보는 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 카탈로그 뷰를 쿼리하여 얻을 수 있습니다.  
  
-   데이터베이스에 함수, 저장 프로시저 또는 생성된 트리거가 있고 이러한 루틴에서 별칭 또는 사용자 정의 형식의 변수 및 매개 변수를 사용하는 경우. 별칭 또는 사용자 정의 형식 매개 변수에 관한 정보는 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) 또는 [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md) 카탈로그 뷰를 쿼리하여 얻을 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 *type_name*에 관한 CONTROL 권한 또는 *schema_name*에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ssn` 형식이 이미 현재 데이터베이스에서 생성된 것으로 가정합니다.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
