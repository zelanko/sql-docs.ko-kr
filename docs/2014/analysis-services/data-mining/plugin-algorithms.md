---
title: 플러그 인 알고리즘 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3112efa1b2eec2f25abe35315ecec13bedbf8871
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375485"
---
# <a name="plugin-algorithms"></a>플러그 인 알고리즘
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 알고리즘 외에 여러 가지 알고리즘을 데이터 마이닝에 사용할 수 있습니다. 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 타사에서 만든 알고리즘을 "연결"하는 메커니즘을 제공합니다. 특정 표준을 따르는 알고리즘은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 내에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 알고리즘을 사용하듯이 사용할 수 있습니다. 플러그 인 알고리즘에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 제공하는 알고리즘의 모든 기능이 포함되어 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 플러그 인 알고리즘과 통신하는 데 사용하는 인터페이스에 대한 전체 설명을 보려면 [CodePlex](https://go.microsoft.com/fwlink/?LinkID=87843) 웹 사이트에 게시된 사용자 지정 알고리즘 및 사용자 지정 모델 뷰어를 만드는 예제를 참조하십시오.  
  
## <a name="algorithm-requirements"></a>알고리즘 요구 사항  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 알고리즘을 연결하려면 다음 COM 인터페이스를 구현해야 합니다.  
  
 `IDMAlgorithm`  
 모델을 생성하는 알고리즘을 구현하고 결과 모델의 예측 작업을 구현합니다.  
  
 `IDMAlgorithmNavigation`  
 브라우저에서 모델의 내용에 액세스할 수 있도록 설정합니다.  
  
 `IDMPersist`  
 알고리즘에서 학습하는 모델을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 저장 및 로드할 수 있도록 설정합니다.  
  
 `IDMAlgorithmMetadata`  
 알고리즘의 기능 및 입력 매개 변수를 설명합니다.  
  
 `IDMAlgorithmFactory`  
 알고리즘 인터페이스를 구현하는 개체의 인스턴스를 만들고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 알고리즘-메타데이터 인터페이스에 액세스할 수 있도록 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 이러한 COM 인터페이스를 사용하여 플러그 인 알고리즘과 통신합니다. 사용하는 플러그 인 알고리즘이 데이터 마이닝용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB 사양을 지원해야 하지만 사양의 데이터 마이닝 옵션을 모두 지원하지 않아도 됩니다. [MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset) 스키마 행 집합을 사용하여 알고리즘의 기능을 확인할 수 있습니다. 이러한 스키마 행 집합은 각 플러그 인 알고리즘 공급자에 대한 데이터 마이닝 지원 옵션을 나열합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 새 알고리즘을 사용하려면 먼저 해당 알고리즘을 등록해야 합니다. 알고리즘을 등록하려면 알고리즘을 포함할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 .ini 파일에 다음 정보를 추가합니다.  
  
-   알고리즘 이름  
  
-   ProgID - 선택적 정보이며 플러그 인 알고리즘의 경우에만 포함됩니다.  
  
-   알고리즘 설정 여부를 나타내는 플래그  
  
 다음 코드 예제에서는 새 알고리즘을 등록하는 방법을 보여 줍니다.  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [DMSCHEMA_MINING_SERVICES 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)  
  
  
