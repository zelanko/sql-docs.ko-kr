---
title: Azure에 대 한 관리 되는 백업 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab44323dfabd389113351e413751b7a230c176e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70175758"
---
# <a name="sql-server-managed--backup-to-azure"></a>Azure에 대 한 관리 되는 백업 SQL Server
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]Azure Blob storage 서비스에 대 한 SQL Server 백업을 관리 하 고 자동화 합니다. 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 사용하는 백업 전략은 데이터베이스의 트랜잭션 작업과 보존 기간을 기반으로 합니다. 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 지정한 보존 기간 동안 지정 시간 복원을 지원합니다.   

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]은 SQL Server 인스턴스의 모든 데이터베이스를 관리하기 위해 인스턴스 수준이나 데이터베이스 수준에서 사용하도록 설정할 수 있습니다. SQL Server은 온-프레미스 또는 Azure 가상 머신과 같은 호스팅된 환경에서 실행 될 수 있습니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]는 Azure Virtual Machines에서 실행 되는 SQL Server에 권장 됩니다.  
  
## <a name="benefits-of-automating-sql-server-backup-using-includess_smartbackupincludesss-smartbackup-mdmd"></a>
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용한 SQL Server 백업 자동화의 이점  
  
-   현재 여러 데이터베이스에 대한 백업을 자동화하려면 백업 전략 개발, 사용자 지정 코드 작성, 백업 예약 등이 필요하지만, 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하는 경우에는 보존 기간 설정과 스토리지 위치만 제공하면 됩니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]백업을 예약, 수행 및 유지 관리 합니다.  
  
     
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]은 데이터베이스 수준에서 구성하거나 SQL Server 인스턴스의 기본 설정으로 구성할 수 있습니다. 를 사용 하 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 여 백업을 자동화 하면 다음과 같은 이점이 있습니다.  
  
    -   인스턴스 수준에서 기본값을 설정하면 이후 만들어진 모든 데이터베이스에 이러한 설정을 적용할 수 있으므로 새 데이터베이스가 백업되지 않고 데이터가 손실될 위험을 제거할 수 있습니다.  
  
    -   데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하도록 설정하고 보존 기간을 설정하면 인스턴스 수준에서 설정한 기본 설정을 재정의할 수 있습니다. 이렇게 하면 특정 데이터베이스에 대한 복구 가능성을 더욱 세부적으로 제어할 수 있습니다.  
  
