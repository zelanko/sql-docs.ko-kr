---
title: sp_OADestroy (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 98907614a132cfafd297e48f0ef625bc8eb4155d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107902"
---
# <a name="spoadestroy-transact-sql"></a>sp_OADestroy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  생성된 OLE 개체를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>인수  
 *objecttoken*  
 사용 하 여 이전에 만든 OLE 개체의 개체 토큰 **sp_OACreate**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 참조 하세요. [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)합니다.  
  
## <a name="remarks"></a>설명  
 하는 경우 **sp_OADestroy** 를 호출 하지 않으면 만들어진 OLE 개체 일괄 처리의 끝에 자동으로 제거 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 서버 역할 또는 권한이이 저장 프로시저에서 직접 실행 합니다. `Ole Automation Procedures` 구성이 있어야 **활성화** OLE Automation과 관련 된 모든 시스템 프로시저를 사용 하도록 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 이전에 만든 소멸 **SQLServer** 개체입니다.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>관련 항목  
 [OLE Automation 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
