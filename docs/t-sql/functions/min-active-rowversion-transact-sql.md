---
title: MIN_ACTIVE_ROWVERSION (Transact SQL) | Microsoft Docs
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
- MIN_ACTIVE_ROWVERSION
- MIN_ACTIVE_ROWVERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN_ACTIVE_ROWVERSION function [Transact-SQL]
ms.assetid: 87c89547-8ea1-4820-b75e-36be683e4e10
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed1254e0e35aa108d9866f30da49962b886a39ae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="minactiverowversion-transact-sql"></a>MIN_ACTIVE_ROWVERSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 비활성 **rowversion** 값을 반환합니다. **rowversion** 값이 아직 커밋되지 않은 트랜잭션에서 사용되는 경우에는 활성 상태입니다. 자세한 내용은 참조 [rowversion &#40; Transact SQL &#41; ](../../t-sql/data-types/rowversion-transact-sql.md).  
  
> [!NOTE]  
>  **rowversion** 데이터 형식이 라고도 **타임 스탬프**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
MIN_ACTIVE_ROWVERSION  
```  
  
## <a name="return-types"></a>반환 형식  
 반환 된 **binary (8)** 값입니다.  
  
## <a name="remarks"></a>주의  
 MIN_ACTIVE_ROWVERSION은 비활성 반환 하는 비 결정적인 함수 **rowversion** 현재 데이터베이스에 있는 값입니다. 새로운 **rowversion** 값은 일반적으로 **rowversion**형식의 열이 포함된 테이블에 삽입 또는 업데이트가 수행될 때 생성됩니다. 데이터베이스의 현재 값이 없는 경우 MIN_ACTIVE_ROWVERSION @와 같은 값을 반환@DBTS + 1입니다.  
  
 MIN_ACTIVE_ROWVERSION은 사용 하는 데이터 동기화와 같은 시나리오에 유용 **rowversion** 함께 변경 내용 그룹 집합에는 값입니다. 응용 프로그램에서 사용 하는 경우@DBTS MIN_ACTIVE_ROWVERSION, 대신 동기화가 일어날 때 활성 상태인 누락 변경 내용을 수는 있습니다.  
  
 MIN_ACTIVE_ROWVERSION 함수는 트랜잭션 격리 수준에 있는 변경 내용의 영향을 받지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 반환 **rowversion** 사용 하 여 값 `MIN_ACTIVE_ROWVERSION` 및 `@@DBTS`합니다. 데이터베이스에 활성 트랜잭션이 없으면 값이 달라집니다.  
  
```  
-- Create a table that has a ROWVERSION column in it.  
CREATE TABLE RowVersionTestTable (rv ROWVERSION)  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E2  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E3  
  
-- Insert a row.  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E3  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Insert a new row inside a transaction but do not commit.  
BEGIN TRAN  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
--0x00000000000007E4  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Commit the transaction.  
COMMIT  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E5  
```  
  
## <a name="see-also"></a>관련 항목:  
 [@@DBTS&#40;Transact-SQL&#41;](../../t-sql/functions/dbts-transact-sql.md)   
 [rowversion&#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)  
  
  

