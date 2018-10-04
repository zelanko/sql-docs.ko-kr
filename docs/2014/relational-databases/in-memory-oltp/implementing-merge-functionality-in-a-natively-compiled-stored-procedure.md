---
title: MERGE 기능 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9614ee30c6e0566dc270f07e20b0c4dc29d1feb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063943"
---
# <a name="implementing-merge-functionality"></a>MERGE 기능 구현
  데이터베이스에 특정 행 이 이미 있는지 여부에 따라 데이터베이스에서 삽입 또는 업데이트를 수행해야 할 수 있습니다.  
  
 사용 하지 않고 합니다 `MERGE` 문, 다음은 사용할 수 있습니다 하는 한 가지 방법은 [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```tsql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 병합을 구현하는 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 방법:  
  
```tsql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE….  
ELSE  
    INSERT  
```  
  
 고유하게 컴파일된 저장 프로시저의 경우  
  
```tsql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT….  
```  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
