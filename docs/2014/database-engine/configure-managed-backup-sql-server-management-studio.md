---
title: 관리 되는 백업 (SQL Server Management Studio) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f8c9664baa2803bbab4282b6897d49f0ddb1831
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812710"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>관리되는 백업 구성(SQL Server Management Studio)
  **관리되는 백업** 대화에서는 인스턴스의 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본값을 구성할 수 있습니다. 이 항목에서는 이 대화를 사용하여인스턴스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 기본값을 구성하는 방법과, 이 때 고려해야 할 옵션에 대해 설명합니다. 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성할 때 이 설정은 이후 생성되는 모든 새 데이터베이스에 적용됩니다.  
  
 구성 하려는 경우 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 특정 데이터베이스에 대해서 [설정 및 구성 SQL Server Managed Backup to Windows Azure 데이터베이스에 대 한](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)합니다.  
 
> [!NOTE] 
> 프록시 서버에서 SQL Server Managed Backup이 지원되지 않습니다. 
  
## <a name="task-list"></a>작업 목록  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>SQL Server Management Studio에서 관리되는 백업 인터페이스를 사용하는 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 함수  
 이 릴리스에서는 **관리 백업** 인터페이스를 사용하여 인스턴스 수준 기본 설정을 구성할 수만 있습니다. 데이터베이스용 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하거나, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 작업을 일시 중지 또는 재개하거나, 이메일 알림을 설정할 수는 없습니다. **관리되는 백업** 인터페이스에서 현재 지원되지 않는 작업을 수행하는 방법은 [SQL Server Managed Backup to Windows Azure - Retention and Storage Settings](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **관리 되는 백업 노드 보기는 SQL Server Management Studio:** 보려는 **Managed Backup** 노드에서 **개체 탐색기**, 시스템 관리자 여야 합니다 또는 다음 사용 권한이 특별히 부여 사용자 계정:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` `smart_admin.fn_is_master_switch_on`합니다.  
  
-   `SELECT` `smart_admin.fn_backup_instance_config`합니다.  
  
 **관리되는 백업을 구성하려면:** SQL Server Management Studio에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하기 위해서는 시스템 관리자이거나 다음 권한이 있어야 합니다.  
  
 `db_backupoperator` 데이터베이스 역할의 멤버 자격, `ALTER ANY CREDENTIAL` 사용 권한 및 `sp_delete_backuphistory` 저장 프로시저의 `EXECUTE` 사용 권한.  
  
 `smart_admin.fn_get_current_xevent_settings` 함수에 대한 `SELECT` 사용 권한.  
  
 `EXECUTE` 에 대 한 권한을 `smart_admin.sp_get_backup_diagnostics` 저장 프로시저입니다. 또한 `VIEW SERVER STATE` 권한도 필요한데, 이 권한이 필요한 다른 시스템 개체를 내부적으로 호출하기 때문입니다.  
  
 `smart_admin.sp_set_instance_backup` 및 `smart_admin.sp_backup_master_switch`에서 `EXECUTE` 권한  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 구성  
 **개체 탐색기**에서 **관리** 노드를 확장하고 **관리되는 백업**을 마우스 오른쪽 단추로 클릭합니다. **구성**을 선택합니다. **관리되는 백업** 대화 상자가 열립니다.  
  
 **관리되는 백업 사용** 옵션을 선택하고 구성 값을 지정합니다.  
  
 **파일 보존** 기간은 일 단위로 지정하며 범위는 1~30입니다.  
  
 선택한 **SQL 자격 증명** 은 스토리지 계정과 일치해야 합니다. 현재 인증 정보를 저장하는 SQL 자격 증명이 없는 경우 **만들기**를 클릭하여 만들 수 있습니다. 또한 CREATE CREDENTIAL Transact-SQL 문을 사용해서 자격 증명을 만들고 SECRET 매개 변수의 ID와 액세스 키에 대해 스토리지 계정 이름을 제공할 수 있습니다. 자세한 내용은 [Create a Credential](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential)을 참조하세요.  
  
 Windows Azure 스토리지 계정에 대한 **스토리지 URL** , 이 스토리지 계정의 인증 정보를 저장하는 SQL 자격 증명과 백업 파일의 보존 기간을 지정합니다.  
  
 저장소 URL 형식은: https://\<StorageAccount >.blob.core.windows.net/  
  
 인스턴스 수준에서 암호화 설정을 지정하려면 **암호화 백업** 옵션을 선택하고 암호화에 사용할 알고리즘 및 인증서 또는 비대칭 키를 지정합니다.  이 항목은 인스턴스 수준에서 설정되어 이 구성 적용 후 생성되는 모든 새 데이터베이스에 사용됩니다.  
  
> [!WARNING]  
>  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]구성 없이 이 대화 상자를 사용하여 암호화 옵션을 지정할 수는 없습니다. 이러한 암호화 옵션은 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 작업에만 적용됩니다. 다른 백업 절차에 암호화를 사용하려면 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)를 참조하세요.  
  
### <a name="considerations"></a>고려 사항  
 인스턴스 수준에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성할 경우 이후 생성되는 모든 새 데이터베이스에 설정이 적용됩니다.  그러나 기존 데이터베이스가 자동으로 이 설정을 상속하지는 않습니다. 기존 데이터베이스에서 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 을 구성하려면 각 데이터베이스를 특정하게 구성해야 합니다. 자세한 내용은 [설정 및 구성 SQL Server Managed Backup to Windows Azure 데이터베이스에 대 한](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)합니다.  
  
 하는 경우 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 일시 중지 된를 사용 하 여는 `smart_admin.sp_backup_master_switch`, 경고가 나타납니다 구성을 완료 하려고 할 때 "관리 되는 백업이 비활성화 되었으며 현재 구성이 적용 되지 것입니다..." 메시지입니다. 사용 된 `smart_admin.sp_backup_master_switch` 저장 하 고 설정는 @new_state= 1입니다. 그러면 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 서비스가 재개되고 구성 설정이 적용됩니다. 저장된 프로시저에 대 한 자세한 내용은 참조 하세요. [smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Windows Azure에 SQL Server의 관리 되는 백업: 상호 운용성 및 공존 성](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
