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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74cc0fbbe0d3eeae2637ca7c91ba28e531abbf22
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711771"
---
# <a name="-scope-resolution-transact-sql"></a>:: (범위 결정) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  범위 결정 연산자 **::** 은 복합 데이터 형식의 정적 멤버에 대한 액세스를 제공합니다. 복합 데이터 형식은 기본 제공 CLR 형식 및 사용자 지정 SQLCLR UDT(User-Defined Types) 등과 같은 여러 단순 데이터 형식과 메서드를 포함하는 형식입니다.  
  
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
  
  
