---
title: PWDCOMPARE (Transact SQL) | Microsoft Docs
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
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aadde33d6d1ee1404170197c32ab77ade2dbfad
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  암호를 해시하고 해당 해시를 기존 암호의 해시와 비교합니다. PWDCOMPARE를 사용하여 빈 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 암호 또는 일반적인 약한 암호를 검색할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>인수  
 **'** *clear_text_password* **'**  
 암호화되지 않은 암호입니다. *clear_text_password* 은 **sysname** (**nvarchar (128)**).  
  
 *password_hash*  
 암호의 암호화 해시입니다. *password_hash* 은 **varbinary(128)**합니다.  
  
 *버전*  
 경우 1로 설정할 수 있는 매개 변수를 사용 되지 않는 *password_hash* 로그인에서 값을 나타내는 보다 이전 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 으로 마이그레이션 되었지만 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 버전 하지만으로 변환 되지 않은 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 시스템입니다. *버전* 은 **int**합니다.  
  
> [!CAUTION]  
>  이 매개 변수는 이전 버전과의 호환성을 위해 제공되지만 지금 암호 해시 BLOB이 해당 버전 설명을 포함하고 있으므로 무시됩니다. [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 1을 반환의 해시는 *clear_text_password* 일치는 *password_hash* 매개 변수를, 그렇지 않으면 0입니다.  
  
## <a name="remarks"></a>주의  
 암호를 첫 번째 매개 변수로 지정하여 로그인을 시도함으로써 동일한 테스트를 수행할 수 있으므로 PWDCOMPARE 함수는 암호 해시의 강력함에 대한 위협이 되지 않습니다.  
  
 **PWDCOMPARE** 포함 된 데이터베이스 사용자의 암호와 함께 사용할 수 없습니다. 동등한 포함된 데이터베이스가 없습니다.  
  
## <a name="permissions"></a>Permissions  
 PWDENCRYPT는 누구나 사용할 수 있습니다.  
  
 sys.sql_logins의 password_hash 열을 검사하려면 CONTROL SERVER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>1. 암호가 없는 로그인 식별  
 다음 예에서는 암호가 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 식별합니다.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>2. 일반적인 암호 검색  
 식별하여 변경할 일반적인 암호를 검색하려면 암호를 첫 번째 매개 변수로 지정합니다. 예를 들어 `password`로 지정된 암호를 검색하려면 다음 문을 실행합니다.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [PWDENCRYPT &#40; Transact SQL &#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

