---
title: "상시 암호화로 보호되는 중요한 데이터 마이그레이션 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 20eb76a9e2cc89015167b5199f1a6f8dd5baec16
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>상시 암호화로 보호되는 중요한 데이터 마이그레이션
 <a name="to-load-encrypted-data-without-performing-metadata-checks-on-the-server-during-bulk-copy-operations-create-the-user-with-the-allowencryptedvaluemodifications-option-this-option-is-intended-to-be-used-by-legacy-tools-from-versions-of-includessnoversionincludesssnoversion-mdmd-older-than-includesssql15includessssql15-mdmd-such-as-bcpexe-or-by-using-third-party-extract-transform-load-etl-work-flows-that-cannot-use-always-encrypted-this-allows-a-user-to-securely-move-encrypted-data-from-one-set-of-tables-containing-encrypted-columns-to-another-set-of-tables-with-encrypted-columns-in-the-same-or-a-different-database"></a>대량 복사 작업 중 서버에서 메타데이터 검사를 수행하지 않고 암호화된 데이터를 로드하려면 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 옵션으로 사용자를 만듭니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 버전의 레거시 도구(예: bcp.exe) 또는 상시 암호화를 사용할 수 없는 타사 ETL(추출-변환-로드) 워크플로를 통해 사용하기 위한 것입니다. 이를 통해 사용자는 암호화된 데이터를 암호화된 열이 포함된 하나의 테이블 집합에서 암호화된 열이 있는 다른 테이블 집합(같거나 다른 데이터베이스)으로 안전하게 이동할 수 있습니다.  
 -  
 -## The ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션  
 - [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 와 [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) 둘 다 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션이 있습니다. ON으로 설정되어 있는 경우(기본값은 OFF) 이 옵션은 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 억제하여 사용자는 데이터를 암호 해독하지 않고 테이블 또는 데이터베이스 간에 암호화된 데이터를 대량 복사할 수 있습니다.  
 -  
 -## 데이터 마이그레이션 시나리오  
 - 다음 표는 몇 가지 마이그레이션 시나리오에 적합한 권장된 설정을 보여줍니다.  
 -  
 - ![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  
 -  
 -## 암호화된 데이터의 대량 로드  
 - 다음 프로세스를 사용하여 암호화된 데이터를 로드합니다.  
 -  
 -1.  데이터베이스에서 대량 복사 작업 대상인 사용자에 대해 이 옵션을 ON으로 설정합니다. 예를 들어  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
 -    ```  
 -  
 -2.  Run your bulk copy application or tool connecting as that user. (If your application uses an Always Encrypted enabled client driver, make sure the connection string for the data source does not contain **column encryption setting=enabled** to ensure the data retrieved from encrypted columns remains encrypted. For more information, see [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md).)  
 -  
 -3.  Set the ALLOW_ENCRYPTED_VALUE_MODIFICATIONS option back to OFF. For example:  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
 -    ```  
 -  
 -## Potential for Data Corruption  
 - Improper use of this option can lead to data corruption. The **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** option allows the user to insert any data into encrypted columns in the database, including data that is encrypted with different keys, incorrectly encrypted, or not encrypted at all. If the user accidently copies the data that is not correctly encrypted using the encryption scheme (column encryption key, algorithm, encryption type) set up for the target column, you will not be able to decrypt the data (the data will be corrupted). This option must be used carefully, as it can lead to corrupting data in the database.  
 -  
 - The following scenario demonstrates how improperly importing data could lead to data corruption:  
 -  
 -1.  The option is set to ON for a user.  
 -  
 -2.  The user runs the application that connects to the database. The application uses bulk APIs to insert plain text values to encrypted columns. The application expects an Always Encrypted-enabled client driver to encrypt the data on insert. However, the application is misconfigured, so that either it ends up using a driver that does not support Always Encrypted or the connection string does not contain **column encryption setting=enabled**.  
 -  
 -3.  The application sends plaintext values to the server. As cryptographic metadata checks are disabled in the server for the user, the server lets the incorrect data (plaintext instead of correctly encrypted ciphertext) to be inserted into an encrypted column.  
 -  
 -4.  The same or another application connects to the database using an Always Encrypted-enabled driver and with **column encryption setting=enabled** in the connection string, and retrieves the data. The application expects the data to be transparently decrypted. However, the driver fails to decrypt the data because the data is incorrect ciphertext.  
 -  
 -## Best practice  
 -  
 --   Use designated user accounts for long running workloads using this option.  
 -  
 --   For short running bulk copy applications or tools that need to move encrypted data without decrypting it, set the option to ON immediately before running the application and set it back to OFF immediately after running the operation.  
 -  
 --   Do not use this option for developing new applications. Instead, use a client driver (such as  ADO 4.6.1) that offers an API for suppressing cryptographic metadata checks for a single session.  
 -  
 -## See Also  
 - [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
 - [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
 - [Always Encrypted &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Always Encrypted Wizard](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
 - [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  

