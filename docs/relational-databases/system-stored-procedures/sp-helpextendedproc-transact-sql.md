---
title: sp_helpextendedproc (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c5ce565f6e393f09aa25c63fc8d12883434fb6d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 정의되어 있는 확장 저장 프로시저와 프로시저(함수)가 속한 DLL(동적 링크 라이브러리)의 이름을 보고합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@funcname =**] **'***프로시저***'**  
 정보를 보고할 확장 저장 프로시저의 이름입니다. *프로시저* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|확장 저장 프로시저의 이름입니다.|  
|**dll**|**nvarchar(255)**|DLL의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 때 *프로시저* 지정 된 **sp_helpextendedproc** 보고서에 지정 된 확장 저장된 프로시저입니다. 이 매개 변수가 제공 되지 않으면 **sp_helpextendedproc** 속한 모든 확장 저장된 프로시저 이름과 각 확장 저장된 프로시저 DLL 이름을 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 실행할 수 있는 권한이 **sp_helpextendedproc** 에 부여 **공용**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>1. 모든 확장 저장 프로시저에 관한 도움말 보고  
 다음 예에서는 모든 확장 저장 프로시저에 관해 보고합니다.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>2. 단일 확장 저장 프로시저에 관한 도움말 보고  
 다음 예제에서는 예제에서 `xp_cmdshell` 확장 저장된 프로시저입니다.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addextendedproc &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
