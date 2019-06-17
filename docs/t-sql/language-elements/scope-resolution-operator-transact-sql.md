---
title: ':: (범위 결정)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d721d6f39b33b553d0a00c55ddbc58df006029a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981829"
---
# <a name="-scope-resolution-transact-sql"></a>:: (범위 결정)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  범위 결정 연산자 **::** 은 복합 데이터 형식의 정적 멤버에 대한 액세스를 제공합니다. 복합 데이터 형식은 여러 단순 데이터 형식 및 메서드를 포함합니다. 복합 데이터 형식에는 기본 제공 CLR 형식 및 사용자 지정 SQLCLR UDT(사용자 정의 형식)가 포함됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 범위 결정 연산자를 사용하여 `GetRoot()` 형식의 `hierarchyid` 멤버에 액세스하는 방법을 보여 줍니다.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
 