---
title: "데이터베이스 범위 이름 자격 증명 (Transact SQL) ALTER | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b45b0d87b846c50abc678692021c427006b3152e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER 데이터베이스 SCOPED 자격 증명 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  데이터베이스의 속성 변경 범위 자격 증명입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 변경할 데이터베이스 범위 자격 증명의 이름을 지정 합니다.  
  
 IDENTITY **='***identity_name***'**  
 서버 외부에 연결할 때 사용할 계정의 이름을 지정합니다. Id 이름 이어야 합니다는 파일을 Azure Blob 저장소에서 가져오려면 `SHARED ACCESS SIGNATURE`합니다.  공유 액세스 서명에 대 한 자세한 내용은 참조 [를 사용 하 여 공유 액세스 서명 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)합니다.  
    
  
 비밀 **='***비밀***'**  
 나가는 인증에 필요한 암호를 지정합니다. *비밀* Azure Blob 저장소에서 파일을 가져오는 데 필요 합니다. *비밀* 다른 용도 대 한 선택 사항이 될 수 있습니다.   
>  [!WARNING]
>  SAS 키 값으로 시작는 '?' (물음표)입니다. 앞에 오는 제거 해야 SAS 키를 사용 하는 경우 '?'입니다. 그렇지 않으면 작업을 차단 될 수 있습니다.    
  
## <a name="remarks"></a>주의  
 때 한 데이터베이스 범위 자격 증명 변경 되 면 값이 모두 *identity_name* 및 *비밀* 다시 설정 됩니다. 옵션인 SECRET 인수를 지정하지 않으면 저장된 암호 값이 NULL로 설정됩니다.  
  
 암호는 서비스 마스터 키를 사용하여 암호화됩니다. 서비스 마스터 키가 다시 생성되면 암호가 새 서비스 마스터 키를 사용하여 다시 암호화됩니다.  
  
 데이터베이스 범위 자격 증명에 대 한 정보에 표시 되는 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 `ALTER` 자격 증명에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>1. 범위 자격 증명을 데이터베이스의 암호 변경  
 다음 예에서는 라는 데이터베이스 범위 자격 증명에 저장 된 암호를 변경 `Saddles`합니다. Windows 로그인을 포함 하는 데이터베이스 범위 자격 증명 `RettigB` 및 암호. 새 암호는 SECRET 절을 사용 하 여 데이터베이스 범위 자격 증명에 추가 됩니다.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>2. 자격 증명에서 암호 제거  
 다음 예에서는 데이터베이스 범위 자격 증명에서 암호를 제거 `Frames`합니다. Windows 로그인을 포함 하는 데이터베이스 범위 자격 증명 `Aboulrus8` 및 암호. 문이 실행 되는 데이터베이스 범위 자격 증명 SECRET 옵션이 지정 되어 있지 않으므로 NULL 암호를 갖게 됩니다.  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [DATABASE SCOPED credential&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED credential&#40; Transact SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
