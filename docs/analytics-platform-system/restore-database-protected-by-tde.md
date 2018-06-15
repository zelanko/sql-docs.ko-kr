---
title: 병렬 데이터 웨어하우스-TDE로 보호 되는 데이터베이스를 복원 | Microsoft Docs
description: 분석 플랫폼 시스템 병렬 데이터 웨어하우스에서 투명 한 데이터 암호화를 사용 하 여 암호화 된 데이터베이스를 복원 하려면 다음 단계를 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538613"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에서 TDE로 보호 되는 데이터베이스를 복원 합니다.
투명 한 데이터 암호화를 사용 하 여 암호화 된 데이터베이스를 복원 하려면 다음 단계를 사용 합니다.  
  
[투명 한 데이터 암호화를 사용 하 여](transparent-data-encryption.md#using-tde) 예제에서 TDE를 설정 하는 코드에는 `AdventureWorksPDW2012` 데이터베이스입니다. 다음 코드는 해당 예제에서는 원래 Analytics Platform System (APS) 어플라이언스에서 데이터베이스의 백업을 만들고 다음 인증서와 다른 장치에서 사용 데이터베이스를 복원 하 여 계속 합니다.  
  
첫 번째 단계는 원본 데이터베이스의 백업을 만드는 것입니다.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
TDE에 대 한 마스터 키를 만들고 암호화를 사용 하면 네트워크 자격 증명을 만드는 새 SQL Server PDW를 준비 합니다.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
마지막 두 단계는 원래 SQL Server PDW에서 백업을 사용 하 여 인증서를 다시 만듭니다. 인증서의 백업을 만들 때 사용한 암호를 사용 합니다.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 백업](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[인증서 만들기](../t-sql/statements/create-certificate-transact-sql.md)  
[데이터베이스 복원](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
