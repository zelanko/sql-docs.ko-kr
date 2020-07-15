---
title: ALTER CREDENTIAL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER CREDENTIAL
- ALTER_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], credentials
- credentials [SQL Server], ALTER CREDENTIAL statement
- modifying credentials
- authentication [SQL Server], credentials
- ALTER CREDENTIAL statement
ms.assetid: b08899a6-c09e-4af4-91aa-a978ada79264
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e30cc37a64f21bd4cae48071e94a98f18160e171
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301990"
---
# <a name="alter-credential-transact-sql"></a>ALTER CREDENTIAL(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  자격 증명의 속성을 변경합니다.  

> [!IMPORTANT]
> 모범 사례로 “수행할 작업” 정보는 작업을 완료하기 위해 “반드시 수행”해야 합니다. ![ 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *credential_name*  
 변경할 자격 증명의 이름을 지정합니다.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다.  
  
 SECRET **='***secret***'**  
 나가는 인증에 필요한 암호를 지정합니다. *비밀*은 선택 사항입니다.
  
> [!IMPORTANT]
> Azure SQL Database는 Azure Key Vault와 공유 액세스 서명 ID만 지원합니다. Windows 사용자 ID는 지원되지 않습니다.
  
## <a name="remarks"></a>설명  
 자격 증명이 변경되면 *identity_name*과 *비밀*의 값이 모두 다시 설정됩니다. 옵션인 SECRET 인수를 지정하지 않으면 저장된 암호 값이 NULL로 설정됩니다.  
  
 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
  
 자격 증명에 대한 정보는 **sys.credentials** 카탈로그 뷰에 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY CREDENTIAL 권한이 필요합니다. 자격 증명이 시스템 자격 증명인 경우에는 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-a-credential"></a>A. 자격 증명의 암호 변경  
 다음 예에서는 `Saddles`라는 자격 증명에 저장된 암호를 변경합니다. 이 자격 증명에는 `RettigB` Windows 로그인과 해당 암호가 들어 있습니다. 새 암호는 SECRET 절을 사용하여 자격 증명에 추가됩니다.  
  
```  
ALTER CREDENTIAL Saddles WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 자격 증명에서 암호 제거  
 다음 예에서는 `Frames`라는 자격 증명에서 암호를 제거합니다. 이 자격 증명에는 `Aboulrus8` Windows 로그인과 해당 암호가 들어 있습니다. SECRET 옵션이 지정되지 않았기 때문에 문이 실행된 후에는 자격 증명 암호가 NULL이 됩니다.  
  
```  
ALTER CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
