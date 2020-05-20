---
title: sp_xp_cmdshell_proxy_account (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xp_cmdshell_proxy_account
- sp_xp_cmdshell_proxy_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xp_cmdshell_proxy_account
- xp_cmdshell
ms.assetid: f807c373-7fbc-4108-a2bd-73b48a236003
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e908d0bfb70e60330ce47377a8537ebe25f80f09
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827467"
---
# <a name="sp_xp_cmdshell_proxy_account-transact-sql"></a>sp_xp_cmdshell_proxy_account(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **Xp_cmdshell**에 대 한 프록시 자격 증명을 만듭니다.  
  
> [!NOTE]  
>  **xp_cmdshell** 은 기본적으로 사용 되지 않습니다. **Xp_cmdshell**를 사용 하도록 설정 하려면 [Xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>인수  
 NULL  
 프록시 자격 증명을 삭제하도록 지정합니다.  
  
 *account_name*  
 프록시가 될 Windows 로그인을 지정합니다.  
  
 *password*  
 Windows 계정의 암호를 지정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 프록시 자격 증명을 **# #xp_cmdshell_proxy_account # #** 이라고 합니다.  
  
 NULL 옵션을 사용 하 여 실행 되는 경우 **sp_xp_cmdshell_proxy_account** 는 프록시 자격 증명을 삭제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-the-proxy-credential"></a>A. 프록시 자격 증명 만들기  
 다음 예에서는 `ADVWKS\Max04` 암호를 사용하여 `ds35efg##65`라는 Windows 계정에 대한 프록시 자격 증명을 만드는 방법을 보여 줍니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'ADVWKS\Max04', 'ds35efg##65';  
GO  
```  
  
### <a name="b-dropping-the-proxy-credential"></a>B. 프록시 자격 증명 삭제  
 다음 예에서는 자격 증명 저장소에서 프록시 자격 증명을 제거합니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account NULL;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;xp_cmdshell &#40;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [Transact-sql&#41;자격 증명 &#40;만들기](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys. 자격 증명 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
