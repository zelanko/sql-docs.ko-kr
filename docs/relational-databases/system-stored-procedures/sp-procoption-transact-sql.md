---
description: sp_procoption(Transact-SQL)
title: sp_procoption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 161f819ba4d9cea76b6cf904b28236f6e6f9fefc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485854"
---
# <a name="sp_procoption-transact-sql"></a>sp_procoption(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  저장 프로시저의 자동 실행을 설정하거나 해제합니다. 자동으로 실행되도록 설정된 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시작될 때마다 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>인수  
`[ @ProcName = ] 'procedure'` 옵션을 설정 하는 프로시저의 이름입니다. *프로시저* 는 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @OptionName = ] 'option'` 설정할 옵션의 이름입니다. *Option* 의 유일한 값은 **startup**입니다.  
  
`[ @OptionValue = ] 'value'` 옵션을 (**true** 또는 **on**) 또는 off (**false** 또는 **off**)로 설정할지 여부입니다. *값* 은 **varchar (12)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 오류 번호(실패)  
  
## <a name="remarks"></a>설명  
 시작 프로시저는 **master** 데이터베이스에 있어야 하며 입력 또는 출력 매개 변수를 포함할 수 없습니다. 시작할 때 모든 데이터베이스가 복구되고 "복구 완료" 메시지가 기록되면 저장 프로시저의 실행이 시작됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 프로시저의 자동 실행을 설정합니다.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 다음 예에서는 저장 프로시저가 자동으로 실행되지 않도록 설정합니다.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
