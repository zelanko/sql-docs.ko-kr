---
title: sp_OAStop (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAStop
- sp_OAStop_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAStop
ms.assetid: aa9eab66-c4f7-4ec7-9f0d-5d24d16da654
author: stevestein
ms.author: sstein
ms.openlocfilehash: ead1a768a89e9b43c02d7e80619dbf52165d2a38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097608"
---
# <a name="sp_oastop-transact-sql"></a>sp_OAStop(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 차원의 OLE Automation 저장 프로시저 실행 환경을 중지합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_OAStop      
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 숫자(실패)이며 OLE Automation 개체가 반환한 HRESULT의 정수 값입니다.  
  
 HRESULT 반환 코드에 대 한 자세한 내용은 [OLE 자동화 반환 코드 및 오류 정보](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)를 참조 하세요.  
  
## <a name="remarks"></a>설명  
 OLE Automation 저장 프로시저를 사용하는 모든 클라이언트는 하나의 실행 환경을 공유합니다. 한 클라이언트가 **sp_OAStop** 를 호출 하는 경우 모든 클라이언트에 대해 공유 실행 환경이 중지 됩니다. 실행 환경이 중지 된 후 **sp_OACreate** 호출은 실행 환경을 다시 시작 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 자격 또는이 저장 프로시저에 대 한 execute 권한이 필요 합니다. `Ole Automation Procedures`OLE 자동화와 관련 된 시스템 프로시저를 사용 하려면 구성을 사용 하도록 **설정** 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 공유 OLE Automation 실행 환경을 중지합니다.  
  
```  
EXEC sp_OAStop;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;OLE 자동화 저장 프로시저](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 자동화 예제 스크립트](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
