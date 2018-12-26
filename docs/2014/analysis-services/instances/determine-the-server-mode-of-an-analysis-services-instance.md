---
title: 서버 모드의 Analysis Services 인스턴스의 확인 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 9e556fb1-ca37-4f06-8f8f-f187cb0fdb37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50ddca5c3cdb1b7e314ccc6650bbd8fcc3ed3841
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113443"
---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>Analysis Services 인스턴스의 서버 모드 확인
  Analysis Services는 다차원 및 데이터 마이닝(기본값), SharePoint용 PowerPivot, 테이블 형식 중 한 가지 서버 모드로 설치할 수 있습니다. Analysis Services 인스턴스의 서버 모드는 설치 중에 서버 설치 옵션을 선택할 때 결정됩니다.  
  
 서버 모드에 따라 만들어서 배포하는 솔루션 유형이 결정됩니다. 서버 소프트웨어를 설치하지 않은 경우 서버가 설치된 모드를 확인하려면 이 항목의 정보를 사용할 수 있습니다. 특정 모드의 기능 가용성에 대한 자세한 내용은 [테이블 형식 및 다차원 솔루션 비교&#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md)를 참조하세요.  
  
 설치한 서버 모드를 사용하지 않으려면 소프트웨어를 제거한 후 다시 설치하여 원하는 모드를 선택해야 합니다. 또는 여러 인스턴스에서 서로 다른 모드를 실행하도록 동일한 컴퓨터에 Analysis Services의 다른 인스턴스를 설치할 수 있습니다.  
  
## <a name="server-icons-in-object-explorer"></a>개체 탐색기의 서버 아이콘  
 서버 모드를 쉽게 확인하려면 SQL Server Management Studio에서 서버에 연결한 다음 개체 탐색기에서 서버 이름 옆에 있는 아이콘을 확인합니다. 다음 그림은 다차원, 테이블 형식 및 PowerPivot 모드에서 배포된 Analysis Services의 세 가지 인스턴스를 보여 줍니다.  
  
 ![개체 탐색기 아이콘 각 서버 모드에 대 한](../media/ssas-ssms-servermodes.gif "각 서버 모드에 대 한 개체 탐색기 아이콘")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>MSMDSRV.INI 파일에서 DeploymentMode 속성 보기  
 또는 모든 Analysis Services 인스턴스에 포함된 msmdsrv.ini 파일에서 `DeploymentMode` 속성을 확인할 수 있습니다. 이 속성의 값은 서버 모드를 식별합니다. 유효한 값은 0(다차원), 1(SharePoint) 또는 2(테이블 형식)입니다. msmdsrv.ini 파일을 열려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자(즉, 서버 역할의 멤버)여야 합니다. 이 파일에는 구조화된 XML이 포함되어 있습니다. 메모장이나 다른 텍스트 편집기를 사용하여 파일을 볼 수 있습니다.  
  
> [!CAUTION]  
>  값을 변경 하지 마십시오는 `DeploymentMode` 속성입니다. 서버를 설치한 후에는 속성을 수동으로 변경할 수 없습니다.  
  
## <a name="about-the-deploymentmode-property"></a>DeploymentMode 속성 정보  
 `DeploymentMode` 속성은 Analysis Services 서버 인스턴스의 작업 컨텍스트를 결정합니다. 대화 상자, 메시지 및 설명서에서는 이 속성을 '서버 모드'라고 합니다. 이 속성은 Analysis Services 설치 방법에 따라 설치 프로그램에 의해 초기화됩니다. 이 속성을 내부 값으로만 간주하여 항상 설치 프로그램에서 지정한 값을 사용해야 합니다.  
  
 이 속성에 유효한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|이것은 기본값입니다. 이 설정은 MOLAP, HOLAP 및 ROLAP 저장소를 사용하는 다차원 데이터베이스와 데이터 마이닝 모델에 서비스를 제공하는 데 사용되는 다차원 모드를 지정합니다.|  
|1|SharePoint용 PowerPivot 배포의 일부로 설치된 Analysis Services 인스턴스를 지정합니다. SharePoint용 PowerPivot 설치의 일부인 Analysis Services 인스턴스의 배포 모드 속성은 변경하지 마십시오. 모드를 변경하면 PowerPivot 데이터가 서버에서 더 이상 실행되지 않습니다.|  
|2|메모리 내 저장소나 DirectQuery 저장소를 사용하는 테이블 형식 model 데이터베이스를 호스팅하는 데 사용되는 테이블 형식 모드를 지정합니다.|  
  
 각 모드는 다른 모드와 함께 사용할 수 없습니다. 테이블 형식 모드용으로 구성된 서버는 큐브 및 차원이 포함된 기본 Analysis Services 데이터베이스를 실행할 수 없습니다. 기본 컴퓨터 하드웨어에서 지원하는 경우 같은 컴퓨터에 Analysis Services 인스턴스를 여러 개 설치하고 각 인스턴스가 다른 배포 모드를 사용하도록 구성할 수 있습니다. Analysis Services는 리소스를 많이 사용하는 애플리케이션이므로 고성능 서버인 경우에만 한 시스템에 여러 개의 인스턴스를 배포하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 모드에서 Analysis Services 설치](install-windows/install-analysis-services.md)   
 [다차원 및 데이터 마이닝 모드에서 Analysis Services 설치](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [PowerPivot for SharePoint 2010 설치](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Analysis Services에 연결](connect-to-analysis-services.md)   
 [테이블 형식 모델 솔루션 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../tabular-model-solutions-ssas-tabular.md)   
 [다차원 모델 솔루션 &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [마이닝 모델 &#40;Analysis Services-데이터 마이닝&#41;](../data-mining/mining-models-analysis-services-data-mining.md)  
  
  
