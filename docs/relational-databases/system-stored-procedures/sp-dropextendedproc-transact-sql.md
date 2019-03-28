---
title: sp_dropextendedproc (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3690d4c954ae3cde5159100280597af14a796d3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529765"
---
# <a name="spdropextendedproc-transact-sql"></a>sp_dropextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  확장 저장 프로시저를 삭제합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>인수  
`[ @functname = ] 'procedure'` 삭제할 확장된 저장된 프로시저의 이름이입니다. *프로시저* 됩니다 **nvarchar(517)**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 실행 **sp_dropextendedproc** 에서 사용자 정의 확장된 저장된 프로시저 이름을 삭제 합니다 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에에서 항목을 제거 하 고는 [sys.extended_procedures ](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 카탈로그 뷰에 있습니다. 이 저장된 프로시저 에서만 실행할 수 있습니다 합니다 **마스터** 데이터베이스입니다.  
  
**sp_dropextendedproc** 시스템 확장 저장된 프로시저를 삭제 하지 않습니다. 시스템 관리자에 확장된 저장된 프로시저에 EXECUTE 권한을 거부 해야 대신 합니다 **공용** 역할입니다.  
  
 **sp_dropextendedproc** 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_dropextendedproc**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `xp_hello` 확장 저장 프로시저를 삭제합니다.  
  
> [!NOTE]  
>  이 확장 저장 프로시저가 이미 존재해야 하며 그렇지 않으면 예에서 오류 메시지를 반환합니다.  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
