---
title: "범위 해결 연산자 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f03f0c8274d52f61e5db2d75fe21e3fe90a4ce26
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="scope-resolution-operator-transact-sql"></a>범위 결정 연산자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  범위 결정 연산자 **::** 복합 데이터 형식의 정적 멤버에 대 한 액세스를 제공 합니다. 복합 데이터 형식은 여러 단순 데이터 형식 및 메서드를 포함합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 범위 결정 연산자를 사용하여 `GetRoot()` 형식의 `hierarchyid` 멤버에 액세스하는 방법을 보여 줍니다.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>관련 항목:  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

