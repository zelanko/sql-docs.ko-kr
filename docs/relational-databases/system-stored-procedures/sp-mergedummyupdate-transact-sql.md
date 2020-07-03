---
title: sp_mergedummyupdate (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5502b64da269639d99fe54d4930f7f3b7b145d73
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899362"
---
# <a name="sp_mergedummyupdate-transact-sql"></a>sp_mergedummyupdate(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정된 행에 더미 업데이트를 수행하여 다음 병합 중에 다시 전송되도록 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 구독 데이터베이스의 구독자에서 실행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>인수  
`[ @source_object = ] 'source_object'`원본 개체의 이름입니다. *source_object*은 **nvarchar (386)** 이며 기본값은 없습니다.  
  
`[ @rowguid = ] 'rowguid'`행 식별자입니다. *rowguid* 는 **uniqueidentifier**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_mergedummyupdate** 는 병합 복제에 사용 됩니다.  
  
 **sp_mergedummyupdate** 은 복제 충돌 뷰어 (Wzcnflct.exe)에 대 한 대안을 직접 작성 하는 경우에 유용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버만 **sp_mergedummyupdate**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
