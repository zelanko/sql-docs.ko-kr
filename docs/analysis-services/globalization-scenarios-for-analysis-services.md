---
title: Analysis Services의 세계화 시나리오 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bdc6ec79432d97d8ed53cade4a7db4c0b8bbec82
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="globalization-scenarios-for-analysis-services"></a>Analysis Services의 세계화 시나리오
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 테이블 형식 데이터 모델과 다차원 데이터 모델 둘 다의 다국어 데이터와 메타데이터를 저장 및 조작합니다. 데이터 저장소는 유니코드 인코딩을 사용하는 문자 집합으로 된 유니코드(UTF-16)입니다. 데이터 모델에 ANSI 데이터를 로드하는 경우 문자는 유니코드 해당 코드 포인트를 사용하여 저장됩니다.  
  
 유니코드를 지원한다는 것은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 Windows 클라이언트 및 서버 운영 체제가 지원하는 언어를 사용하여 데이터를 저장하여, Windows 컴퓨터에 사용된 문자 집합으로 데이터를 읽고, 쓰고, 정렬하고 비교할 수 있음을 의미합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터를 사용하는 BI 클라이언트 응용 프로그램에서는 데이터가 모델에서 해당 언어로 존재한다고 가정하여 데이터를 사용자가 선택한 언어로 나타낼 수 있습니다.  
  
 언어 지원은 서로 다른 사람에게 서로 다른 것을 의미할 수 있습니다. 다음 목록에는 Analysis Services에서 언어를 지원하는 방법과 관련된 몇 가지 일반적인 질문을 해결합니다.  
  
-   이미 언급했듯이 데이터는 Windows 클라이언트 운영 체제에 있는 유니코드로 인코딩된 임의의 문자 집합으로 저장됩니다.  
  
