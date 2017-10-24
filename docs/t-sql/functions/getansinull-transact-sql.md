---
title: GETANSINULL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GETANSINULL
- GETANSINULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], default
- GETANSINULL function
- default nullability
- database nullability [SQL Server]
ms.assetid: 189399e4-428d-4902-b3a8-94f07fdefc6a
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a103d3d4cc1c66bfcfe47decd4366b47d7831e8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="getansinull-transact-sql"></a>GETANSINULL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 세션에서 데이터베이스의 기본 Null 허용 여부를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GETANSINULL ( [ 'database' ] )  
```  
  
## <a name="arguments"></a>인수  
 '*데이터베이스*'  
 Null 허용 여부 정보를 반환할 데이터베이스의 이름입니다. *데이터베이스*있거나 **char** 또는 **nchar**합니다. 경우 **char**, *데이터베이스* 암시적으로 변환할 **nchar**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 지정된 데이터베이스의 Null 허용 여부가 Null 값 허용이고 열 또는 데이터 형식의 Null 허용 여부가 명시적으로 정의되어 있지 않으면 GETANSINULL은 1을 반환합니다. 이는 ANSI NULL 기본값입니다.  
  
 ANSI NULL 기본 동작을 활성화하려면 다음 조건 중 하나를 설정해야 합니다.  
  
-   ALTER DATABASE *database_name* ANSI_NULL_DEFAULT ON 설정  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET ANSI_NULL_DFLT_OFF OFF  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에 대한 기본 Null 허용 여부를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT GETANSINULL('AdventureWorks2012')  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

