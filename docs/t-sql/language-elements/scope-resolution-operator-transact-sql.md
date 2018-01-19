---
title: ":: (범위 결정) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79ebca248982e3fb6543991ba6fdc6c0837ae4c8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="-scope-resolution-transact-sql"></a>:: (범위 결정) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  범위 결정 연산자 **::** 복합 데이터 형식의 정적 멤버에 대 한 액세스를 제공 합니다. 복합 데이터 형식은 여러 단순 데이터 유형 및 기본 제공 CLR 형식 및 사용자 지정 SQLCLR User-Defined 형식 (Udt)와 같은 메서드를 포함 합니다.  
  
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
  
  
