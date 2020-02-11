---
title: sp_addextendedproc (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 0bc8ea22699762927a026ae4cc811500c193555c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68072748"
---
# <a name="sp_addextendedproc-transact-sql"></a>sp_addextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 확장 저장 프로시저의 이름을에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]등록 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>인수  
`[ @functname = ] 'procedure'`DLL (동적 연결 라이브러리)에서 호출할 함수의 이름입니다. *프로시저* 는 **nvarchar (517)** 이며 기본값은 없습니다. 필요한 경우 *프로시저* 는 owner *. 함수*형식으로 소유자 이름을 포함할 수 있습니다.  
  
`[ @dllname = ] 'dll'`함수를 포함 하는 DLL의 이름입니다. *dll* 은 **varchar (255)** 이며 기본값은 없습니다. DLL의 전체 경로를 지정하는 것이 좋습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 확장 저장 프로시저를 만든 후에는 **sp_addextendedproc**를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 추가 해야 합니다. 자세한 내용은 [SQL Server에 확장 저장 프로시저 추가](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)를 참조 하세요.  
  
 이 프로시저는 **master** 데이터베이스 에서만 실행할 수 있습니다. **Master**이외의 데이터베이스에서 확장 저장 프로시저를 실행 하려면 **master**를 사용 하 여 확장 저장 프로시저의 이름을 한정 합니다.  
  
 **sp_addextendedproc** 는 새 확장 저장 프로시저의 이름을로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]등록 하는 항목을 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에 추가 합니다. 또한 [sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) 카탈로그 뷰에 항목을 추가 합니다.  
  
> [!IMPORTANT]  
>  전체 경로에 등록되지 않은 기존 DLL은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후에 작동하지 않습니다. 이 문제를 해결 하려면 **sp_dropextendedproc** 를 사용 하 여 DLL의 등록을 취소 한 다음 전체 경로를 지정 하 여 **sp_addextendedproc**에 다시 등록 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_addextendedproc**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **xp_hello** 확장 저장 프로시저를 추가 합니다.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Transact-sql&#41;sp_dropextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Transact-sql&#41;sp_helpextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
