---
title: sp_procoption (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3c4c9907c52ad99e1a397b4ad08f9897b6a0c4d5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018213"
---
# <a name="spprocoption-transact-sql"></a>sp_procoption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  저장 프로시저의 자동 실행을 설정하거나 해제합니다. 자동으로 실행되도록 설정된 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작될 때마다 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>인수  
 [  **@ProcName =** ] **'***프로시저***'**  
 옵션을 설정할 프로시저의 이름이입니다. *프로시저* 됩니다 **nvarchar(776)**, 기본값은 없습니다.  
  
 [  **@OptionName =** ] **'***옵션***'**  
 설정할 옵션의 이름입니다. 에 대 한 값만 *옵션* 됩니다 **시작**합니다.  
  
 [  **@OptionValue =** ] **'***값***'**  
 옵션을 설정할 것인지 여부입니다 (**true** 또는 **온**) 또는 해제 (**false** 또는 **해제**). *값* 됩니다 **varchar(12)**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 오류 번호(실패)  
  
## <a name="remarks"></a>Remarks  
 시작 프로시저에 있어야 합니다 **마스터** 데이터베이스 하며 입력 또는 출력 매개 변수를 포함할 수 없습니다. 시작할 때 모든 데이터베이스가 복구되고 "복구 완료" 메시지가 기록되면 저장 프로시저의 실행이 시작됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 프로시저의 자동 실행을 설정합니다.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';   
```  
  
 다음 예에서는 저장 프로시저가 자동으로 실행되지 않도록 설정합니다.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>관련 항목  
 [저장 프로시저 실행](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
