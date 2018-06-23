---
title: MERGE 기능 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: e2d4c6255b7b6a91fad1d99c2676bf76fae68385
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090854"
---
# <a name="implementing-merge-functionality"></a>MERGE 기능 구현
  데이터베이스에 특정 행 이 이미 있는지 여부에 따라 데이터베이스에서 삽입 또는 업데이트를 수행해야 할 수 있습니다.  
  
 사용 하지 않고는 `MERGE` 문, 다음은 사용할 수 있습니다는 한 가지 방법은 [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
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
  
  