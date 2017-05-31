---
title: "복원 및 복구 개요(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring tables [SQL Server]
- backups [SQL Server], restore scenarios
- database backups [SQL Server], restore scenarios
- database restores [SQL Server]
- restoring [SQL Server]
- restores [SQL Server]
- table restores [SQL Server]
- restoring databases [SQL Server], about restoring databases
- database restores [SQL Server], scenarios
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
caps.latest.revision: 46
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e04261e1d43b3ca49c1c3d005d7c3ef683964ce
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="restore-and-recovery-overview-sql-server"></a>복원 및 복구 개요(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 오류를 복구하려면 데이터베이스 관리자는 논리적으로 올바르고 의미 있는 복원 시퀀스로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 집합을 복원해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복원 및 복구에서는 다음과 같이 전체 데이터베이스, 데이터 파일 또는 데이터 페이지 백업으로부터의 데이터 복원을 지원합니다.  
  
-   데이터베이스( *전체 데이터베이스 복원*)  
  
     전체 데이터베이스가 복원 및 복구되며 복원 및 복구 작업 기간 동안 데이터베이스는 오프라인 상태가 됩니다.  
  
-   데이터 파일( *파일 복원*)  
  
     데이터 파일 또는 파일 집합이 복원 및 복구됩니다. 해당 파일을 포함한 파일 그룹은 복원 기간 동안 자동으로 오프라인 상태가 됩니다. 오프라인 파일 그룹에 액세스하려고 하면 오류가 발생합니다.  
  
-   데이터 페이지( *페이지 복원*)  
  
     전체 복구 모델 또는 대량 로그 복구 모델에서 개별 데이터베이스를 복원할 수 있습니다. 페이지 복원은 파일 그룹의 수에 관계없이 모든 데이터베이스에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원은 지원되는 모든 운영 체제에서 작동합니다. 지원되는 운영 체제에 대한 자세한 내용은 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요. 이전 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 백업 지원에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)의 "호환성 지원" 섹션을 참조하세요.  
  
 **항목 내용**  
  
