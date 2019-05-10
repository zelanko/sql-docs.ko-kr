---
title: 데이터베이스 요구 사항(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: fe731839-c5c4-4884-bb6a-644eca28bb30
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 75bd453d4540a675809973f711bd778ab8639d10
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479310"
---
# <a name="database-requirements-master-data-services"></a>데이터베이스 요구 사항(MDS(Master Data Services))
  모든 마스터 데이터는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 저장됩니다. 이 데이터베이스를 호스팅하는 컴퓨터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스를 실행해야 합니다.  
  
 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 사용하여 로컬 또는 원격 컴퓨터에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만들고 구성할 수 있습니다. 여러 환경 간에 데이터베이스를 이동하는 경우 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 서비스 및 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 를 새 위치의 데이터베이스에 연결하여 새 환경에서 정보를 유지 관리할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 의 구성 요소를 설치할 모든 컴퓨터는 사용 허가를 받아야 합니다. 자세한 내용은 EULA(최종 사용자 사용권 계약)를 참조하십시오.  
  
## <a name="requirements"></a>요구 사항  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만들기 전에 다음 요구 사항이 충족되는지 확인하십시오.  
  
### <a name="sql-server-edition"></a>SQL Server 버전  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스는 다음 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호스팅할 수 있습니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence(64비트) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(64비트) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer(64비트) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Business Intelligence(64비트) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Enterprise(64비트) x64 – [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Enterprise에서만 업그레이드  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Developer(64비트) x64  
  
-   Microsoft SQL Server 2008 R2 Enterprise(64비트) x64  
  
-   Microsoft SQL Server 2008 R2 Developer(64비트) x64  
  
 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
### <a name="operating-system"></a>운영 체제  
 지원 되는 Windows 운영 체제 및 기타 요구 사항에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 참조 하십시오 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)합니다.  
  
### <a name="accounts-and-permissions"></a>계정 및 사용 권한  
  
|형식|Description|  
|----------|-----------------|  
|사용자 계정|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 호스팅하기 위해 Windows 계정 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 계정을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 인스턴스에 연결할 수 있습니다. 사용자 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 **sysadmin** 서버 역할에 속해야 합니다. **sysadmin** 역할에 대한 자세한 내용은 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)을 참조하세요.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 관리자 계정|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만들 때 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 시스템 관리자가 될 도메인 사용자 계정을 지정해야 합니다. 이 데이터베이스에 연결된 모든 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에 대해 이 사용자는 모든 기능 영역에서 모든 모델과 데이터를 업데이트할 수 있습니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../administrators-master-data-services.md)를 참조하세요.|  
  
### <a name="database-backup"></a>데이터베이스 백업  
 매일 작업량이 적은 시간에 전체 데이터베이스를 백업하고 사용자 환경의 요구 사항에 따라 트랜잭션 로그를 보다 자주 백업하는 것이 가장 좋습니다. 데이터베이스 백업에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [MDS(Master Data Services) 설치](install-master-data-services.md)   
 [Master Data Services 데이터베이스 만들기](create-a-master-data-services-database.md)   
 [Master Data Services 데이터베이스](../master-data-services-database.md)   
 [Master Data Services 데이터베이스에 연결 대화 상자](../connect-to-a-master-data-services-database-dialog-box.md)   
 [데이터베이스 만들기 마법사&#40;Master Data Services 구성 관리자&#41;](../create-database-wizard-master-data-services-configuration-manager.md)  
  
  
