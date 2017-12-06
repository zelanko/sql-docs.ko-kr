---
title: "Reporting Services 백업 및 복원 작업 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 90bad3a50068d2ba4f372a46ffcb3fc6cf6b8c22
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Reporting Services 백업 및 복원 작업

  이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에 사용되는 모든 데이터 파일에 대해 간략히 설명하고 이러한 파일을 백업하는 시기와 방법을 설명합니다. 보고서 서버 데이터베이스 파일에 대한 백업 및 복원 계획을 세우는 것이 복구 전략에서 가장 중요한 부분입니다. 그러나 복구 전략이 복잡할수록 보고서 암호화 키, 사용자 지정 어셈블리 또는 확장 프로그램, 구성 파일, 보고서 및 모델 원본 파일 등의 백업이 포함됩니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드  
  
 백업 및 복원 작업은 주로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 전체나 일부를 이동하는 데 사용됩니다.  
  
-   보고서 서버 데이터베이스만 이동하는 경우에는 백업 후 복원이나 분리 후 연결 방법으로 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스를 재배치할 수 있습니다. 자세한 내용은 [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)를 참조하세요.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 새 컴퓨터로 이동하는 것을 마이그레이션이라고 합니다. 설치를 마이그레이션할 때는 설치 프로그램을 실행하여 새 보고서 서버 인스턴스를 설치한 후 인스턴스 데이터를 새 컴퓨터로 복사합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 마이그레이션하는 방법은 다음 항목을 참조하십시오.  
  
    -   [Reporting Services 업그레이드 및 마이그레이션](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
    -   [Reporting Services 설치 마이그레이션&#40;SharePoint 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [Reporting Services 설치 마이그레이션&#40;기본 모드&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>보고서 서버 데이터베이스 백업  
 보고서 서버는 상태 비저장 서버이므로 응용 프로그램 데이터는 모두 **인스턴스에서 실행되는** reportserver **및** reportservertempdb [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스에 저장됩니다. 지원되는 **데이터베이스 백업 방법 중 하나를 사용하여** reportserver **및** reportservertempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업할 수 있습니다. 보고서 서버 데이터베이스에 특정한 권장 사항은 다음과 같습니다.  
  
-   **reportserver** 데이터베이스를 백업하려면 전체 복구 모델을 사용합니다.  
  
-   **reportservertempdb** 데이터베이스를 백업하려면 단순 복구 모델을 사용합니다.  
  
-   데이터베이스마다 다른 백업 일정을 사용할 수 있습니다. **reportservertempdb** 를 백업하는 유일한 이유는 하드웨어 오류가 있을 때 데이터베이스를 다시 만들지 않아도 되게 하기 위해서입니다. 하드웨어 오류가 발생할 경우 **reportservertempdb**의 데이터를 복구할 필요는 없지만 테이블 구조는 복구해야 합니다. **reportservertempdb**가 손실된 경우 보고서 서버 데이터베이스를 다시 만들어야만 복구가 가능합니다. **reportservertempdb**를 다시 만드는 경우에는 기본 보고서 서버 데이터베이스와 같은 이름을 지정하는 것이 중요합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스 백업 및 복구에 대한 자세한 내용은 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  보고서 서버가 SharePoint 모드에 있는 경우에는 SharePoint 구성 데이터베이스 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 경고 데이터베이스 등 추가 데이터베이스를 고려해야 합니다. SharePoint 모드에서는 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대해 3개의 데이터베이스( **Reportserver**, **reportservertempdb**및 **dataalerting** 데이터베이스)가 만들어집니다. 자세한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램 백업 및 복원](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)을 참조하세요.  
  
## <a name="backing-up-the-encryption-keys"></a>암호화 키 백업  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 처음으로 구성하는 경우에는 암호화 키를 백업해야 합니다. 서비스 계정의 ID를 변경하거나 컴퓨터 이름을 바꾸는 경우에도 항상 키를 백업해야 합니다. 자세한 내용은 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)을 참조하세요. SharePoint 모드 보고서 서버에 대한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)의 "키 관리" 섹션을 참조하세요.  
  
## <a name="backing-up-the-configuration-files"></a>구성 파일 백업  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 구성 파일을 사용하여 응용 프로그램 설정을 저장합니다. 서버를 처음 구성할 때와 사용자 지정 확장 프로그램을 배포한 후에 파일을 백업해야 합니다. 백업할 파일에는 다음이 포함됩니다.  
  
-   Rsreportserver.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   보고서 서버 및 보고서 관리자 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램용 Web.config  
  
-   Machine.config: [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>데이터 파일 백업  
 보고서 디자이너와 모델 디자이너에서 만들어 유지 관리하는 파일을 백업합니다. 여기에는 보고서 정의 파일(.rdl), 보고서 모델 파일(.smdl), 공유 데이터 원본 파일(.rds), 데이터 뷰 파일(.dv), 데이터 원본 파일(.ds), 보고서 서버 프로젝트 파일(.rptproj) 및 보고서 솔루션 파일(.sln)이 포함됩니다.  
  
 관리 또는 배포 태스크를 위해 만든 스크립트 파일(.rss)은 반드시 백업합니다.  
  
 사용 중인 사용자 지정 확장 프로그램 및 사용자 지정 어셈블리의 백업 복사본이 있는지 확인합니다.  

## <a name="next-steps"></a>다음 단계

[보고서 서버 데이터베이스](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
[rskeymgmt 유틸리티](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)   
[백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
[보고서 서버 데이터베이스 관리](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
[암호화 키 구성 및 관리](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
