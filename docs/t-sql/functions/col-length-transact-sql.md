---
title: COL_LENGTH (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e0debbe52f8e0bbff8e8f7cc0d6509e1e9436b5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="collength-transact-sql"></a>COL_LENGTH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

열의 정의된 길이(바이트)를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>인수  
**'** *테이블* **'**  
열 길이 정보를 확인할 테이블의 이름입니다. *테이블* 형식의 식 **nvarchar**합니다.
  
**'** *열* **'**  
길이를 확인할 열의 이름입니다. *열* 형식의 식 **nvarchar**합니다.
  
## <a name="return-type"></a>반환 형식
**smallint**
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 사용 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 COL_LENGTH와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>주의  
형식의 열에 대 한 **varchar** 사용 하 여 선언 된 **max** 지정자 (**varchar (max)**), COL_LENGTH가 값-1을 반환 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 `varchar(40)` 형식의 열과 `nvarchar(40)` 형식의 열에 대한 반환 값을 보여 줍니다.
  
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
[메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40; Transact SQL &#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  

