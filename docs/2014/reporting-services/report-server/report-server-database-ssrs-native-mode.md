---
title: 보고서 서버 데이터베이스(SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e5f5225ef696a5477ef9d0aa4a67749bc5e4a88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103447"
---
# <a name="report-server-database-ssrs-native-mode"></a>보고서 서버 데이터베이스(SSRS 기본 모드)
  보고서 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 사용하여 메타데이터와 개체 정의를 저장하는 상태 비저장 서버입니다. 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치는 두 개의 데이터베이스를 사용하여 임시 스토리지와는 별도로 영구 데이터 스토리지를 제공합니다. 데이터베이스는 함께 생성되며 이름별로 바인딩됩니다. 기본적으로 데이터베이스 이름은 각각 **reportserver** 와 **reportservertempdb**입니다.  
  
 SharePoint 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치도 데이터 경고 기능에 대한 데이터베이스를 만듭니다. SharePoint 모드에 있는 3개의 데이터베이스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션과 연결되어 있습니다. 자세한 내용은 [Reporting Services SharePoint 서비스 애플리케이션 관리](../manage-a-reporting-services-sharepoint-service-application.md)를 참조하세요.  
  
 데이터베이스는 로컬 또는 원격 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 실행될 수 있습니다. 시스템 리소스가 충분하거나 소프트웨어 라이선스를 절약하려는 경우 로컬 인스턴스를 선택하면 유용하지만 원격 컴퓨터에서 데이터베이스를 실행하면 성능이 개선될 수 있습니다.  
  
 이전 설치 또는 다른 보고서 서버 인스턴스가 있는 다른 인스턴스에서 기존 보고서 서버 데이터베이스를 이식하거나 다시 사용할 수 있습니다. 보고서 서버 데이터베이스의 스키마는 보고서 서버 인스턴스와 호환되어야 합니다. 데이터베이스가 이전 형식일 경우 현재 형식으로 업그레이드할지 묻는 메시지가 표시됩니다. 최신 버전을 이전 버전으로 다운그레이드할 수는 없습니다. 최신 보고서 서버 데이터베이스가 있는 경우 이 데이터베이스를 이전 버전의 보고서 서버 인스턴스와 함께 사용할 수 없습니다. 보고서 서버 데이터베이스를 최신 형식으로 업그레이드하는 방법에 대한 자세한 내용은 [보고서 서버 데이터베이스 업그레이드](../install-windows/upgrade-a-report-server-database.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  데이터베이스의 테이블 구조는 서버 작업을 위해 최적화된 것이므로 수정하거나 조정하지 마십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서 현재 릴리스의 테이블 구조를 다음 릴리스에서 변경할 수 있습니다. 데이터베이스를 수정하거나 확장하면 나중에 프로그램을 업그레이드하거나 서비스 팩을 적용하기 어려울 수 있습니다. 또한 사용자 변경에 따라 보고서 서버 작업이 올바르게 수행되지 않을 수 있습니다. 예를 들면 ReportServer 데이터베이스에서 READ_COMMITTED_SNAPSHOT을 설정하면 대화형 정렬 기능이 중단됩니다.  
  
 보고서 서버 데이터베이스에 대한 모든 액세스는 보고서 서버를 통해 처리되어야 합니다. 보고서 서버 데이터베이스의 내용에 액세스하기 위해 보고서 서버 관리 도구(예: 보고서 관리자 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) 또는 URL 액세스, 보고서 서버 웹 서비스, WMI(Windows Management Instrumentation) 공급자와 같은 프로그래밍 인터페이스를 사용할 수 있습니다.  
  
 보고서 서버 데이터베이스에 대한 연결은 일반적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 통해 정의됩니다. 그러나 기본 구성을 설치하도록 선택한 경우에는 설치 중에 정의할 수도 있습니다. 데이터베이스로의 보고서 서버 연결에 대한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.  
  
## <a name="report-server-database"></a>보고서 서버 데이터베이스  
 보고서 서버 데이터베이스는 다음 내용을 저장하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   보고서 서버에서 관리 되는 항목 (... 보고서와 연결 된 보고서, 공유 데이터 원본, 보고서 모델, 폴더, 리소스) 및 모든 속성 및 해당 항목과 연관 된 보안 설정 합니다.  
  
-   구독 및 일정 정의  
  
-   보고서 스냅샷(쿼리 결과 포함)과 보고서 기록  
  
-   시스템 속성 및 시스템 수준 보안 설정  
  
-   보고서 실행 로그 데이터  
  
-   보고서 데이터 원본에 대한 대칭 키와 암호화된 연결 및 자격 증명  
  
 보고서 서버 데이터베이스에서는 애플리케이션 상태 및 지속적 데이터를 저장하므로 데이터 손실을 방지하려면 이 데이터베이스에 대한 백업 일정을 만들어야 합니다. 데이터베이스를 백업하는 방법에 대한 권장 사항 및 지침은 [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)을 참조하세요.  
  
## <a name="report-server-temporary-database"></a>보고서 서버 임시 데이터베이스  
 각 보고서 서버 데이터베이스는 관련된 임시 데이터베이스를 사용하여 보고서 서버에서 생성한 세션 및 실행 데이터, 캐시된 보고서 및 작업 테이블을 저장합니다. 백그라운드 서버 프로세스에서는 임시 데이터베이스의 테이블에서 사용되지 않는 오래된 항목을 정기적으로 제거합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 데이터베이스가 없어도 임시 데이터베이스를 다시 만들지 않으며 테이블이 없거나 수정된 경우에도 해당 테이블을 복구하지 않습니다. 임시 데이터베이스에는 지속적 데이터가 들어 있지 않지만 오류 복구 작업의 일환으로 데이터베이스를 다시 만들 필요가 없도록 데이터베이스 복사본을 백업해야 합니다.  
  
 임시 데이터베이스를 백업하고 이후에 복원한 경우에는 내용을 삭제해야 합니다. 일반적으로 임시 데이터베이스의 내용은 언제든지 삭제하는 것이 안전합니다. 그러나 내용을 삭제한 후에는 보고서 서버 Windows 서비스를 다시 시작해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 장애 조치(failover) 클러스터에서 보고서 서버 데이터베이스 호스팅](../install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 보고서 서버](../reporting-services-report-server.md)   
 [보고서 서버 데이터베이스 관리&#40;SSRS 기본 모드&#41;](report-server-database-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services 백업 및 복원 작업](../install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
