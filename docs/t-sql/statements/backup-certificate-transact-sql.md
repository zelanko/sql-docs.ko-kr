---
description: BACKUP CERTIFICATE(Transact-SQL)
title: BACKUP CERTIFICATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DUMP_CERTIFICATE_TSQL
- BACKUP CERTIFICATE
- sql13.swb.exportcertificate.f1
- DUMP CERTIFICATE
- BACKUP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- decryption [SQL Server], certificates
- exporting certificates
- certificates [SQL Server], exporting
- BACKUP CERTIFICATE statement
- backing up certificates [SQL Server]
- decryption [SQL Server]
- cryptography [SQL Server], certificates
ms.assetid: 509b9462-819b-4c45-baae-3d2d90d14a1c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017'
ms.openlocfilehash: d37f473dad430d9b0be03beb83be2aa81da615ee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460846"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE(Transact-SQL)
[!INCLUDE [sql-pdw](../../includes/applies-to-version/sql-pdw.md)]

  인증서를 파일로 내보냅니다.  
  
 ![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
   
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *certname*  
 백업할 인증서의 이름입니다.

 TO FILE = '*path_to_file*'  
 인증서를 저장할 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 파일 이름만 지정한 경우 파일은 인스턴스의 기본 사용자 데이터 폴더([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 폴더일 수도 있고 아닐수도 있음)에 저장됩니다. SQL Server Express LocalDB의 경우 인스턴스의 기본 사용자 데이터 폴더는 인스턴스를 만든 계정의 `%USERPROFILE%` 환경 변수에 의해 지정된 경로입니다.  

 WITH PRIVATE KEY 인증서의 프라이빗 키를 파일에 저장되도록 지정합니다. 이 절은 옵션입니다.

 FILE = '*path_to_private_key_file*'  
 프라이빗 키를 저장할 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 파일 이름만 지정한 경우 파일은 인스턴스의 기본 사용자 데이터 폴더([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 폴더일 수도 있고 아닐수도 있음)에 저장됩니다. SQL Server Express LocalDB의 경우 인스턴스의 기본 사용자 데이터 폴더는 인스턴스를 만든 계정의 `%USERPROFILE%` 환경 변수에 의해 지정된 경로입니다.  

 ENCRYPTION BY PASSWORD = '*encryption_password*'  
 키를 백업 파일에 작성하기 전에 프라이빗 키를 암호화하는 데 사용되는 암호입니다. 이 암호의 복잡성을 확인해야 합니다.  
  
 DECRYPTION BY PASSWORD = '*decryption_password*'  
 키를 백업하기 전에 프라이빗 키의 암호를 해독하는 데 사용되는 암호입니다. 이 인수는 인증서가 마스터 키로 암호화된 경우에는 필요하지 않습니다. 
  
## <a name="remarks"></a>설명  
 프라이빗 키가 데이터베이스에 있는 암호로 암호화된 경우 암호 해독 암호를 지정해야 합니다.  
  
 프라이빗 키를 파일로 백업할 때는 암호화가 필요합니다. 파일의 프라이빗 키를 보호하는 데 사용되는 암호는 데이터베이스에 있는 인증서의 프라이빗 키를 암호화하는 데 사용되는 암호와 다릅니다.  

 프라이빗 키는 PVK 파일 형식으로 저장됩니다.

 프라이빗 키의 유무와 관계없이 백업된 인증서를 복원하려면 [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md) 문을 사용합니다.
 
 데이터베이스의 기존 인증서에 프라이빗 키를 복원하려면 [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md) 문을 사용합니다.
 
 백업을 수행할 때 파일은 SQL Server 인스턴스의 서비스 계정에 대한 ACL이 됩니다. 다른 계정으로 실행하는 서버로 인증서를 복원해야 할 경우 새 계정에서 읽을 수 있도록 파일에 대한 권한을 조정해야 합니다. 
  
## <a name="permissions"></a>사용 권한  
 인증서에 대한 CONTROL 권한이 필요하고 프라이빗 키를 암호화하는 데 사용된 암호를 알고 있어야 합니다. 인증서의 공개 부분만 백업하는 경우 이 명령을 사용하려면 인증서에 대한 일부 권한이 필요하고 호출자가 인증서에 대해 VIEW 권한이 거부되지 않아야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>A. 인증서를 파일로 내보내기  
 다음 예에서는 인증서를 파일로 내보냅니다.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. 인증서와 프라이빗 키 내보내기  
 다음 예에서는 백업된 인증서의 프라이빗 키가 암호 `997jkhUbhk$w4ez0876hKHJH5gh`를 사용하여 암호화됩니다.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. 프라이빗 키가 암호화된 인증서 내보내기  
 다음 예에서 인증서의 프라이빗 키가 데이터베이스에서 암호화됩니다. 프라이빗 키는 암호 `9875t6#6rfid7vble7r`로 암호화되어야 합니다. 인증서가 백업 파일에 저장될 때 프라이빗 키는 암호 `9n34khUbhk$w4ecJH5gh`로 암호화됩니다.  
  
```sql
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

