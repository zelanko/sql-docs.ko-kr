---
title: ALTER CERTIFICATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_CERTIFICATE_TSQL
- ALTER CERTIFICATE
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- encryption [SQL Server], certificates
- modifying certificates
- private keys [SQL Server]
- ALTER CERTIFICATE statement
- certificates [SQL Server], modifying
ms.assetid: da4dc25e-72e0-4036-87ce-22de83160836
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30f81401f3f322f44d71df139e4f9cfafa6c9de8
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81629523"
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  인증서의 프라이빗 키를 암호화하는 데 사용되는 암호를 변경하고, 프라이빗 키를 제거하거나 존재하지 않은 경우 프라이빗 키를 가져옵니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]에 대한 인증서의 가용성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> )  
    | WITH ACTIVE FOR BEGIN_DIALOG = { ON | OFF }  
  
<private_key_spec> ::=   
      {   
        { FILE = 'path_to_private_key' | BINARY = private_key_bits }  
         [ , DECRYPTION BY PASSWORD = 'current_password' ]  
         [ , ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
    |  
      {  
         [ DECRYPTION BY PASSWORD = 'current_password' ]  
         [ [ , ] ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  
  
## <a name="arguments"></a>인수  
 *certificate_name*  
 데이터베이스에서 인증서를 식별하는 고유한 이름입니다.  
  
 REMOVE PRIVATE KEY  
 데이터베이스 내에서 더 이상 프라이빗 키를 유지하지 않도록 지정합니다.  
  
 WITH PRIVATE KEY 인증서의 프라이빗 키가 SQL Server에 저장되도록 지정합니다.

 FILE ='*path_to_private_key*'  
 프라이빗 키에 대해 파일 이름을 포함하여 전체 경로를 지정합니다. 이 매개 변수는 로컬 경로이거나 네트워크 위치에 대한 UNC 경로가 될 수 있습니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트 내에서 액세스할 수 있습니다. 이 옵션을 사용할 경우 서비스 계정이 지정된 파일에 액세스할 수 있는지 확인합니다.
 
 파일 이름만 지정하는 경우 파일은 인스턴스의 기본 사용자 데이터 폴더에 저장됩니다. 이 폴더는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 폴더일 수도 있고 아닐 수도 있습니다. SQL Server Express LocalDB의 경우 인스턴스의 기본 사용자 데이터 폴더는 인스턴스를 생성한 계정의 `%USERPROFILE%` 환경 변수에 의해 지정된 경로입니다.  
  
 BINARY ='*private_key_bits*'  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 이진 상수로 지정되는 프라이빗 키 비트입니다. 이러한 비트는 암호화된 형식일 수 있습니다. 암호화된 경우 사용자는 해독 암호를 입력해야 합니다. 이 암호에 대해서는 암호 정책 확인이 수행되지 않습니다. 프라이빗 키 비트는 PVK 파일 형식이어야 합니다.  
  
 DECRYPTION BY PASSWORD ='*current_password*'  
 프라이빗 키를 해독하는 데 필요한 암호를 지정합니다.  
  
 ENCRYPTION BY PASSWORD ='*new_password*'  
 데이터베이스에서 인증서의 프라이빗 키를 암호화하는 데 사용되는 암호를 지정합니다. *new_password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
 ACTIVE FOR BEGIN_DIALOG **=** { ON | OFF }  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 기능의 시작자가 인증서를 사용할 수 있게 합니다.  
  
## <a name="remarks"></a>설명  
 프라이빗 키는 *certificate_name*으로 지정한 퍼블릭 키와 일치해야 합니다.  
  
 파일에 있는 암호가 Null 암호로 보호되는 경우에는 DECRYPTION BY PASSWORD 절을 생략할 수 있습니다.  
  
 데이터베이스에 이미 있는 인증서의 프라이빗 키를 가져오는 경우 해당 프라이빗 키는 데이터베이스 마스터 키에 의해 자동으로 보호됩니다. 프라이빗 키를 암호로 보호하려면 ENCRYPTION BY PASSWORD 절을 사용합니다.  
  
 REMOVE PRIVATE KEY 옵션을 사용하면 데이터베이스에서 인증서의 프라이빗 키를 삭제할 수 있습니다. 서명 확인에 인증서를 사용할 때 또는 프라이빗 키가 필요 없는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 시나리오에서 프라이빗 키를 제거할 수 있습니다. 대칭 키를 보호하는 인증서의 프라이빗 키는 제거하지 마십시오. 인증서로 확인해야 하는 추가 모듈이나 문자열에 서명하거나 인증서로 암호화된 값을 해독하려면 프라이빗 키를 복원해야 합니다.   
  
 데이터베이스 마스터 키를 사용하여 프라이빗 키를 암호화한 경우에는 해독 암호를 지정할 필요가 없습니다.  
 
 프라이빗 키를 암호화하는 데 사용되는 암호를 변경하려면 FILE 또는 BINARY 절을 지정하지 마세요.
  
> [!IMPORTANT]  
>  데이터베이스에서 프라이빗 키를 제거하기 전에 복사본을 만들어 보관하십시오. 자세한 내용은 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md) 및 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)을 참조하세요.  
  
 포함된 데이터베이스에서는 WITH PRIVATE KEY 옵션을 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 인증서에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-the-private-key-of-a-certificate"></a>A. 인증서의 프라이빗 키 제거  
  
```  
ALTER CERTIFICATE Shipping04   
    REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. 프라이빗 키를 암호화하는 데 사용된 암호 변경  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%',  
    ENCRYPTION BY PASSWORD = '34958tosdgfkh##38');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. 데이터베이스의 기존 인증서에 대한 프라이빗 키 가져오기  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. 프라이빗 키 보호를 암호에서 데이터베이스 마스터 키로 변경  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)  
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

