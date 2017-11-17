---
title: SUSER_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e098c614f4e70cabf718ee4413920e61eb634c1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="suserid-transact-sql"></a>SUSER_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자의 로그인 ID를 반환합니다.  
  
> [!NOTE]  
>  부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID로 나열 된 값을 반환 합니다. **principal_id** 에 **sys.server_principals** 카탈로그 뷰.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>인수  
 **'** *로그인* **'**  
 사용자의 로그인 이름입니다. *로그인* 은 **nchar**합니다. 경우 *로그인* 로 지정 된 **char**, *로그인* 암시적으로 변환할 **nchar**합니다. *로그인* 하나일 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이나 Windows 사용자 또는 그룹의 인스턴스에 연결할 수 있는 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우 *로그인* 은 지정 하지 않으면 현재 사용자에 대 한 로그인 id 번호 반환 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 SUSER_ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부에서 명시적으로 제공된 로그인에 대해서만 ID를 반환합니다. 이 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 소유권 및 사용 권한을 추적하는 데 사용되며 SUSER_SID가 반환하는 로그인의 SID와는 다릅니다. 경우 *로그인* SQL Server 로그인 SID 매핑되는 GUID입니다. 경우 *로그인* 이 Windows 로그인 또는 Windows 그룹인 경우 SID는 Windows 보안 id에 매핑됩니다.  
  
 SUSER_SID는 항목이 있는 로그인에 대해서만 SUID를 반환 합니다.는 **syslogins** 시스템 테이블입니다.  
  
 시스템 함수는 WHERE 절의 선택 목록 및 식 어디서나 사용될 수 있으며 매개 변수가 지정되지 않아도 항상 뒤에 괄호가 와야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sa` 로그인에 대한 로그인 ID를 반환합니다.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40; Transact SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

