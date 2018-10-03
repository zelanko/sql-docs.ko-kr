---
title: Analysis Services 인스턴스 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ad91ac53d2ff041c3da32fd9a609e67e8b9d1c1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196225"
---
# <a name="analysis-services-instance-management"></a>Analysis Services 인스턴스 관리
  Analysis Services 인스턴스는 운영 체제 서비스로 실행되는 `msmdsrv.exe` 실행 파일의 복사본입니다. 각 인스턴스는 동일한 서버에서 완전히 독립적이며 고유한 구성 설정, 사용 권한, 포트, 시작 계정, 파일 저장소 및 서버 모드 속성을 가지고 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 각 인스턴스는 정의된 로그온 계정의 보안 컨텍스트에서 Windows 서비스인 Msmdsrv.exe로 실행됩니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 기본 인스턴스에 대한 서비스 이름은 MSSQLServerOLAPService입니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 명명된 인스턴스 각각에 대한 서비스 이름은 MSOLAP$InstanceName입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 여러 개 설치되는 경우 설치 프로그램에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스와 통합되는 리디렉터 서비스도 설치합니다. 리디렉터 서비스는 클라이언트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 해당 명명된 인스턴스로 전달합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 항상 로컬 서비스 계정의 보안 컨텍스트에서 실행됩니다. 로컬 서비스 계정은 Windows에서 로컬 컴퓨터 외부의 리소스에 액세스하지 않는 서비스에 사용되는 제한된 사용자 계정입니다.  
  
 다중 인스턴스는 동일한 하드웨어에 여러 서버 인스턴스를 설치하여 확장할 수 있음을 의미합니다. 특히, Analysis Services에서는 각각 특정 모드에서 실행하도록 구성된 여러 인스턴스를 동일한 서버에 설치하여 여러 서버 모드를 지원할 수 있습니다.  
  
 서버 모드는 인스턴스에 사용되는 저장소와 메모리 아키텍처를 결정하는 서버 속성입니다. 다차원 모드에서 실행되는 서버는 다차원 큐브 데이터베이스 및 데이터 마이닝 모델용으로 작성된 리소스 관리 계층을 사용합니다. 반대로 테이블 형식 서버 모드에서는 xVelocity 메모리 내 분석 엔진(VertiPaq) 및 데이터 압축을 사용하여 요청 시 데이터를 집계합니다.  
  
 저장소 및 메모리 아키텍처가 다르다는 것은 Analysis Services의 단일 인스턴스에서 테이블 형식 데이터베이스와 다차원 데이터베이스 중 하나를 실행함을 의미합니다. 서버 모드 속성에 따라 인스턴스에서 실행되는 데이터베이스의 유형이 결정됩니다.  
  
 서버 모드는 설치 중에 서버에서 실행되는 데이터베이스 유형을 지정할 때 설정됩니다. 사용 가능한 모드를 모두 지원하려면 Analysis Services 인스턴스를 여러 개 설치합니다. 이때 각 인스턴스는 작성 중인 프로젝트에 해당하는 서버 모드로 배포됩니다.  
  
 수행해야 하는 대부분의 관리 태스크는 대개 모드별로 다릅니다. Analysis Services 시스템 관리자는 동일한 절차와 스크립트를 사용하여 인스턴스의 설치 방법에 상관없이 네트워크에서 모든 Analysis Services 인스턴스를 관리할 수 있습니다.  
  
> [!NOTE]  
>  SharePoint용 PowerPivot은 예외입니다. PowerPivot 배포 서버 관리는 항상 SharePoint 팜 컨텍스트 내에서 이루어집니다. PowerPivot은 다른 서버 모드와 달리 항상 단일 인스턴스이고 SharePoint 중앙 관리 또는 PowerPivot 구성 도구를 통해 관리됩니다. SQL Server Management Studio에서 SharePoint 용 PowerPivot에 연결할 수 있지만 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], 것은 바람직하지 않습니다. SharePoint 팜에는 서버 상태를 동기화하고 서버 가용성을 감독하는 인프라가 포함되어 있습니다. 다른 도구를 사용하면 이 작업에 방해가 될 수 있습니다. PowerPivot 서버 관리에 대 한 자세한 내용은 참조 하세요. [SharePoint 용 PowerPivot &#40;SSAS&#41;](../power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|링크|태스크 설명|  
|----------|----------------------|  
|[설치 후 구성 &#40;Analysis Services&#41;](post-install-configuration-analysis-services.md)|Analysis Services의 설치를 완료하거나 수정하는 필수 태스크와 선택적 태스크에 대해 설명합니다.|  
|[Analysis Services에 연결](connect-to-analysis-services.md)|연결 문자열 속성, 클라이언트 라이브러리, 인증 방법 및 연결을 설정하거나 해제하는 단계에 대해 설명합니다.|  
|[Analysis Services 인스턴스 모니터링](monitor-an-analysis-services-instance.md)|성능 모니터 및 SQL Server Profiler를 사용하는 방법을 비롯하여 서버 인스턴스를 모니터링하는 데 유용한 도구와 기술에 대해 설명합니다.|  
|[Analysis Services의 스크립트 관리 태스크](../script-administrative-tasks-in-analysis-services.md)|처리를 비롯한 많은 관리 태스크를 자동화하는 방법에 대해 설명합니다.|  
|[Analysis Services 다차원에 대 한 세계화 시나리오](../globalization-scenarios-for-analysis-services-multiidimensional.md)|언어 및 데이터 정렬 지원, 두 속성의 변경 단계, 언어 및 데이터 정렬 동작 설정 및 테스트를 위한 팁 등에 대해 설명합니다.|  
|[Analysis Services의 로그 작업](log-operations-in-analysis-services.md)|로그와 로그를 구성하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 및 다차원 솔루션 비교 &#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [PowerPivot 구성 도구](../power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [중앙 관리에서 PowerPivot 서버 관리 및 구성](../power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
