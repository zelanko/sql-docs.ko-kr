---
title: sp_droptype (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droptype_TSQL
- sp_droptype
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droptype
ms.assetid: e78464ac-2370-4c4e-9cc0-06aebc07cec5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5004bbdefe29ec13142c66d333f346643261aeb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724008"
---
# <a name="spdroptype-transact-sql"></a>sp_droptype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  별칭 데이터 형식에서 삭제 **systypes**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>인수  
`[ @typename = ] 'type'` 소유 하 고 있는 별칭 데이터 형식의 이름이입니다. *형식* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-type"></a>반환 코드 유형  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 합니다 **형식** 별칭 데이터 형식을 삭제할 수 없습니다 테이블 또는 다른 데이터베이스 개체를 참조 합니다.  
  
> [!NOTE]  
>  별칭 데이터 형식이 테이블 정의에서 사용되거나 별칭 데이터 형식에 규칙 또는 기본값이 바인딩되어 있는 경우 해당 별칭 데이터 형식을 삭제할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할 또는 **db_ddladmin** 고정된 데이터베이스 역할.  
  
## <a name="examples"></a>예  
 다음 예에서는 별칭 데이터 형식 `birthday`를 삭제합니다.  
  
> [!NOTE]  
>  이 별칭 데이터 형식은 이미 존재해야 하며 그렇지 않은 경우 오류 메시지가 반환됩니다.  
  
```  
USE master;  
GO  
EXEC sp_droptype 'birthday';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addtype &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
