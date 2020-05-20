---
title: sp_droptype (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8bc4462e05c97975d643f6900574f39000bc4eca
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827809"
---
# <a name="sp_droptype-transact-sql"></a>sp_droptype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **Systypes**에서 별칭 데이터 형식을 삭제 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>인수  
`[ @typename = ] 'type'`소유 하 고 있는 별칭 데이터 형식의 이름입니다. *형식은* **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-type"></a>반환 코드 유형  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 테이블 또는 다른 데이터베이스 개체가 참조 하는 경우에는 **형식** 별칭 데이터 형식을 삭제할 수 없습니다.  
  
> [!NOTE]  
>  별칭 데이터 형식이 테이블 정의에서 사용되거나 별칭 데이터 형식에 규칙 또는 기본값이 바인딩되어 있는 경우 해당 별칭 데이터 형식을 삭제할 수 없습니다.  
  
## <a name="permissions"></a>권한  
 **Db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addtype &#40;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
