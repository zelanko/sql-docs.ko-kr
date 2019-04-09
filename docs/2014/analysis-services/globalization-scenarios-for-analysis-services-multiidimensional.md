---
title: Analysis Services 다차원에 대 한 전역화 시나리오 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b12c2f4a95b2fc295aa1a3524def774e74a5ed32
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241918"
---
# <a name="globalization-scenarios-for-analysis-services-multiidimensional"></a>Analysis Services 다차원에 대한 세계화 시나리오
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 표 형식 데이터 모델과 다차원 데이터 모델 모두에서 다국어 데이터와 메타데이터를 저장 및 조작합니다. 데이터 스토리지는 유니코드 인코딩을 사용하는 문자 집합으로 된 유니코드(UTF-16)입니다. 데이터 모델에 ANSI 데이터를 로드하는 경우 문자는 유니코드 해당 코드 포인트를 사용하여 저장됩니다.  
  
 유니코드를 지원한다는 것은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 Windows 클라이언트 및 서버 운영 체제가 지원하는 언어를 사용하여 데이터를 저장하여, Windows 컴퓨터에 사용된 문자 집합으로 데이터를 읽고, 쓰고, 정렬하고 비교할 수 있음을 의미합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터를 사용하는 BI 클라이언트 응용 프로그램에서는 데이터가 모델에서 해당 언어로 존재한다고 가정하여 데이터를 사용자가 선택한 언어로 나타낼 수 있습니다.  
  
 언어 지원은 서로 다른 사람에게 서로 다른 것을 의미할 수 있습니다. 다음 목록에는 Analysis Services에서 언어를 지원하는 방법과 관련된 몇 가지 일반적인 질문을 해결합니다.  
  
-   이미 언급했듯이 데이터는 Windows 클라이언트 운영 체제에 있는 유니코드로 인코딩된 임의의 문자 집합으로 저장됩니다.  
  
-   개체 이름, 식별자 및 설명과 같은 메타데이터는 유니코드 언어 및 스크립트로 되어 있을 수도 있습니다. 도구와 환경이 다른 언어로 되어 있는 경우에도 마찬가지입니다. 예를 들어, 전체 스택에서 영어와 라틴어 데이터 정렬을 사용하는 개발 환경에서는 이름에 키릴자모 문자를 사용하는 개체를 모델에 포함할 수 있습니다.  
  
     다차원 모델의 경우만은 캡션과 특성 멤버를 번역으로 표현할 수 있습니다. 하나 이상의 번역을 정의한 다음, 로캘 식별자를 사용하여 클라이언트에 반환되는 번역을 결정할 수 있습니다. 자세한 내용은 아래의 [기능](#bkmk_features) 을 참조하세요.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 엔진(msmdsrv)에서 반환되는 오류, 경고 및 정보 메시지는 Office와 Office 365에서 지원하는 43개의 언어로 지역화되어 있습니다. 메시지를 특정 언어로 가져오는 데에는 구성이 필요하지 않습니다. 클라이언트 애플리케이션의 로캘은 반환되는 문자열을 결정합니다.  
  
-   구성 파일(msmdsrv.ini) 및 AMO PowerShell은 영어로만 되어 있습니다.  
  
-   로그 파일에는 Analysis Services가 실행되는 Windows 서버에 언어 팩을 설치한 것으로 가정하여 영어 메시지와 지역화된 메시지가 섞여 있습니다.  
  
-   설명서 및 도구와 같은 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)], 이러한 언어로 번역 됩니다. 한국어, 중국어 간체, 중국어 번체, 프랑스어, 독일어, 이탈리아어, 포르투갈어(브라질), 러시아어, 스페인어 및 일본어로 지역화되어 있습니다. 도구의 언어별 버전을 사용하려면 해당 언어 버전의 SQL Server를 설치(예를 들어 독일어 버전의 SQL Server Management Studio를 설치하여 독일어로 가져오기)하거나 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]에 대해 대상 언어로 독립 실행형 설치 프로그램을 실행합니다.  
  
 Analysis Services를 사용하면 언어, 데이터 정렬 및 번역을 개체 계층 구조 전체에서 독립적으로 설정할 수 있습니다.  
  
 언어, 데이터 정렬 및 번역을 통해 사용할 수 있게 되는 시나리오는 다음과 같습니다.  
  
