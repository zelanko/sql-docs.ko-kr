---
title: sp_addextendedproc (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2083d370479fa19049a083ef401574f21740929c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239793"
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  확장 저장된 프로시저의 새 이름을 등록 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>인수  
 [  **@functname =** ] **'***프로시저***'**  
 DDL(동적 연결 라이브러리)에서 호출할 함수의 이름입니다. *프로시저* 은 **nvarchar (517)**, 기본값은 없습니다. *프로시저* 필요에 따라 소유자 이름 포함 형태로 *owner.function*합니다.  
  
 [  **@dllname =** ] **'***dll***'**  
 함수를 포함하고 있는 DLL의 이름입니다. *dll* 은 **varchar (255)**, 기본값은 없습니다. DLL의 전체 경로를 지정하는 것이 좋습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 확장된 저장된 프로시저를 만든 후에 추가 되어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 **sp_addextendedproc**합니다. 자세한 내용은 참조 [확장 저장 프로시저를 SQL Server에 추가](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)합니다.  
  
 이 프로시저에만 실행할 수 있습니다는 **마스터** 데이터베이스입니다. 이외의 다른 데이터베이스에서 확장된 저장된 프로시저를 실행 하려면 **마스터**와 확장된 저장된 프로시저의 이름을 한정 **마스터**합니다.  
  
 **sp_addextendedproc** 항목을 추가 하는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰, 새 이름 등록과 확장 저장된 프로시저를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 또한 추가 항목에는 [sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 카탈로그 뷰.  
  
> [!IMPORTANT]  
>  전체 경로에 등록되지 않은 기존 DLL은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후에 작동하지 않습니다. 문제를 해결 하려면 사용 **sp_dropextendedproc** DLL을 등록 취소 하 고 다음 사용 하 여 다시 등록 **sp_addextendedproc**, 전체 경로 지정 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_addextendedproc**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 추가 **xp_hello** 확장 저장된 프로시저입니다.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
