---
title: sp_OASetProperty (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OASetProperty
- sp_OASetProperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OASetProperty
ms.assetid: 0fe7d554-6b67-4d55-9d3e-4096802c47f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d2d3cc319a99c9e1b157e5b6bc06cabea2dd19a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65450076"
---
# <a name="spoasetproperty-transact-sql"></a>sp_OASetProperty(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE 개체의 속성을 새 값으로 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OASetProperty objecttoken , propertyname , newvalue [ , index... ]  
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 가 이전에 만든 OLE 개체의 개체 토큰 **sp_OACreate**합니다.  
  
 *propertyname*  
 새 값으로 설정할 OLE 개체의 속성 이름입니다.  
  
 *newvalue*  
 속성의 새 값이며 반드시 적절한 데이터 형식의 값이어야 합니다.  
  
 *index*  
 인덱스 매개 변수입니다. 를 지정 하는 경우 *인덱스* 적절 한 데이터 형식의 값 이어야 합니다.  
  
 일부 속성에는 매개 변수가 있습니다. 이러한 속성을 인덱싱된 속성이라 하고 매개 변수를 인덱스 매개 변수라고 합니다. 하나의 속성이 여러 개의 인덱스 매개 변수를 가질 수 있습니다.  
  
> [!NOTE]  
>  이 저장 프로시저의 매개 변수는 이름이 아니라 위치로 지정됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 참조 하세요. [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 서버 역할 또는 권한이이 저장 프로시저에서 직접 실행 합니다. `Ole Automation Procedures` 구성이 있어야 **활성화** OLE Automation과 관련 된 모든 시스템 프로시저를 사용 하도록 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 합니다 `HostName` 속성 (이전에 생성 **SQLServer** 개체)를 새 값입니다.  
  
```  
EXEC @hr = sp_OASetProperty @object, 'HostName', 'Gizmo';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END'  
```  
  
## <a name="see-also"></a>관련 항목  
 [OLE Automation 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
