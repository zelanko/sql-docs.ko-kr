---
title: ALTER DATABASE SCOPED CREDENTIAL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f76ff430e75f572378f0ed1994ed6ed204a20fa9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008492"
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스 범위 자격 증명의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 변경할 데이터베이스 범위 자격 증명의 이름을 지정합니다.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. Azure Blob 스토리지에서 파일을 가져오려면 ID 이름이 `SHARED ACCESS SIGNATURE`여야 합니다.  공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.  
    
  
 SECRET **='***secret***'**  
 나가는 인증에 필요한 암호를 지정합니다. *secret*은 Azure Blob 스토리지에서 파일을 가져오는 데 필요합니다. *secret*은 다른 용도에 대해서는 선택 사항이 될 수 있습니다.   
> [!WARNING]
>  SAS 키 값은 '?'(물음표)로 시작될 수 있습니다. SAS 키를 사용할 때는 앞의 '?'를 제거해야 합니다. 그렇지 않으면 작업이 차단될 수 있습니다.    
  
## <a name="remarks"></a>설명  
 데이터베이스 범위 자격 증명이 변경되면 *identity_name*과 *secret*의 값이 모두 다시 설정됩니다. 옵션인 SECRET 인수를 지정하지 않으면 저장된 암호 값이 NULL로 설정됩니다.  
  
 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
  
 데이터베이스 범위 자격 증명에 대한 내용은 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 자격 증명에 대한 `ALTER` 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. 데이터베이스 범위 자격 증명의 암호 변경  
 다음 예에서는 `Saddles`라는 데이터베이스 범위 자격 증명에 저장된 암호를 변경합니다. 데이터베이스 범위 자격 증명에는 `RettigB` Windows 로그인과 해당 암호가 들어 있습니다. 새 암호는 SECRET 절을 사용하여 데이터베이스 범위 자격 증명에 추가됩니다.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 자격 증명에서 암호 제거  
 다음 예에서는 `Frames`라는 데이터베이스 범위 자격 증명에서 암호를 제거합니다. 데이터베이스 범위 자격 증명에는 `Aboulrus8` Windows 로그인과 해당 암호가 들어 있습니다. SECRET 옵션이 지정되지 않았기 때문에 문이 실행된 후에는 데이터베이스 범위 자격 증명 암호가 NULL이 됩니다.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
