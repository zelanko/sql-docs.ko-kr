---
title: 개체 계층 구조 구문 (TRANSACT-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3405621d604e6450756520f6d93b66a51d4d66c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941982"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>개체 계층 구조 구문(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  합니다 *propertyname* sp_OAGetProperty와 sp_OASetProperty의 매개 변수 및 *methodname* sp_OAMethod의 매개 변수는 개체 계층 구조 구문과 비슷한 구문을의 지원 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. 이 특수 구문을 사용할 때 이러한 매개 변수는 다음과 같은 일반적인 형식을 갖습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>인수  
 *TraversedObject*  
 계층 구조의 OLE 개체를 *objecttoken* 저장된 프로시저에 지정 합니다. 개체를 반환하는 일련의 컬렉션, 개체 속성, 메서드를 지정하려면 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 구문을 사용합니다. 각 개체 지정자는 마침표(.)로 구분해야 합니다.  
  
 각 항목은 컬렉션 이름일 수 있습니다. 컬렉션을 지정하려면  
  
 컬렉션 ("*항목*")  
  
 큰따옴표(")가 필요합니다. 컬렉션에 대한 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]의 느낌표(!) 구문은 지원되지 않습니다.  
  
 *PropertyOrMethod*  
 속성의 이름 또는 메서드를 *TraversedObject*합니다.  
  
 sp_OAGetProperty, sp_OASetProperty 또는 sp_OAMethod 매개 변수(sp_OAMethod 출력 매개 변수에 대한 지원 포함)를 사용하여 모든 인덱스 또는 메서드 매개 변수를 지정하려면 다음 구문을 사용하십시오.  
  
 *PropertyOrMethod*  
  
 sp_OAGetProperty, sp_OASetProperty 또는 sp_OAMethod의 모든 인덱스 및 메서드 매개 변수를 무시하기 위해 괄호 안에 모든 인덱스 및 메서드 매개 변수를 지정하려면 다음 구문을 사용합니다.  
  
 *PropertyOrMethod*([ *ParameterName*: =] "*매개 변수*" [,...])  
  
 큰따옴표(")가 필요합니다. 모든 명명된 매개 변수는 반드시 모든 위치 매개 변수가 지정된 후에 지정되어야 합니다.  
  
## <a name="remarks"></a>설명  
 하는 경우 *TraversedObject* 지정 하지 않으면 *PropertyOrMethod* 필요 합니다.  
  
 하는 경우 *PropertyOrMethod* 지정 하지 않으면 합니다 *TraversedObject* OLE Automation 저장 프로시저에서 개체 토큰 출력 매개 변수로 반환 됩니다. 경우 *PropertyOrMethod* 지정 된 속성 또는 메서드의 *TraversedObject* 호출 되 고 속성 값 또는 메서드 반환 값은 OLE Automation에서 출력 매개 변수로 반환 됩니다 저장된 프로시저입니다.  
  
 항목이 있으면 합니다 *TraversedObject* 목록 OLE 개체를 반환 하지 않는, 오류가 발생 합니다.  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE 개체 구문에 대한 자세한 내용은 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 설명서를 참조하십시오.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 참조 하세요. [sp_OACreate &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)합니다.  
  
## <a name="examples"></a>예  
 다음은 SQL-DMO SQLServer 개체를 사용 하는 개체 계층 구문의 예입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE 자동화 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
