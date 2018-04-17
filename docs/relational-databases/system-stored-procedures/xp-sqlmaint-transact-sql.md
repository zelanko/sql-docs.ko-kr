---
title: xp_sqlmaint (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea6da80de3845f87d3e8bef7757e13bb71c8b737
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  호출 된 **sqlmaint** 유틸리티를 포함 하는 문자열 **sqlmaint**스위치입니다. **sqlmaint** 유틸리티는 하나 이상의 데이터베이스에서 유지 관리 작업의 집합을 수행 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>인수  
 **'** *switch_string* **'**  
 문자열을 포함 하는 **sqlmaint** 유틸리티 스위치입니다. 스위치와 해당 값은 공백으로 구분되어야 합니다.  
  
 **-?** 스위치에 대해 올바르지 않습니다. **xp_sqlmaint**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음 오류를 반환 된 **sqlmaint** 유틸리티 실패 합니다.  
  
## <a name="remarks"></a>주의  
 SQL Server 인증으로 로그온 한 사용자가이 프로시저를 호출 하는 경우는 **-U "***login_id***"** 및 **-P "***암호***"** 스위치 앞에 놓이게 됩니다 *switch_string* 실행 하기 전에. 사용자가 Windows 인증으로 로그온 하는 경우 *switch_string* 를 변경 하지 않고 전달 **sqlmaint**합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `xp_sqlmaint`가 무결성 검사를 수행하고 보고서 파일을 만들며, `sqlmaint`를 업데이트하기 위해 `msdb.dbo.sysdbmaintplan_history`를 호출합니다.  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sqlmaint 유틸리티](../../tools/sqlmaint-utility.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
