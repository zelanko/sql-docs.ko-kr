---
title: SET IDENTITY_INSERT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9725d774075f21fc86d5276c91ed281fa34eba7d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-identityinsert-transact-sql"></a>SET IDENTITY_INSERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  명시적 값을 테이블의 ID 열에 삽입할 수 있도록 합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET IDENTITY_INSERT [ database_name . [ schema_name ] . ] table { ON | OFF }  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 지정한 테이블이 있는 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table*  
 ID 열이 있는 테이블의 이름입니다.  
  
## <a name="remarks"></a>주의  
 언제든지 세션에서 한 테이블의 IDENTITY_INSERT 속성만 ON으로 설정할 수 있습니다. 한 테이블에 이 속성이 ON으로 설정되어 있는데 다른 테이블에 대해 SET IDENTITY_INSERT ON 문을 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SET IDENTITY_INSERT가 이미 ON으로 설정되어 있음을 알리고 ON으로 설정된 테이블을 보고하는 오류 메시지를 반환합니다.  
  
 테이블의 현재 ID 값보다 큰 값을 삽입하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 새로 삽입한 값을 현재 ID 값으로 사용합니다.  
  
 SET IDENTITY_INSERT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 사용자는 테이블을 소유하거나 테이블에 대한 ALTER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ID 열이 있는 테이블을 만든 다음 `SET IDENTITY_INSERT` 설정을 사용하여 `DELETE` 문으로 인해 생긴 ID 값의 차이를 채우는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return a warning.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY &#40; Transact SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

