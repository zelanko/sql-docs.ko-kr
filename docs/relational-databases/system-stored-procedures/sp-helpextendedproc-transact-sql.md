---
title: sp_helpextendedproc (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 3dcbe6d187b56b0b15ae829eeecf1811b02dfee7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67943503"
---
# <a name="sp_helpextendedproc-transact-sql"></a>sp_helpextendedproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 정의되어 있는 확장 저장 프로시저와 프로시저(함수)가 속한 DLL(동적 링크 라이브러리)의 이름을 보고합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @funcname = ] 'procedure'`정보가 보고 되는 확장 저장 프로시저의 이름입니다. *프로시저* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|확장 저장 프로시저의 이름입니다.|  
|**gdiplus.dll**|**nvarchar(255)**|DLL의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 *프로시저* 를 지정 하면 지정 된 확장 저장 프로시저에 대해 보고서를 **sp_helpextendedproc** 합니다. 이 매개 변수를 지정 하지 않으면 **sp_helpextendedproc** 는 확장 저장 프로시저의 모든 확장 저장 프로시저 이름 및 DLL 이름을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sp_helpextendedproc** 를 실행할 수 있는 권한은 **public**에 부여 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. 모든 확장 저장 프로시저에 관한 도움말 보고  
 다음 예에서는 모든 확장 저장 프로시저에 관해 보고합니다.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. 단일 확장 저장 프로시저에 관한 도움말 보고  
 다음 예에서는 `xp_cmdshell` 확장 저장 프로시저에 대해 보고 합니다.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [Transact-sql&#41;sp_dropextendedproc &#40;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
