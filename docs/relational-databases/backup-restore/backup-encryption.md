---
title: "백업 암호화 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 334b95a8-6061-4fe0-9e34-b32c9f1706ce
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 30654c4f7950f188cf08608cf946f4fe42e6d3e4
ms.lasthandoff: 04/11/2017

---
# <a name="backup-encryption"></a>백업 암호화
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업의 암호화 옵션에 대해 간략하게 설명합니다. 여기에서는 백업 중의 암호화에 대한 사용법, 이점 및 권장 방법을 살펴봅니다.  
  
  
##  <a name="Overview"></a> 개요  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 SQL Server에는 백업을 만드는 동안 데이터를 암호화하는 기능이 포함됩니다. 백업을 만들 때 암호화 알고리즘과 암호기(인증서 또는 비대칭 키)를 지정하여 암호화된 백업 파일을 만들 수 있습니다. 모든 저장소 대상, 즉 온-프레미스 및 Window Azure Storage가 지원됩니다. 또한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 도입된 새로운 기능인 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]작업에 대해 암호화 옵션을 구성할 수 있습니다.  
  
 백업 중에 암호화하려면 암호화 키를 보호할 암호기와 암호화 알고리즘을 지정해야 합니다. 지원되는 암호화 옵션은 다음과 같습니다.  
  
-   **암호화 알고리즘:** 지원되는 암호화 알고리즘은 AES 128, AES 192, AES 256, Triple DES입니다.  
  
-   **암호기:** 인증서 또는 비대칭 키입니다.  
  
> [!CAUTION]  
>  인증서나 비대칭 키를 백업하는 것이 매우 중요하며, 이때 가급적이면 인증서나 비대칭 키를 사용하여 암호화한 백업 파일과 다른 위치에 백업하는 것이 좋습니다. 인증서나 비대칭 키가 없으면 백업을 복원할 수 없으므로 백업 파일을 사용할 수 없게 됩니다.  
  
 **암호화된 백업 복원:** SQL Server 복원에서는 복원 중에 암호화 매개 변수를 지정할 필요가 없습니다. 또한 복원할 대상 인스턴스에서 백업 파일을 암호화하는 데 사용된 인증서나 비대칭 키를 사용할 수 없어도 됩니다. 복원을 수행하는 사용자 계정에는 인증서나 키에 대한 **VIEW DEFINITION** 권한이 있어야 합니다. 암호화된 백업을 다른 인스턴스로 복원하는 경우 해당 인스턴스에서 인증서를 사용할 수 있는지 확인해야 합니다.  
  
 TDE로 암호화된 데이터베이스에서 백업을 복원하는 경우에는 복원할 대상 인스턴스에서 TDE 인증서를 사용할 수 있어야 합니다.  
  
##  <a name="Benefits"></a> 이점  
  
1.  데이터베이스 백업을 암호화하면 데이터를 보호할 수 있습니다. SQL Server는 백업을 만드는 동안 백업 데이터를 암호화하는 옵션을 제공합니다.  
  
2.  TDE를 사용하여 암호화된 데이터베이스에도 암호화를 사용할 수 있습니다.  
  
3.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]으로 수행된 백업에 대한 암호화가 지원되며, 이를 통해 오프사이트 백업의 보안이 강화됩니다.  
  
4.  이 기능은 AES 256비트까지 여러 암호화 알고리즘을 지원하므로 사용자의 요구 사항에 적합한 알고리즘을 선택할 수 있습니다.  
  
5.  EKM(확장 키 관리) 공급자와 암호화 키를 통합할 수 있습니다.  
  
  
##  <a name="Prerequisites"></a> 필수 구성 요소  
 백업을 암호화하기 위한 사전 요구 사항은 다음과 같습니다.  
  
1.  **master 데이터베이스용 데이터베이스 마스터 키 만들기:** 데이터베이스 마스터 키는 데이터베이스에 있는 비대칭 키와 인증서의 개인 키를 보호하는 데 사용되는 대칭 키입니다. 자세한 내용은 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)를 참조하세요.  
  