-   개체 이름 등의 메타데이터는 번역할 수 있습니다. 모델 유형별로 지원되는 기능도 다르지만 다차원 모델과 테이블 형식 모델에서는 모두 번역된 문자열을 모델에 추가할 수 있습니다. 여러 번역을 정의한 다음 로컬 식별자를 사용하여 클라이언트로 반환되는 번역을 결정할 수 있습니다. 자세한 내용은 아래의 [기능](#bkmk_features) 을 참조하세요.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 엔진(msmdsrv)에서 반환되는 오류, 경고 및 정보 메시지는 Office와 Office 365에서 지원하는 43개의 언어로 지역화되어 있습니다. 메시지를 특정 언어로 가져오는 데에는 구성이 필요하지 않습니다. 클라이언트 응용 프로그램의 로캘은 반환되는 문자열을 결정합니다.  
  
-   구성 파일(msmdsrv.ini) 및 AMO PowerShell은 영어로만 되어 있습니다.  
  
-   로그 파일에는 Analysis Services가 실행되는 Windows 서버에 언어 팩을 설치한 것으로 가정하여 영어 메시지와 지역화된 메시지가 섞여 있습니다.  
  
-   [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 및 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]와 같은 설명서와 도구는 한국어, 중국어 간체, 중국어 번체, 프랑스어, 독일어, 이탈리아어, 일본어, 포르투갈어(브라질), 러시아어 및 스페인어로 지역화되어 있습니다. 문화권은 설치 중에 지정됩니다.  
  
 다차원 모델의 경우 Analysis Services를 사용하면 언어, 데이터 정렬 및 번역을 개체 계층 전체에서 독립적으로 설정할 수 있습니다.  테이블 형식 모델의 경우에는 번역만 추가할 수 있으며 언어와 데이터 정렬은 호스트 운영 체제에서 상속됩니다.  
  
 Analysis Services 세계화 기능을 통해 사용 가능한 시나리오는 다음과 같습니다.  
  
-   필드 이름과 값이 사용자가 선택한 언어로 표시되도록 하나의 데이터 모델에서 여러 가지의 번역된 캡션을 제공합니다. 캐나다 벨기에, 스위스와 같은 이중 언어 국가에서 운영되는 회사의 경우에는 클라이언트 및 서버 응용 프로그램에서 여러 언어를 지원하는 것이 표준 코딩 요구 사항입니다. 이 시나리오는 번역 및 통화 환산을 통해 사용됩니다. 자세한 내용 및 링크는 아래의 [기능](#bkmk_features) 을 참조하세요.  
  
-   개발 및 프로덕션 환경은 다양한 국가에 위치해 있습니다. 한 국가에서 솔루션을 개발한 다음 다른 국가에서 배포하는 것은 점점 일반화되고 있습니다. 특정 언어로 개발된 솔루션을 다른 언어 팩을 사용하는 서버에 배포할 준비 작업을 맡은 경우 언어 및 데이터 정렬 속성을 설정하는 방법을 알아 두어야 합니다. 이러한 속성들을 설정하면 원래의 호스트 시스템에서 얻을 수 있는 상속된 기본값을 재정의할 수 있습니다. 자세한 내용은 아래의 [언어 및 데이터 정렬&#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md) 을 참조하세요.  
  
##  <a name="bkmk_features"></a> 세계화된 다국어 솔루션을 구축하기 위한 기능  
 클라이언트 수준에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 데이터를 사용하거나 조작하는 세계화된 응용 프로그램에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 다국어 및 다문화 기능을 사용할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결할 때 로캘 ID를 제공하여 번역을 자동으로 정의한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에서 데이터 및 메타데이터를 검색할 수 있습니다.  
  
 다중 언어 데이터와 관련된 문제를 방지하는 데 도움이 될 수 있는 디자인 및 코딩 방법은 [세계화 팁 및 모범 사례&#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)를 참조하세요.  
  
||||  
|-|-|-|  
|**기능**|**테이블 형식**|**다차원**|  
|[언어 및 데이터 정렬&#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)|운영 체제에서 상속됩니다.|상속되지만 모델 개체의 주요 개체 언어와 데이터 정렬을 모두 재정의할 수 있습니다.|  
|번역 지원 범위|캡션 및 설명|개체 이름, 캡션, 식별자 및 설명에 대해 모든 유니코드 언어와 스크립트로 번역을 생성할 수 있습니다. 도구와 환경이 다른 언어로 되어 있는 경우에도 마찬가지입니다. 예를 들어, 전체 스택에서 영어와 라틴어 데이터 정렬을 사용하는 개발 환경에서는 이름에 키릴자모 문자를 사용하는 개체를 모델에 포함할 수 있습니다.|  
|번역 지원 구현|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 데이터를 작성해 번역 파일을 생성한 다음 내용을 입력하고 모델로 다시 가져옵니다.<br /><br /> 자세한 내용은 [테이블 형식 모델 번역&#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)을 참조하세요.|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 데이터를 작성해 큐브/측정값/치수/특성에 대한 캡션, 설명 및 계정 유형의 번역을 정의합니다.<br /><br /> 자세한 내용은 [다차원 모델의 번역&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)을 참조하세요. 이 기능을 사용하는 방법에 대한 단원은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 자습서의 [9단원: 큐브 뷰 및 번역 정의](../analysis-services/lesson-9-defining-perspectives-and-translations.md)에 있습니다.|  
|통화 변환|사용할 수 없습니다.|통화 변환은 통화 데이터를 포함하는 측정값을 변환하는 특수화된 MDX 스크립트를 통해 수행됩니다. [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 의 비즈니스 인텔리전스 마법사를 사용하면 통화 데이터를 포함하는 측정값을 변환하기 위해 차원, 특성 및 측정값 그룹의 데이터 및 메타데이터를 조합하여 사용하는 MDX 스크립트를 생성할 수 있습니다. [통화 환산&#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md)을 참조하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서의 번역 지원](../analysis-services/translation-support-in-analysis-services.md)   
 [Windows 응용 프로그램에 대 한 국제화](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Go Global 개발자 센터](http://msdn.microsoft.com/goglobal/bb871628.aspx)   
 [로캘 기반 적응형 디자인을 사용 하 여 쓰기 Windows 스토어 앱](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [C# 및 XAML을 사용 하 여 유니버설 Windows 앱 개발](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