-   [복원 시나리오 개요](#RestoreScenariosOv)  
  
-   [복구 모델 및 지원되는 복원 작업](#RMsAndSupportedRestoreOps)  
  
-   [단순 복구 모델에서의 복원 제한 사항](#RMsimpleScenarios)  
  
-   [대량 로그 복구 모델에서 복원](#RMblogRestore)  
  
-   [데이터베이스 복구 관리자(SQL Server Management Studio)](#DRA)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="RestoreScenariosOv"></a> 복원 시나리오 개요  
 *의* 복원 시나리오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 하나 이상의 백업에서 데이터를 복원한 다음 데이터베이스를 복구하는 프로세스입니다. 지원되는 복원 시나리오는 데이터베이스의 복구 모델 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 따라 달라집니다.  
  
 다음 표에서는 복구 모델별로 지원되는 복원 시나리오에 대해 설명합니다.  
  
|의|단순 복구 모델의 경우|전체/대량 로그 복구 모델의 경우|  
|----------------------|---------------------------------|----------------------------------------------|  
|전체 데이터베이스 복원|이 전략이 기본 복원 전략입니다. 전체 데이터베이스 복원은 단순히 전체 데이터베이스 백업을 복원 및 복구하거나 전체 데이터베이스 백업을 복원한 다음 차등 백업을 복원 및 복구합니다.<br /><br /> 자세한 내용은 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)을 참조하세요.|이 전략이 기본 복원 전략입니다. 전체 데이터베이스 복원은 전체 데이터베이스 백업 및 필요에 따라 차등 백업(있는 경우)을 복원한 후 모든 후속 로그 백업을 순서대로 복원합니다. 전체 데이터베이스 복원은 마지막 로그 백업을 복구 및 복원함으로써 완료됩니다(RESTORE WITH RECOVERY).<br /><br /> 자세한 내용은 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)을 참조하세요.|  
|File restore **\***|전체 데이터베이스를 복원하지 않고 하나 이상의 손상된 읽기 전용 파일을 복원합니다. 파일 복원은 데이터베이스에 적어도 하나 이상의 읽기 전용 파일 그룹이 있는 경우에만 사용할 수 있습니다.|전체 데이터베이스를 복원하지 않고 하나 이상의 파일을 복원합니다. 파일 복원은 데이터베이스가 오프라인 상태일 때 수행할 수 있으며 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 데이터베이스가 여전히 온라인 상태일 때에도 수행할 수 있습니다. 파일을 복원하는 동안 복원되는 파일을 포함하는 파일 그룹은 항상 오프라인 상태입니다.|  
|페이지 복원|해당 사항 없음|하나 이상의 손상된 페이지를 복원합니다. 페이지 복원은 데이터베이스가 오프라인 상태일 때 수행할 수 있으며 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 데이터베이스가 여전히 온라인 상태일 때에도 수행할 수 있습니다. 페이지를 복원하는 동안 복원되는 페이지는 항상 오프라인 상태입니다.<br /><br /> 손상되지 않은 로그 백업 체인은 현재 로그 파일을 포함하여 모두 사용할 수 있어야 하며 페이지가 현재 로그 파일 상태로 업데이트되도록 모두 적용되어야 합니다.<br /><br /> 자세한 내용은 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)을 참조하세요.|  
|증분 복원 **\***|파일 그룹 수준의 주 파일 그룹에서 시작하여 읽기/쓰기가 가능한 모든 파일 그룹, 보조 파일 그룹순으로 단계별로 데이터베이스를 복원 및 복구합니다.|파일 그룹 수준에서 주 파일 그룹에서 시작하여 단계별로 데이터베이스를 복원 및 복구합니다.|  
  
 **\*** 온라인 복원은 엔터프라이즈 버전에서만 지원됩니다.  
  
 데이터 복원 방식과 관계없이 데이터베이스가 복구되기 전에 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 전체 데이터베이스가 논리적으로 일치하도록 해야 합니다. 예를 들어 파일을 복원할 경우 데이터베이스와 일치하도록 충분히 롤포워드해야 파일을 복구하고 온라인 상태로 만들 수 있습니다.  
  
### <a name="advantages-of-a-file-or-page-restore"></a>파일 또는 페이지 복원의 이점  
 전체 데이터베이스 대신 파일이나 페이지를 복원 및 복구하면 다음과 같은 이점이 있습니다.  
  
-   복원하는 데이터가 적어 데이터를 복사하고 복구하는 데 필요한 시간이 줄어듭니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 파일 또는 페이지를 복원하면 복원 작업을 수행하는 동안 데이터베이스에 있는 다른 데이터가 온라인 상태를 유지할 수 있습니다.  
  
##  <a name="RMsAndSupportedRestoreOps"></a> 복구 모델 및 지원되는 복원 작업  
 데이터베이스에서 사용할 수 있는 복원 작업은 복구 모델에 따라 다릅니다. 다음 표에서는 각 복구 모델이 지정된 복원 시나리오를 지원하는지, 또 지원하면 어느 범위까지 지원하는지 요약합니다.  
  
|복원 작업|전체 복구 모델|대량 로그 복구 모델|단순 복구 모델|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|데이터 복구|전체 복구합니다(로그를 사용 가능한 경우).|일부 데이터 손실이 노출됩니다.|마지막 전체 또는 차등 백업 이후의 데이터는 손실됩니다.|  
|지정 시간 복원|로그 백업 범위 내의 시간에서 복원합니다.|로그 백업이 대량 로그된 변경 내용을 포함한 경우 허용되지 않습니다.|지원되지 않습니다.|  
|File restore **\***|전체 지원됩니다.|경우에 따라 지원됩니다.**\*\***|읽기 전용 보조 파일에만 사용 가능합니다.|  
|Page restore **\***|전체 지원됩니다.|경우에 따라 지원됩니다.**\*\***|없음|  
|증분(파일 그룹 수준) 복원 **\***|전체 지원됩니다.|경우에 따라 지원됩니다.**\*\***|읽기 전용 보조 파일에만 사용 가능합니다.|  
  
 **\*** 엔터프라이즈 버전에서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** 필요한 조건은 이 항목의 뒷부분에 나오는 [단순 복구 모델에서의 복원 제한 사항](#RMsimpleScenarios)을 참조하세요.  
  
> [!IMPORTANT]  
>  데이터베이스 복구 모델에 관계없이, 백업을 만든 버전보다 오래된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 복원할 수는 없습니다.  
  
##  <a name="RMsimpleScenarios"></a> 단순 복구 모델에서의 증분 시나리오  
 단순 복구 모델의 경우 복원 작업 시 다음과 같은 제한 사항이 있습니다.  
  
-   파일 복원과 증분 복원은 읽기 전용 보조 파일 그룹에만 사용할 수 있습니다. 이러한 복원 시나리오에 대한 자세한 내용은 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md) 및 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)을 참조하세요.  
  
-   페이지 복원은 허용되지 않습니다.  
  
-   지정 시간 복원은 허용되지 않습니다.  
  
 이러한 모든 제한 사항이 복구 요구에 적합하지 않을 경우 전체 복구 모델 사용을 고려하는 것이 좋습니다. 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  데이터베이스 복구 모델에 관계없이, 백업을 만든 버전보다 오래된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 복원할 수는 없습니다.  
  
##  <a name="RMblogRestore"></a> 대량 로그 복구 모델에서 복원  
 이 섹션에서는 전체 복구 모델을 보완하기 위한 용도로만 사용되는 대량 로그 복구 모델에 관련된 복원 고려 사항에 대해 설명합니다.  
  
> [!NOTE]  
>  대량 로그된 복구 모델에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
 일반적으로 대량 로그 복구 모델은 전체 복구 모델과 유사하며 전체 복구 모델에 설명된 정보는 두 모델에 모두 적용됩니다. 하지만 지정 시간 복구 및 온라인 복원은 대량 로그 복구 모델의 영향을 받습니다.  
  
### <a name="restrictions-for-point-in-time-recovery"></a>지정 시간 복구에 대한 제한 사항  
 대량 로그 복구 모델에서 수행된 로그 백업에 대량 로그 변경 내용이 포함되어 있는 경우 지정 시간 복구를 사용할 수 없습니다. 대량 변경 내용이 포함되어 있는 로그 백업에서 지정 시간 복구를 수행하면 복원 작업이 실패합니다.  
  
### <a name="restrictions-for-online-restore"></a>온라인 복원에 대한 제한 사항  
 온라인 복원 시퀀스는 다음 조건이 충족되는 경우에만 작동합니다.  
  
-   복원 시퀀스를 시작하기 전에 필요한 모든 로그 백업을 완료해야 합니다.  
  
-   온라인 복원 시퀀스를 시작하기 전에 대량 변경 내용의 백업을 완료해야 합니다.  
  
-   데이터베이스에 대량 변경 내용이 있는 경우 모든 파일이 온라인 상태이거나[존재하지 않는 상태](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)여야 합니다. 이는 더 이상 데이터베이스의 부분이 아니라는 의미입니다.  
  
 이러한 조건이 충족되지 않으면 온라인 복원 시퀀스가 실패합니다.  
  
> [!NOTE]  
>  온라인 복원을 시작하기 전에 전체 복구 모델로 전환하는 것이 좋습니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
 온라인 복원을 수행하는 방법은 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.  
  
##  <a name="DRA"></a> 데이터베이스 복구 관리자(SQL Server Management Studio)  
 데이터베이스 복구 관리자는 올바른 최적의 복원 시퀀스를 구현하는 복원 계획 생성을 용이하게 합니다. 알려진 데이터베이스 복원 문제와 고객이 요청한 개선 사항이 해결되었습니다. 데이터베이스 복구 관리자에 의해 도입되는 주요 개선 사항은 다음과 같습니다.  
  
-   **복원 계획 알고리즘:**  복원 계획 생성에 사용되는 알고리즘, 특히 복잡한 복원 시나리오가 크게 향상되었습니다. 지정 시간 복원의 분기 시나리오를 비롯한 여러 경계 사례가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서보다 효율적으로 처리됩니다.  
  
-   **지정 시간 복원:**  데이터베이스 복구 관리자를 사용하면 지정된 시간 내의 데이터베이스 복원이 훨씬 쉬워집니다. 시각적 백업 시간대에서 지정 시간 복원에 대한 지원이 크게 향상됩니다. 이 시각적 시간대를 사용하면 데이터베이스 복원의 대상 복원 시점으로 적합한 시점을 확인할 수 있습니다. 시간대는 분기 복구 경로(복구 분기를 연결하는 경로) 순회를 용이하게 합니다. 특정 지정 시간 복원 계획은 대상 지정 시간(날짜 및 시간)으로의 복원과 관련된 백업을 자동으로 포함합니다. 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
 데이터베이스 복구 관리자에 대한 자세한 내용은 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 효율성 블로그를 참조하십시오.  
  
-   [복구 관리자: 소개](http://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-an-introduction.aspx)  
  
-   [복구 관리자: SSMS를 사용하여 분할 백업 만들기/복원](http://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-using-ssms-to-create-restore-split-backups.aspx)  
  
##  <a name="RelatedContent"></a> 관련 내용  
 없음  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
