---
title: sp_addextendedproc (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b895692bf9ce65d9e063fb1d484cf84734897c86
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494285"
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  확장 저장된 프로시저를 새 이름을 등록 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>인수  
`[ @functname = ] 'procedure'` 동적 연결 라이브러리 (DLL)에서 호출할 함수의 이름이입니다. *프로시저* 됩니다 **nvarchar(517)**, 기본값은 없습니다. *프로시저* 필요에 따라 폼의 소유자 이름을 포함할 수 있습니다 *owner.function*합니다.  
  
`[ @dllname = ] 'dll'` 함수를 포함 하는 DLL의 이름이입니다. *dll* 됩니다 **varchar(255)**, 기본값은 없습니다. DLL의 전체 경로를 지정하는 것이 좋습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 확장된 저장된 프로시저를 만든 후에 추가 되어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 **sp_addextendedproc**합니다. 자세한 내용은 [확장 저장 프로시저를 SQL Server에 추가](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)합니다.  
  
 이 절차를 에서만 실행할 수 있습니다 합니다 **마스터** 데이터베이스입니다. 이외의 다른 데이터베이스에서 확장된 저장된 프로시저를 실행할 **마스터**를 사용 하 여 확장된 저장된 프로시저 이름을 한 정하는 **마스터**.  
  
 **sp_addextendedproc** 항목을 추가 하는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰, 새 이름을 등록 확장 저장된 프로시저를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 또한 항목을 추가 합니다 [sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 카탈로그 뷰.  
  
> [!IMPORTANT]  
>  전체 경로에 등록되지 않은 기존 DLL은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후에 작동하지 않습니다. 문제를 해결 하려면 사용 **sp_dropextendedproc** DLL의 등록을 취소 한 다음 사용 하 여 다시 등록 하려면 **sp_addextendedproc**, 전체 경로 지정 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_addextendedproc**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에 추가 합니다 **xp_hello** 확장 저장된 프로시저입니다.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>관련 항목  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