-   
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하는 경우 데이터베이스 백업 주기 또는 유형을 지정할 필요가 없습니다.  보존 기간을 지정 하 고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 데이터베이스에 대 한 백업 유형과 빈도를 결정 하 여 Azure Blob 저장소 서비스에 백업을 저장 합니다. 에서 백업 전략을 만드는 데 사용 하는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 조건 집합에 대 한 자세한 내용은이 항목의 [구성 요소 및 개념](#Concepts) 섹션을 참조 하십시오.  
  
-   암호화를 사용하도록 구성된 경우 백업 데이터에 대한 추가 보안이 적용됩니다. 자세한 내용은 [백업 암호화](backup-encryption.md) 를 참조 하세요.  
  
 백업에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure Blob storage를 사용 하는 이점에 대 한 자세한 내용은 [Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 를 참조 하세요.  
  
## <a name="terms-and-definitions"></a>용어 및 정의  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 데이터베이스 백업을 자동화하고 보존 기간에 따라 백업을 관리하는 SQL Server 기능입니다.  
  
 재방문 주기 기간  
 보존 기간은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 지정한 기간 내 지정 시간에 데이터베이스를 복구하도록 스토리지에 보존할 백업 파일을 결정하는 데 사용됩니다.  지원되는 값 범위는 1-30일입니다.  
  
 로그 체인  
 로그 백업의 연속된 시퀀스를 로그 체인이라고 합니다. 로그 체인은 데이터베이스의 전체 백업으로 시작합니다.  
  
##  <a name="Concepts"></a>요구 사항, 개념 및 구성 요소  
  
  
###  <a name="Security"></a> 권한  
 Transact-SQL은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 구성 및 모니터링하는 데 사용되는 주 인터페이스입니다. 일반적으로 구성 저장 프로시저를 실행 하려면 **ALTER ANY CREDENTIAL** 권한이 있는 데이터베이스 역할 `EXECUTE` **db_backupoperator** 하 고 **sp_delete_backuphistory** 저장 프로시저에 대 한 사용 권한이 필요 합니다.  일반적으로 정보를 검토하는 데 사용되는 저장 프로시저 및 함수는 저장 프로시저에 대한 `Execute` 사용 권한과 함수에 대한 `Select` 사용 권한이 각각 필요합니다.  
  
###  <a name="Prereqs"></a> 필수 조건  
 **사전**  
  
 **Azure Storage 서비스** 는에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 백업 파일을 저장 하는 데 사용 됩니다.    Azure storage 계정을 만들기 위한 개념, 구조 및 요구 사항은 **URL에 백업 SQL Server** 항목의 [주요 구성 요소 및 개념 소개](sql-server-backup-to-url.md#intorkeyconcepts) 섹션에 자세히 설명 되어 있습니다.  
  
 **SQL 자격 증명** 은 Azure 저장소 계정에 인증 하는 데 필요한 정보를 저장 하는 데 사용 됩니다. SQL 자격 증명 개체는 계정 이름 및 액세스 키 정보를 저장합니다. 자세한 내용은 URL에 대 한 **SQL Server 백업** 항목의 [주요 구성 요소 및 개념 소개](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 섹션을 참조 하세요. Azure Storage 인증 정보를 저장 하는 SQL 자격 증명을 만드는 방법에 대 한 연습은 [2 단원: SQL Server 자격 증명 만들기](../../tutorials/lesson-2-create-a-sql-server-credential.md)를 참조 하세요.  
  
###  <a name="Concepts_Components"></a>개념 및 주요 구성 요소  
 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]은 백업 작업을 관리하는 기능입니다. **Msdb** 데이터베이스에 메타 데이터를 저장 하 고 시스템 작업을 사용 하 여 전체 데이터베이스 및 트랜잭션 로그 백업을 작성 합니다.  
  
#### <a name="components"></a>구성 요소  
 Transact-SQL은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 상호 작용하는 주 인터페이스입니다. 시스템 저장 프로시저는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하도록 설정하고 구성 및 모니터링하는 데 사용됩니다. 시스템 함수는 기존 구성 설정, 매개 변수 값 및 백업 파일 정보를 검색하는 데 사용됩니다. 확장 이벤트는 오류 및 경고를 노출하는 데 사용됩니다. 경고 메커니즘은 SQL 에이전트 작업 및 SQL Server 정책 기반의 관리를 통해 설정됩니다 다음은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 관련된 개체와 해당 기능에 대한 설명 목록입니다.  
  
 PowerShell cmdlet도 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 구성하는 데 사용할 수 있습니다. SQL Server Management Studio는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 **데이터베이스 복원** 태스크를 사용하여 만든 백업 복원을 지원합니다.  
  
|||  
|-|-|  
|시스템 개체|Description|  
|**데이터베이스가**|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 만든 모든 백업에 대한 메타데이터, 백업 기록을 저장합니다.|  
|[smart_admin. set_db_backup &#40;Transact-sql&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정 및 구성하기 위한 시스템 저장 프로시저입니다.|  
|[smart_admin. set_instance_backup &#40;Transact-sql&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|SQL Server 인스턴스에 대 한 기본 설정을 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 사용 하도록 설정 하 고 구성 하기 위한 시스템 저장 프로시저입니다.|  
|[smart_admin sp_ backup_master_switch &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 일시 중지 및 재개하는 시스템 저장 프로시저입니다.|  
|[smart_admin. sp_set_parameter &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 대한 모니터링을 설정 및 구성하는 시스템 저장 프로시저입니다. 예제: 알림을 위한 메일 설정, 확장 이벤트 설정입니다.|  
|[smart_admin. sp_backup_on_demand &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|로그 체인을 중단 하지 않고를 사용 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 하도록 설정 된 데이터베이스에 대 한 임시 백업을 수행 하는 데 사용 되는 시스템 저장 프로시저입니다.|  
|[smart_admin. fn_backup_db_config &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|데이터베이스 또는 인스턴스의 모든 데이터베이스에 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 대 한 현재 상태 및 구성 값을 반환 하는 시스템 함수입니다.|  
|[smart_admin. fn_is_master_switch_on &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|마스터 스위치의 상태를 반환하는 시스템 함수입니다.|  
|[smart_admin. sp_get_backup_diagnostics &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|확장 이벤트가 기록한 이벤트를 반환하는 데 사용되는 시스템 저장 프로시저입니다.|  
|[smart_admin. fn_get_parameter &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|경고의 메일 설정 및 모니터링 등 백업 시스템 설정의 현재 값을 반환하는 시스템 함수입니다.|  
|[smart_admin. fn_available_backups &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|지정한 데이터베이스 또는 인스턴스의 모든 데이터베이스에 대해 사용 가능한 백업을 검색하는 데 사용되는 저장 프로시저입니다.|  
|[smart_admin. fn_get_current_xevent_settings &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|현재 확장 이벤트 설정을 반환하는 시스템 함수입니다.|  
|[smart_admin. fn_get_health_status &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|지정한 기간 동안 확장 이벤트에서 기록한 집계된 오류 수를 반환하는 시스템 함수입니다.|  
|[Azure에 SQL Server 관리 백업 모니터링](sql-server-managed-backup-to-microsoft-azure.md)|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]의 모니터링, 오류 및 경고의 전자 메일 알림, SQL Server 정책 기반 관리에 대한 확장 이벤트입니다.|  
  
#### <a name="backup-strategy"></a>백업 전략  
 **에서 사용 하 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]는 백업 전략:**  
  
 예약된 백업 유형 및 백업 주기는 데이터베이스 작업을 기준으로 결정됩니다. 보존 기간 설정은 보존 기간 내 지정 시간에 데이터베이스를 복구하는 기능과 스토리지에 보존할 백업 파일의 시간을 결정하는 데 사용됩니다.  
  
 **백업 컨테이너 및 파일 이름 지정 규칙**  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]가용성 데이터베이스를 제외한 모든 데이터베이스에 대 한 SQL Server 인스턴스 이름을 사용 하 여 Azure storage 컨테이너의 이름을로 제공 합니다.  가용성 데이터베이스의 경우 가용성 그룹 GUID를 사용 하 여 Azure storage 컨테이너의 이름을 제공 합니다.  
  
 가용성이 아닌 데이터베이스의 백업 파일은 다음 규칙을 사용 하 여 명명 됩니다. 데이터베이스 이름의 첫 40 문자, '-'를 제외한 데이터베이스 GUID 및 타임 스탬프를 사용 하 여 이름이 만들어집니다. 밑줄 문자는 구분 기호로 세그먼트 사이에 삽입됩니다. 
  **.bak** 파일 확장명은 전체 백업에 사용되고 **.log** 파일 확장명은 로그 백업에 사용됩니다. 가용성 그룹 데이터베이스의 경우 위에서 설명한 파일 명명 규칙 외에도 가용성 그룹 데이터베이스 GUID가 40자의 데이터베이스 이름 뒤에 추가됩니다. 가용성 그룹 데이터베이스 GUID 값은 sys.databases의 group_database_id 값입니다.  
  
 **전체 데이터베이스 백업:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에이전트는 다음 조건 중 하나라도 해당 되는 경우 전체 데이터베이스 백업을 예약 합니다.  
  
-   데이터베이스에 처음으로 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정되거나 인스턴스 수준에서 기본 설정과 함께 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 설정된 경우  
  
-   마지막 전체 데이터베이스 백업 이후 증가한 로그가 1GB 이상인 경우  
  
-   마지막 전체 데이터베이스 백업 이후 최대 시간 간격인 일주일이 지난 경우  
  
-   로그 체인이 끊어진 경우. 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 주기적으로 백업 파일의 첫 번째 LSN과 마지막 LSN을 비교하여 로그 체인의 변경 여부를 확인합니다. 이유에 관계없이 로그 체인이 끊어진 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 전체 데이터베이스 백업을 예약합니다. 로그 체인이 끊어지는 가장 일반적인 이유는 Transact-SQL을 사용하거나 SQL Server Management Studio의 백업 태스크를 통해 실행되는 백업 명령 때문입니다.  그 외에 실수로 백업 로그 파일을 삭제하거나 백업을 덮어쓰는 경우가 있을 수 있습니다.  
  
 **트랜잭션 로그 백업:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 다음 조건에 해당 하는 경우 로그 백업을 예약 합니다.  
  
-   로그 백업 기록을 찾을 수 없는 경우. 이는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이 처음으로 설정된 경우 발생합니다.  
  
-   사용된 트랜잭션 로그 공간이 5MB 이상인 경우  
  
-   마지막 로그 백업 후 최대 시간 간격인 2시간이 경과한 경우  
  
-   트랜잭션 로그 백업이 전체 데이터베이스 백업보다 뒤처지는 경우. 목표는 로그 체인이 전체 백업을 앞서도록 유지하는 것입니다.  
  
#### <a name="retention-period-settings"></a>보존 기간 설정  
 백업을 사용하도록 설정할 때는 일 단위로 보존 기간을 설정해야 합니다. 최소 1일, 최대 30일입니다.  
  
 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 지정한 시간 내 지정 시간에 복구하는 기능을 평가하여 보존해야 할 백업 파일과 삭제할 백업 파일을 결정합니다. 백업의 backup_finish_date는 보존 기간 설정에서 지정한 시간을 확인하고 일치시키는 데 사용됩니다.  
  
#### <a name="important-considerations"></a>중요 고려 사항  
 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 작업에 대한 영향을 이해하는 데 중요한 고려 사항은 다음과 같습니다.  
  
-   특정 데이터베이스의 경우 기존의 전체 데이터베이스 백업 작업이 실행 중이면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 는 현재 작업이 완료될 때까지 기다린 다음 동일한 데이터베이스에 대해 다른 전체 데이터베이스 백업을 수행합니다. 마찬가지로 한 번에 한 트랜잭션 로그 백업만 실행할 수 있습니다. 그러나 전체 데이터베이스 백업 및 트랜잭션 로그 백업은 동시에 실행할 수 있습니다. 실패는 확장 이벤트로 기록됩니다.  
  
-   10개 이상의 전체 데이터베이스 백업이 동시에 예약된 경우 확장 이벤트의 디버그 채널을 통해 경고가 발생합니다. 
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 은 백업이 필요한 나머지 데이터베이스의 우선 순위 큐를 관리합니다.  
  
###  <a name="support_limits"></a> 지원 제한 사항  
 다음은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에만 적용되는 제한 사항입니다.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에이전트는 데이터베이스 백업만 지원 합니다 (전체 및 로그 백업).  파일 백업 자동화는 지원되지 않습니다.  
  
-   
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 작업은 현재 Transact-SQL을 통해 지원됩니다. 모니터링 및 문제 해결은 확장 이벤트를 사용하여 수행됩니다. PowerShell 및 SMO 지원은 SQL Server 인스턴스의 보존 기간 기본 설정 및 스토리지 구성, 그리고 SQL Server 정책 기반 관리 정책을 기반으로 한 백업 상태 및 전체 상태 모니터링으로 제한됩니다.  
  
-   시스템 데이터베이스는 지원되지 않습니다.  
  
-   Azure Blob Storage service는 유일 하 게 지원 되는 백업 저장소 옵션입니다. 디스크 또는 테이프 백업은 지원되지 않습니다.  
  
-   현재 Azure Storage의 페이지 Blob에 허용 되는 최대 파일 크기는 1TB입니다. 1TB보다 큰 백업 파일은 실패합니다. 이러한 상황을 방지하려면 데이터베이스 크기가 큰 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 설정하기 전에 압축을 사용하고 백업 파일 크기를 테스트하는 것이 좋습니다. 로컬 디스크에 백업 하거나 Transact-sql 문을 사용 하 `BACKUP TO URL` 여 Azure 저장소에 수동으로 백업 하 여 테스트할 수 있습니다. 자세한 내용은 [URL에 대한 SQL Server Backup](sql-server-backup-to-url.md)을 참조하세요.  
  
-   복구 모델: 전체 또는 대량 로그 모델로 설정 된 데이터베이스만 지원 됩니다.  단순 복구 모델로 설정된 데이터베이스는 지원되지 않습니다.  
  
-   
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 을 구성한 경우 일부 제한 사항이 있을 수 있습니다. 자세한 내용은 [Azure에 대 한 관리 되는 백업 SQL Server: 상호 운용성 및 공존 성](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)을 참조 하세요.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
|||  
|-|-|  
|**작업 설명**|**항목**|  
|데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성, 인스턴스 수준에서 기본 설정 구성, 인스턴스 또는 데이터베이스 수준에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 해제, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 일시 중지 및 다시 시작 등의 기본 태스크|[Azure에 SQL Server 관리 백업 - 보존 및 스토리지 설정](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**자습서:** 구성 및 모니터링 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에 대 한 단계별 지침입니다.|[Azure에 SQL Server 관리 백업 설정](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**자습서:** 가용성 그룹의 데이터베이스를 구성 하 고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 모니터링 하기 위한 단계별 지침을 제공 합니다.|[가용성 그룹의 Azure에 SQL Server 관리 백업 설정](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 모니터링과 관련된 도구, 개념 및 태스크|[Azure에 SQL Server 관리 백업 모니터링](sql-server-managed-backup-to-microsoft-azure.md)|  
|
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 문제 해결 도구 및 단계|[Azure에 SQL Server 관리 백업 문제 해결](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [URL에 백업 SQL Server](sql-server-backup-to-url.md)   
 [Azure에 대 한 관리 되는 백업 SQL Server: 상호 운용성 및 공존 성](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [Azure에 SQL Server 관리 백업 문제 해결](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
