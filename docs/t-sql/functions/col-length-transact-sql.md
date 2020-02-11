---
title: COL_LENGTH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bf23672374db7d8348154e95ca6228723934aa5a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68064721"
---
# <a name="col_length-transact-sql"></a>COL_LENGTH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 정의된 열의 길이(바이트)를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>인수  
**'** *table* **'**  
열 길이 정보를 확인하려는 테이블의 이름입니다. *table*은 **nvarchar** 형식의 식입니다.
  
**'** *column* **'**  
확인하려는 길이의 열 이름입니다. *column*은 **nvarchar** 형식의 식입니다.
  
## <a name="return-type"></a>반환 형식
**smallint**
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자에게 개체를 볼 수 있는 올바른 권한이 없으면 NULL을 반환합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자에게 개체에 대한 올바른 권한이 없으면 COL_LENGTH와 같은 메타데이터 내보내기 기본 제공 함수에서 NULL을 반환할 수 있습니다. 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>설명  
**max** 지정자(**varchar(max)** )를 사용하여 선언된 **varchar** 열의 경우 COL_LENGTH는 -1 값을 반환합니다.
  
## <a name="examples"></a>예  
다음 예제에서는 `varchar(40)` 형식 및 `nvarchar(40)` 형식의 열에 대한 반환 값을 보여 줍니다.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>참고 항목
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
