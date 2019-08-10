---
title: 다차원 및 데이터 마이닝 모드에서 Analysis Services 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 2353d2f623a5aa0e0f1f5c25710724f836093998
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890381"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>다차원 및 데이터 마이닝 모드에서 Analysis Services 설치
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 비즈니스 인텔리전스 응용 프로그램을 위한 OLAP(온라인 분석 처리) 및 데이터 마이닝 기능을 제공합니다. 이 릴리스에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] *다차원 모드로*를 설치할 때 OLAP 데이터베이스 및 데이터 마이닝 모델에 대 한 지원을 사용할 수 있습니다. 다차원 모드는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]가 실행되는 세 가지 서버 모드 중 하나이며 기본 모드입니다. 기본값을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 설치하면 다차원 데이터베이스 및 데이터 마이닝 모델을 실행하는 인스턴스를 얻게 됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 여러 인스턴스를 지원하므로 한 컴퓨터에 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 설치하거나 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 이전 버전과 함께 실행할 수 있습니다. 서버 모드는 인스턴스에 적용됩니다. 다른 모드를 사용하려면 서버 인스턴스를 추가로 설치해야 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 단독으로 설치하거나 다른 구성 요소와 함께 설치할 수 있습니다. 만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]설치 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 기능 선택 페이지에서 **Analysis Services** 를 선택 하면 다음 기능이 설치 됩니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 및 데이터 마이닝 모델을 실행하기 위한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버  
  
-   원본 데이터베이스에 대한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 액세스에 사용되는 데이터 공급자  
  
-   SQL Server 구성 관리자  
  
## <a name="choosing-additional-features"></a>추가 기능 선택  
 Analysis Services OLAP 및 데이터 웨어하우스 솔루션의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개발, 배포 및 관리를 수행하려면 추가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치해야 합니다. 일반적인 여러 사용자 시나리오에서 다음과 같은 추가 기능이 옵션으로 제공됩니다.  
  
-   Analysis Services 데이터 구조 및 데이터 마이닝 모델을 만들고 보는 데 사용되는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   클라이언트 및 서버 간 통신에 사용 되는 클라이언트 도구 연결 구성 요소 (DB-LIBRARY, ODBC 및 OLE DB의 네트워크 라이브러리 포함)  
  
-   데이터 이동, 복사 및 변환을 위한 그래픽 및 프로그래밍 가능 개체 모음인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 및 복제 모니터를 비롯한 관리 도구  
  
## <a name="installation-tasks"></a>설치 태스크  
 설치할 때는 다음 태스크를 수행해야 합니다.  
  
|링크|태스크|  
|-----------|-----------|  
|SQL Server 2014을 설치 하 고 [Windows 서비스 계정 및 사용 권한을 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) [하기 위한 하드웨어 및 소프트웨어 요구 사항](hardware-and-software-requirements-for-installing-sql-server.md) 입니다.|설치 프로그램을 실행하기 전에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설치에 필요한 필수 구성 요소를 확인하고 서버 프로비전에 사용할 계정을 결정합니다.|  
|[설치 마법사 &#40;설치 프로그램&#41;에서 SQL Server 2014을 설치](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)합니다.|SQL Server 설치 프로그램을 실행하여 소프트웨어를 설치합니다.|  
|[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|설치가 완료되면 서버로의 원격 연결을 허용하도록 방화벽 설정을 구성해야 합니다.|  
|[개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services)|Analysis Services 데이터베이스에 액세스하는 사용자는 서버에 있는 데이터베이스 하나 이상에 대해 읽기 권한을 가지고 있어야 합니다.|  
  
## <a name="related-content"></a>관련 내용  
 설치와 관련된 추가적인 내용은 다음 항목을 참조하십시오.  
  
 [테이블 형식 모드에서 Analysis Services 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Analysis Services 인스턴스의 서버 모드 확인](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)  
  
 [SQL Server 데이터 마이닝 추가 기능](https://go.microsoft.com/fwlink/?LinkId=197091)  
  
 기본적으로 예제 데이터베이스, 예제 코드 및 클라이언트 응용 프로그램 추가 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 설치되지 않습니다. 예제 데이터베이스와 예제 코드를 설치하려면 [CodePlex 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=87843)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)   
 [언어 및 데이터 정렬&#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
