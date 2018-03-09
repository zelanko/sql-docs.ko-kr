---
title: sp_mergedummyupdate (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords: sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46c1fb620db4c4bbe4dde9872897cad07553173a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spmergedummyupdate-transact-sql"></a>sp_mergedummyupdate(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 행에 더미 업데이트를 수행하여 다음 병합 중에 다시 전송되도록 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 구독 데이터베이스의 구독자에서 실행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>인수  
 [  **@source_object=**] **'***source_object***'**  
 원본 개체의 이름입니다. *source_object*은 **nvarchar (386)**, 기본값은 없습니다.  
  
 [  **@rowguid=**] **'***rowguid***'**  
 행 식별자입니다. *rowguid* 은 **uniqueidentifier**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_mergedummyupdate** 병합 복제에 사용 됩니다.  
  
 **sp_mergedummyupdate** 복제 충돌 뷰어 (Wzcnflct.exe)에 자신의 대체를 작성 하는 경우 유용 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_mergedummyupdate**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
