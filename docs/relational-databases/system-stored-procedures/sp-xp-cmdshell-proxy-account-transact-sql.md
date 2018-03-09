---
title: sp_xp_cmdshell_proxy_account (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xp_cmdshell_proxy_account
- sp_xp_cmdshell_proxy_account_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_xp_cmdshell_proxy_account
- xp_cmdshell
ms.assetid: f807c373-7fbc-4108-a2bd-73b48a236003
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2aa36f38df0fdf1f36e5cfddc48044222d9509c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spxpcmdshellproxyaccount-transact-sql"></a>sp_xp_cmdshell_proxy_account(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  에 대 한 프록시 자격 증명을 만든 **xp_cmdshell**합니다.  
  
> [!NOTE]  
>  **xp_cmdshell** 기본적으로 비활성화 되어 있습니다. 사용할 수 있도록 **xp_cmdshell**, 참조 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>인수  
 NULL  
 프록시 자격 증명을 삭제하도록 지정합니다.  
  
 *account_name*  
 프록시가 될 Windows 로그인을 지정합니다.  
  
 *암호*  
 Windows 계정의 암호를 지정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 프록시 자격 증명 이름은 **# # xp_cmdshell_proxy_account # #**합니다.  
  
 NULL 옵션을 사용 하 여 실행 될 때 **sp_xp_cmdshell_proxy_account** 프록시 자격 증명을 삭제 합니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-the-proxy-credential"></a>1. 프록시 자격 증명 만들기  
 다음 예에서는 `ADVWKS\Max04` 암호를 사용하여 `ds35efg##65`라는 Windows 계정에 대한 프록시 자격 증명을 만드는 방법을 보여 줍니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'ADVWKS\Max04', 'ds35efg##65';  
GO  
```  
  
### <a name="b-dropping-the-proxy-credential"></a>2. 프록시 자격 증명 삭제  
 다음 예에서는 자격 증명 저장소에서 프록시 자격 증명을 제거합니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account NULL;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [xp_cmdshell &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