2.  백업 암호화에 사용할 인증서나 비대칭 키를 만듭니다. 인증서를 만드는 방법은 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)를 참조하세요. 비대칭 키를 만드는 방법은 [CREATE ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  EKM(확장 키 관리)에 있는 비대칭 키만 지원됩니다.  
  
##  <a name="Restrictions"></a> 제한 사항  
 암호화 옵션에 적용되는 제한 사항은 다음과 같습니다.  
  
-   비대칭 키를 사용하여 백업 데이터를 암호화하는 경우 EKM 공급자에 있는 비대칭 키만 지원됩니다.  
  
-   SQL Server Express와 SQL Server Web은 백업 중에 암호화를 지원하지 않습니다. 그러나 암호화된 백업을 SQL Server Express 또는 SQL Server Web의 인스턴스로 복원할 수는 있습니다.  
  
-   이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 암호화된 백업을 읽을 수 없습니다.  
  
-   암호화된 백업의 경우 기존 백업 세트 옵션에 추가는 지원되지 않습니다.  
  
  
##  <a name="Permissions"></a> 사용 권한  
 **백업을 암호화하거나 암호화된 백업에서 복원하려면:**  
  
 데이터베이스 백업을 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한**VIEW DEFINITION** 권한을 사용합니다.  
  
> [!NOTE]  
>  TDE 인증서에 대한 액세스 권한은 TDE로 보호되는 데이터베이스를 백업하거나 복원하는 데 필요하지 않습니다.  
  
##  <a name="Methods"></a> 백업 암호화 방법  
 아래의 섹션들에서는 백업 중에 데이터를 암호화하는 단계를 간략하게 소개합니다. Transact-SQL을 사용하여 백업을 암호화하는 다른 단계에 대한 전체 연습은 [암호화된 백업 만들기](../../relational-databases/backup-restore/create-an-encrypted-backup.md)를 참조하세요.  
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용  
 다음 대화 상자에서 데이터베이스의 백업을 만들 때 백업을 암호화할 수 있습니다.  
  
1.  [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md) **백업 옵션** 페이지에서 **암호화**를 선택하고 암호화 알고리즘과 암호화에 사용할 인증서 또는 비대칭 키를 지정할 수 있습니다.  
  
2.  [유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure) 백업 태스크를 선택할 때 **백업 태스크 정의** 페이지의 **옵션** 탭에서 **백업 암호화**를 선택하고 암호화 알고리즘과 암호화에 사용할 인증서 또는 키를 지정할 수 있습니다.  
  
### <a name="using-transact-sql"></a>Transact-SQL 사용  
 다음은 백업 파일을 암호화하는 예제 Transact-SQL 문입니다.  
  
```  
BACKUP DATABASE [MYTestDB]  
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
  
```  
  
 전체 Transact-SQL 문 구문은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
### <a name="using-powershell"></a>PowerShell 사용  
 이 예제에서는 암호화 옵션을 만든 다음 **Backup-SqlDatabase** cmdlet에서 매개 변수 값으로 사용하여 암호화된 백업을 만듭니다.  
  
```  
C:\PS>$encryptionOption = New-SqlBackupEncryptionOption -Algorithm Aes256 -EncryptorType ServerCertificate -EncryptorName "BackupCert"  
```  
  
```  
C:\PS>Backup-SqlDatabase -ServerInstance . -Database "MyTestDB" -BackupFile "MyTestDB.bak" -CompressionOption On -EncryptionOption $encryptionOption  
```  
  
##  <a name="RecommendedPractices"></a> 권장 방법  
 암호화 인증서 및 키의 백업을 인스턴스가 설치된 로컬 컴퓨터 이외의 위치에 만듭니다. 재해 복구 시나리오를 고려하여 인증서 또는 키의 백업을 오프사이트 위치에 저장하는 것이 좋습니다. 암호화된 백업은 해당 백업을 암호화하는 데 사용된 인증서 없이 복원할 수 없습니다.  
  
 암호화된 백업을 복원하려면 일치하는 지문을 사용하여 백업을 만들 때 사용된 원래 인증서가 복원할 대상 인스턴스에서 사용 가능해야 합니다. 따라서 인증서가 만료 시 갱신되거나 어떤 식으로든 변경되면 안 됩니다. 갱신하면 인증서가 업데이트되어 지문 변경이 트리거될 수 있으므로 백업 파일에 인증서를 사용할 수 없게 됩니다. 복원을 수행하는 계정에는 백업 중에 암호화하는 데 사용된 인증서나 비대칭 키에 대한 VIEW DEFINITION 권한이 있어야 합니다.  
  
 가용성 그룹 데이터베이스 백업은 기본 백업 복제본에서 일반적으로 수행됩니다.  백업이 수행된 복제본이 아닌 복제본에서 백업을 복원하는 경우 백업에 사용된 원래 인증서가 복원할 복제본에서 사용 가능한지 확인해야 합니다.  
  
 데이터베이스에서 TDE를 사용하도록 설정된 경우 데이터베이스와 백업을 암호화하기 위해 다른 인증서 또는 비대칭 키를 선택하여 보안을 강화합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
|항목/태스크|설명|  
|-----------------|-----------------|  
|[암호화된 백업 만들기](../../relational-databases/backup-restore/create-an-encrypted-backup.md)|암호화된 백업을 만드는 데 필요한 기본 단계에 대해 설명합니다.|  
|[Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)|Azure 키 자격 증명 모음에서 키로 보호하는 암호화된 백업을 만드는 예제를 제공합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
