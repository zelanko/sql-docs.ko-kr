---
description: sp_dropextendedproc(Transact-SQL)
title: sp_dropextendedproc (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02d4287b2825401acd0eca532b3fad100fa32639
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538973"
---
# <a name="sp_dropextendedproc-transact-sql"></a>sp_dropextendedproc(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  확장 저장 프로시저를 삭제합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>인수  
`[ @functname = ] 'procedure'` 삭제할 확장 저장 프로시저의 이름입니다. *프로시저* 는 **nvarchar (517)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **Sp_dropextendedproc** 를 실행 하면 사용자 정의 확장 저장 프로시저 이름이 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에서 삭제 되 고 [extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 카탈로그 뷰에서 항목이 제거 됩니다. 이 저장 프로시저는 **master** 데이터베이스 에서만 실행할 수 있습니다.  
  
**sp_dropextendedproc** 는 시스템 확장 저장 프로시저를 삭제 하지 않습니다. 대신 시스템 관리자는 **공용** 역할에 대 한 확장 저장 프로시저에 대 한 EXECUTE 권한을 거부 해야 합니다.  
  
 **sp_dropextendedproc** 은 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dropextendedproc**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `xp_hello` 확장 저장 프로시저를 삭제합니다.  
  
> [!NOTE]  
>  이 확장 저장 프로시저가 이미 존재해야 하며 그렇지 않으면 예에서 오류 메시지를 반환합니다.  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [Transact-sql&#41;sp_helpextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
