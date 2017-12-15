---
title: "데이터베이스 백업(백업 옵션 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
caps.latest.revision: "62"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f1d587759b7c57accdc4836346446e181f7df60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="back-up-database-backup-options-page"></a>데이터베이스 백업(백업 옵션 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **데이터베이스 백업** 대화 상자의 **백업 옵션** 페이지를 사용하여 데이터베이스 백업 옵션을 확인하거나 수정할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  데이터베이스 유지 관리 계획을 정의하여 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md) 및 [유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)][스크립트](../../t-sql/statements/backup-transact-sql.md) 단추를 클릭한 다음 스크립트에 대한 대상을 선택하여 해당되는 **BACKUP** 스크립트를 생성할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
### <a name="backup-set"></a>백업 세트  
 **백업 세트** 패널의 옵션을 사용하면 백업 작업으로 생성된 백업 세트에 대한 선택 가능한 정보를 지정할 수 있습니다.  
  
 **이름**  
 백업 세트 이름을 지정합니다. 데이터베이스 이름과 백업 유형에 따라 기본 이름이 자동으로 제안됩니다.  
  
 백업 세트에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
 **Description**  
 백업 세트에 대한 설명을 입력합니다.  
  
 **백업 세트 만료 기한**  
 다음 만료 옵션 중 하나를 선택합니다. **URL** 이 백업 대상으로 선택된 경우 이 옵션을 사용할 수 없습니다.  
  
|||  
|-|-|  
|**After**|만료되기 전에 이 백업 세트를 덮어쓰지 않고 보존할 일 수를 지정합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.<br /><br /> 백업 만료 기본값은 **백업 미디어 기본 보존 기간(일)** 옵션에 설정된 값입니다. 이 페이지에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음 **서버 속성** 대화 상자의 **데이터베이스 설정** 페이지를 클릭합니다.|  
|**위치**|백업 세트가 만료되어 덮어쓸 수 있는 특정 날짜를 지정합니다.|  
  
### <a name="compression"></a>압축  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (이상 버전)에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다.  
  
 **백업 압축 설정**  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (이상 버전)에서 다음 백업 압축 값 중 하나를 선택합니다.  
  
|||  
|-|-|  
|**기본 서버 설정 사용**|서버 수준 기본값을 사용하려면 클릭합니다.<br /><br /> 이 기본값은 **백업 압축 기본값** 서버 구성 옵션으로 설정됩니다. 이 옵션의 현재 설정을 확인하는 방법에 대한 자세한 내용은 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)을 참조하세요.|  
|**백업 압축**|서버 수준 기본값에 관계없이 백업을 압축하려면 클릭합니다.<br /><br /> **\*\* 중요 \*\*** 기본적으로 압축하면 CPU 사용량이 크게 늘어나고 압축 프로세스로 사용되는 추가 CPU는 동시 작업에 악영향을 줄 수 있습니다. 따라서 CPU 사용량이 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 자세한 내용은 이 항목 뒷부분의 [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다.|  
|**백업 압축 안 함**|서버 수준 기본값에 관계없이 압축되지 않은 백업을 만들려면 클릭합니다.|  
  
### <a name="encryption"></a>암호화  
 암호화된 백업을 만들려면 **백업 암호화** 확인란을 선택합니다. 암호화 단계에 사용할 암호화 알고리즘을 선택하고 기존 인증서 또는 비대칭 키 목록의 인증서 또는 비대칭 키를 제공합니다. 사용 가능한 암호화 알고리즘은 다음과 같습니다.  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
> [!TIP]  
>  기존 백업 세트에 추가하도록 선택한 경우 암호화 옵션을 사용할 수 없습니다.  
>   
>  인증서나 키를 백업하고 암호화한 백업과 다른 위치에 저장하는 것이 좋습니다.  
>   
>  EKM(Extensible Key Management)에 있는 키만 지원됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
