---
title: "백업 인증서 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: fb1632ed04904150247280962d8423a493b51d60
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  인증서를 파일로 내보냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
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
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
## <a name="arguments"></a>인수  
 *path_to_file*  
 인증서를 저장할 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 기본 경로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 폴더입니다.  
  
 *path_to_private_key_file*  
 개인 키를 저장할 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 기본 경로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA 폴더입니다.  
  
 *encryption_password*  
 키를 백업 파일에 작성하기 전에 개인 키를 암호화하는 데 사용되는 암호입니다. 이 암호의 복잡성을 확인해야 합니다.  
  
 *decryption_password*  
 키를 백업하기 전에 개인 키의 암호를 해독하는 데 사용되는 암호입니다.  
  
## <a name="remarks"></a>주의  
 개인 키가 데이터베이스에 있는 암호로 암호화된 경우 암호 해독 암호를 지정해야 합니다.  
  
 개인 키를 파일로 백업할 때는 암호화가 필요합니다. 백업된 인증서를 보호하는 데 사용되는 암호는 인증서의 개인 키를 암호화하는 데 사용되는 암호와 다릅니다.  
  
 사용 하 여 인증서를 백업 된 복원는 [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md)문.  
  
## <a name="permissions"></a>Permissions  
 인증서에 대한 CONTROL 권한이 필요하고 개인 키를 암호화하는 데 사용된 암호를 알고 있어야 합니다. 인증서의 공개 부분만 백업하면 인증서에 대한 일부 권한이 필요하고 호출자가 인증서에 대해 VIEW 권한이 거부되지 않아야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>1. 인증서를 파일로 내보내기  
 다음 예에서는 인증서를 파일로 내보냅니다.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>2. 인증서와 개인 키 내보내기  
 다음 예에서는 백업된 인증서의 개인 키가 암호 `997jkhUbhk$w4ez0876hKHJH5gh`를 사용하여 암호화됩니다.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>3. 개인 키가 암호화된 인증서 내보내기  
 다음 예에서 인증서의 개인 키가 데이터베이스에서 암호화됩니다. 개인 키는 암호 `9875t6#6rfid7vble7r`로 암호화되어야 합니다. 인증서가 백업 파일에 저장될 때 개인 키는 암호 `9n34khUbhk$w4ecJH5gh`로 암호화됩니다.  
  
```  
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
  
  


