---
title: sp_helpextendedproc (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43d9180ace10e61bbb9a9e65f48e718b8b426ea8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763881"
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 정의되어 있는 확장 저장 프로시저와 프로시저(함수)가 속한 DLL(동적 링크 라이브러리)의 이름을 보고합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@funcname =**] **'***프로시저***'**  
 정보를 보고할 확장 저장 프로시저의 이름입니다. *프로시저* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|확장 저장 프로시저의 이름입니다.|  
|**dll**|**nvarchar(255)**|DLL의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 때 *프로시저* 를 지정 하면 **sp_helpextendedproc** 확장 저장된 프로시저를 지정 된 보고서. 이 매개 변수가 제공 되지 않은 경우 **sp_helpextendedproc** 속한 모든 확장 저장된 프로시저 이름과 각 확장 저장된 프로시저 DLL 이름을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 실행할 수 있는 권한이 **sp_helpextendedproc** 에 부여 됩니다 **공용**합니다.  
  
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
 다음 예에서는 보고를 `xp_cmdshell` 확장 저장된 프로시저입니다.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
