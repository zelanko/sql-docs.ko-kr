---
description: 개체 계층 구조 구문(Transact-SQL)
title: 개체 계층 구조 구문 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81db44bae57dec8bb0298e872221998ac45e0a3a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542077"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>개체 계층 구조 구문(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sp_OAGetProperty 및 sp_OASetProperty의 *propertyname* 매개 변수와 sp_OAMethod의 *methodname* 매개 변수는와 유사한 개체 계층 구조 구문을 지원 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . 이 특수 구문을 사용할 때 이러한 매개 변수는 다음과 같은 일반적인 형식을 갖습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>인수  
 *TraversedObject*  
 저장 프로시저에 지정 된 *objecttoken* 아래의 계층 구조에 있는 OLE 개체입니다. 개체를 반환하는 일련의 컬렉션, 개체 속성, 메서드를 지정하려면 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 구문을 사용합니다. 각 개체 지정자는 마침표(.)로 구분해야 합니다.  
  
 각 항목은 컬렉션 이름일 수 있습니다. 컬렉션을 지정하려면  
  
 Collection ("*item*")  
  
 큰따옴표(")가 필요합니다. 컬렉션에 대한 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 느낌표(!) 구문은 지원되지 않습니다.  
  
 *PropertyOrMethod*  
 *TraversedObject*의 속성 또는 메서드 이름입니다.  
  
 sp_OAGetProperty, sp_OASetProperty 또는 sp_OAMethod 매개 변수(sp_OAMethod 출력 매개 변수에 대한 지원 포함)를 사용하여 모든 인덱스 또는 메서드 매개 변수를 지정하려면 다음 구문을 사용하십시오.  
  
 *PropertyOrMethod*  
  
 sp_OAGetProperty, sp_OASetProperty 또는 sp_OAMethod의 모든 인덱스 및 메서드 매개 변수를 무시하기 위해 괄호 안에 모든 인덱스 및 메서드 매개 변수를 지정하려면 다음 구문을 사용합니다.  
  
 *Propertyormethod*([ *ParameterName*: =] "*parameter*" [, ...])  
  
 큰따옴표(")가 필요합니다. 모든 명명된 매개 변수는 반드시 모든 위치 매개 변수가 지정된 후에 지정되어야 합니다.  
  
## <a name="remarks"></a>설명  
 *TraversedObject* 을 지정 하지 않으면 *propertyormethod* 가 필요 합니다.  
  
 *Propertyormethod* 가 지정 되지 않은 경우 *TraversedObject* 는 OLE 자동화 저장 프로시저에서 개체 토큰 출력 매개 변수로 반환 됩니다. *Propertyormethod* 를 지정 하면 *TraversedObject* 의 속성 또는 메서드가 호출 되 고 속성 값 또는 메서드 반환 값이 OLE 자동화 저장 프로시저에서 출력 매개 변수로 반환 됩니다.  
  
 *TraversedObject* 목록의 항목이 OLE 개체를 반환 하지 않는 경우 오류가 발생 합니다.  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE 개체 구문에 대한 자세한 내용은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 설명서를 참조하십시오.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 [sp_OACreate &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)를 참조 하세요.  
  
## <a name="examples"></a>예제  
 다음은 SQL-DMO SQLServer 개체를 사용하는 개체 계층 구문의 예입니다.  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>참고 항목  
 [OLE 자동화 샘플 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE 자동화 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