-   필드 이름과 값이 사용자가 선택한 언어로 표시되도록 하나의 데이터 모델에서 여러 가지의 번역된 캡션을 제공합니다. 캐나다 벨기에, 스위스와 같은 이중 언어 국가에서 운영되는 회사의 경우에는 클라이언트 및 서버 애플리케이션에서 여러 언어를 지원하는 것이 표준 코딩 요구 사항입니다. 이 시나리오는 번역 및 통화 환산을 통해 사용됩니다. 자세한 내용 및 링크는 아래의 [기능](#bkmk_features) 을 참조하세요.  
  
-   개발 및 프로덕션 환경은 다양한 국가에 위치해 있습니다. 한 국가에서 솔루션을 개발한 다음 다른 국가에서 배포하는 것은 점점 일반화되고 있습니다. 특정 언어로 개발된 솔루션을 다른 언어 팩을 사용하는 서버에 배포할 준비 작업을 맡은 경우 언어 및 데이터 정렬 속성을 설정하는 방법을 알아 두어야 합니다. 이러한 속성들을 설정하면 원래의 호스트 시스템에서 얻을 수 있는 상속된 기본값을 재정의할 수 있습니다. 자세한 내용은 아래의 [Languages and Collations &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md) 을 참조하세요.  
  
##  <a name="bkmk_features"></a> 세계화 된 다차원 솔루션을 구축 하기 위한 기능  
 [!INCLUDE[applies](../includes/applies-md.md)] 다차원 데이터 모델에만 해당  
  
 클라이언트 수준에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 데이터를 사용하거나 조작하는 세계화된 애플리케이션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 다국어 및 다문화 기능을 사용할 수 있습니다.  
  
-   [번역 &#40;Analysis Services&#41; ](translations-analysis-services.md) 번역 된 각 문자열이 다른 번역과 함께 있을 수 있는 단일 개체에 대해 여러 캡션을 포함 하 여 사용 됩니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]을 사용하여 큐브 및 측정값, 차원 및 특성의 캡션, 설명 및 계정 유형에 대한 번역을 정의할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결할 때 로캘 ID를 제공하여 번역을 자동으로 정의한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에서 데이터 및 메타데이터를 검색할 수 있습니다.  
  
     이 기능을 사용 하는 방법에 대 한 단원에서 찾을 수 있습니다 [단원 9: 큐브 뷰 및 번역 정의](lesson-9-defining-perspectives-and-translations.md) 의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 자습서입니다.  
  
-   [통화 변환 &#40;Analysis Services&#41; ](currency-conversions-analysis-services.md) 통화 데이터를 포함 하는 측정값을 변환 하는 특수화 된 MDX 스크립트를 통해 이루어집니다. [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 의 비즈니스 인텔리전스 마법사를 사용하면 통화 데이터를 포함하는 측정값을 변환하기 위해 차원, 특성 및 측정값 그룹의 데이터 및 메타데이터를 조합하여 사용하는 MDX 스크립트를 생성할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[언어 및 데이터 정렬&#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 기본 언어 및 Windows 데이터 정렬을 지정합니다. 선택 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 관리하는 데이터 및 메타데이터에 영향을 줍니다.|  
|[번역 &#40;Analysis Services&#41;](translations-analysis-services.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스와 데이터베이스에 포함된 개체에 대한 번역을 정의합니다. 이 항목에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]이 클라이언트 응용 프로그램의 번역된 데이터와 메타데이터에 대한 요청을 해결하는 방법에 대해 설명합니다.|  
|[통화 변환 &#40;Analysis Services&#41;](currency-conversions-analysis-services.md)|비즈니스 인텔리전스 마법사를 사용하여 통화 변환을 정의합니다.|  
|[세계화 팁과 모범 사례&#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)|다중 언어 데이터와 관련된 문제를 방지하는 데 도움이 될 수 있는 몇 가지 디자인과 코딩 방법을 검토합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Windows 애플리케이션에 대한 국제화](/windows/desktop/Intl/international-support)   
 [Microsoft 전역화 설명서](/globalization/)   
 [로캘 기반 적응형 디자인을 사용하여 Windows 스토어 앱 작성](http://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [C# 및 XAML을 사용하여 범용 Windows 앱 개발](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
