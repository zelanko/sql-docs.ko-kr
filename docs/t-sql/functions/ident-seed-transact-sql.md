---
title: IDENT_SEED(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENT_SEED_TSQL
- IDENT_SEED
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], IDENT_SEED function
- seed values [SQL Server]
- IDENT_SEED function
ms.assetid: e4cb8eb8-affb-4810-a8a9-0110af3c247a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c5c5e2ca321deb2b7e82774db1e91c0b0149deb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024375"
---
# <a name="identseed-transact-sql"></a>IDENT_SEED(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  테이블이나 뷰에 ID 열을 만들 때 지정된 원래 초기값(**numeric**( **@@** MAXPRECISION,0)으로 반환됨)을 반환합니다. DBCC CHECKIDENT를 사용하여 현재 ID 열 값을 변경해도 이 함수에서 반환되는 값은 변경되지 않습니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IDENT_SEED ( 'table_or_view' )  
```  
  
## <a name="arguments"></a>인수  
 **'** *table_or_view* **'**  
 ID 초기값을 확인할 테이블 또는 뷰를 지정하는 [expression](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *table_or_view*는 따옴표로 묶은 문자열 상수, 변수, 함수 또는 열 이름일 수 있습니다. *table_or_view*는 **char**, **nchar**, **varchar** 또는 **nvarchar**입니다.  
  
## <a name="return-types"></a>반환 형식  
 **numeric**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자에게 개체를 볼 수 있는 권한이 없으면 NULL을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하거나 권한이 부여된 보안 개체의 메타데이터만 볼 수 있습니다. 이 보안은 사용자가 개체에 대한 사용 권한이 없으면 IDENT_SEED와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환할 수 있음을 의미합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-seed-value-from-a-specified-table"></a>1\. 지정된 테이블에서 초기값 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Person.Address` 테이블에 대한 초기값을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENT_SEED('Person.Address') AS Identity_Seed;  
GO  
```  
  
### <a name="b-returning-the-seed-value-from-multiple-tables"></a>2\. 여러 테이블에서 초기값 반환  
 다음 예제에서는 초기값이 있는 ID 열을 포함하는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 테이블을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_SCHEMA, TABLE_NAME,   
   IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) AS IDENT_SEED  
FROM INFORMATION_SCHEMA.TABLES  
WHERE IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) IS NOT NULL;  
GO  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
 TABLE_SCHEMA       TABLE_NAME                   IDENT_SEED  
------------       ---------------------------  -----------  
Person             Address                                1  
Production         ProductReview                          1  
Production         TransactionHistory                100000  
Person             AddressType                            1  
Production         ProductSubcategory                     1  
Person             vAdditionalContactInfo                 1  
dbo                AWBuildVersion                         1
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [IDENT_CURRENT&#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENT_INCR&#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
