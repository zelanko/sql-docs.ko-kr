---
title: xp_sqlmaint (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9948767ca0eca5721207079f978987142653e9c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091916"
---
# <a name="xp_sqlmaint-transact-sql"></a>xp_sqlmaint(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sqlmaint**스위치를 포함 하는 문자열을 사용 하 여 **sqlmaint** 유틸리티를 호출 합니다. **Sqlmaint** 유틸리티는 하나 이상의 데이터베이스에서 유지 관리 작업 집합을 수행 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>인수  
 **'** *switch_string* **'**  
 는 **sqlmaint** 유틸리티 스위치를 포함 하는 문자열입니다. 스위치와 해당 값은 공백으로 구분되어야 합니다.  
  
 **-?** 스위치가 **xp_sqlmaint**에 적합 하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음 **Sqlmaint** 유틸리티에 오류가 발생 하는 경우 오류를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 SQL Server 인증을 사용 하 여 로그온 한 사용자가이 프로시저를 호출 하는 경우 **-U "***login_id***"** 및 **-P "***password***"** 스위치가 실행 되기 전에 *switch_string* 앞에 붙습니다. 사용자가 Windows 인증을 사용 하 여 로그온 한 경우에는 **sqlmaint**로 변경 하지 않고 *switch_string* 전달 됩니다.  
  
## <a name="permissions"></a>사용 권한  
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
  
## <a name="see-also"></a>참고 항목  
 [sqlmaint 유틸리티](../../tools/sqlmaint-utility.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
