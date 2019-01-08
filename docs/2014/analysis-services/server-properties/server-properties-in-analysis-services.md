---
title: Analysis Services의 서버 속성 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a2f99dc4ba728fb97eac0ced00624fc8c8831e6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369735"
---
# <a name="configure-server-properties-in-analysis-services"></a>Analysis Services에서 서버 속성 구성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 기본 서버 구성 속성을 수정할 수 있습니다. 각 인스턴스에는 동일한 서버의 다른 인스턴스와 독립적으로 설정할 수 있는 자체 구성 속성이 있습니다.  
  
 서버 속성을 설정하려면 SQL Server Management Studio를 사용하거나 특정 인스턴스의 msmdsrv.ini 파일을 편집합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [서버 (인스턴스) 속성 구성](#bkmk_config)  
  
 [서버 속성 참조](#bkmk_ref)  
  
##  <a name="bkmk_config"></a> 서버 (인스턴스) 속성 구성  
 SQL Server Management Studio의 속성 페이지에는 사용 가능한 속성의 하위 집합이 포함되어 있으며 수정할 가능성이 높은 속성만 표시됩니다. 전체 속성 집합은 msmdsrv.ini 파일에 있습니다.  
  
> [!NOTE]  
>  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 배포 구성 속성에 대해 설명하지 않습니다. 배포 구성에 대 한 자세한 내용은 참조 하세요. [솔루션 배포에 대 한 구성 설정 지정](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)합니다.  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Management Studio에서 구성 속성 보기 또는 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다.  
  
     개체 탐색기에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 일반 페이지가 표시되고 더 일반적으로 사용되는 속성이 표시됩니다.  
  
2.  추가 속성을 보려면 페이지 맨 아래의 **고급 속성 모두 표시** 확인란을 클릭합니다.  
  
     테이블 형식 모드 및 다차원 모드 서버에 대해서만 서버 속성을 수정할 수 있습니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]을 설치한 경우 Microsoft 제품 지원 담당자가 다르게 지시한 경우가 아니라면 항상 기본값을 사용하십시오.  
  
     서버 속성을 통해 운영 또는 성능 문제를 해결하는 방법은 [SQL Server 2008 R2 Analysis Services 작업 가이드](https://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.  
  
     Microsoft 백서 [SQL Server 2005 Analysis Services (SSAS) Server Properties](https://go.microsoft.com/fwlink/?LinkID=199102)(SQL Server 2005 Analysis Services(SSAS) 서버 속성)에 나와 있는 서버 속성도 참조할 수 있습니다. 서버 속성의 대부분은 지난 몇 번의 릴리스에서 변경되지 않았습니다.  
  
    > [!NOTE]  
    >  일부 속성은 msmdrsrv.ini 파일에서만 설정할 수 있습니다. 고급 속성을 표시한 후에도 설정할 속성이 표시되지 않으면 msmdsrv.ini 파일을 직접 편집해야 합니다.  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>수동으로 msmdsrv.ini 파일의 구성 속성 보기 또는 편집  
  
1.  시작하기 전에 Management Studio의 일반 속성 페이지에서 **DataDir** 속성을 검토하여 msmdsrv.ini 파일을 비롯한 Analysis Services 프로그램 파일의 위치를 확인합니다. 이 프로그램 파일의 위치를 확인하면 올바른 파일을 수정하고 있음을 알 수 있습니다.  
  
    > [!NOTE]  
    >  기본 설치에서는 \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config 폴더에서 이 파일을 찾을 수 있습니다.  
  
2.  원래 파일로 되돌려야 하는 경우를 대비하여 파일의 백업을 만듭니다.  
  
3.  텍스트 편집기를 사용하여 msmdsrv.ini 파일을 보거나 편집합니다.  
  
4.  파일을 저장한 후 서비스를 다시 시작해야 합니다.  
  
##  <a name="bkmk_ref"></a> 서버 속성 참조  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 속성은 시스템을 제대로 튜닝하기 위해 중요합니다. 예를 들어 요구 사항과 일관적으로 쿼리 로그 동작을 만들기 위해 관련 속성들을 설정할 수 있습니다.  
  
 다음 항목에서는 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 속성에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[일반 속성](general-properties.md)|일반 속성에는 데이터 디렉터리, 백업 디렉터리 및 기타 서버 동작을 정의하는 속성을 비롯한 기본 및 고급 속성이 모두 포함됩니다.|  
|[데이터 마이닝 속성](data-mining-properties.md)|데이터 마이닝 속성은 설정 및 해제할 데이터 마이닝 알고리즘을 제어합니다. 기본적으로 모든 알고리즘이 설정됩니다.|  
|DSO|DSO는 더 이상 지원되지 않습니다. DSO 속성은 무시됩니다.|  
|[기능 속성](feature-properties.md)|기능 속성은 서버 인스턴스 간 연결을 제어하는 속성을 비롯한 제품 기능(대부분 고급 기능)에 해당합니다.|  
|[파일 저장소 속성](filestore-properties.md)|파일 저장 속성은 고급 사용을 위한 것입니다. 여기에는 고급 메모리 관리 설정이 포함됩니다.|  
|[잠금 관리자 속성](lock-manager-properties.md)|잠금 관리자 속성은 잠금 및 제한 시간에 해당하는 서버 동작을 정의합니다. 이러한 속성은 대부분 고급 사용을 위한 것입니다.|  
|[로그 속성](log-properties.md)|로그 속성은 서버에서 이벤트를 기록하는 경우, 장소 및 방법을 제어합니다. 여기에는 오류 로깅, 예외 로깅, 비행 레코더, 쿼리 로깅 및 추적이 포함됩니다.|  
|[메모리 속성](memory-properties.md)|메모리 속성은 서버의 메모리 사용 방법을 제어합니다. 이 속성은 주로 고급 사용을 위한 것입니다.|  
|[네트워크 속성](network-properties.md)|네트워크 속성은 압축 및 이진 XML을 제어하는 속성을 비롯한 네트워킹과 관련된 서버 동작을 제어합니다. 이러한 속성은 대부분 고급 사용을 위한 것입니다.|  
|[OLAP 속성](olap-properties.md)|OLAP 속성은 큐브 및 차원 처리, 지연 처리, 데이터 캐싱 및 쿼리 동작을 제어합니다. 여기에는 기본 및 고급 속성이 모두 포함됩니다.|  
|[보안 속성](security-properties.md)|보안 섹션에는 액세스 권한을 정의하는 기본 및 고급 속성이 모두 포함됩니다. 여기에는 관리자 및 사용자와 관련된 설정이 포함됩니다.|  
|[스레드 풀 속성](thread-pool-properties.md)|스레드 풀 속성은 서버에서 만드는 스레드 개수를 제어합니다. 이 속성은 주로 고급 속성입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 인스턴스 관리](../instances/analysis-services-instance-management.md)   
 [솔루션 배포를 위한 구성 설정 지정](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
