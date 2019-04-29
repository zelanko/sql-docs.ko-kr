---
title: Services (기본 데이터 마이닝 자습서) 프로젝트 분석 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee6c1a8b765843304d25f1e2ad485ede2badcba4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855191"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>Analysis Services 프로젝트 만들기(기본 데이터 마이닝 자습서)
  각 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트에서는 단일 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 있는 개체를 정의합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에는 여러 다른 유형의 개체가 포함될 수 있습니다.  
  
-   다차원 모델(큐브)  
  
-   마이닝 구조 및 마이닝 모델  
  
-   데이터 원본, 데이터 원본 뷰 및 사용자 지정 어셈블리와 같은 개체 지원  
  
 데이터 마이닝을 수행하는 데는 큐브가 필요하지 **않습니다** . 기존 큐브에서 데이터 마이닝을 수행해야 하는 경우 큐브를 빌드하는 데 사용한 동일한 프로젝트에 데이터 마이닝 모델을 추가해야 합니다. 그러나 대부분의 경우 데이터 웨어하우스와 같은 관계형 데이터 원본에서 모델을 빌드할 수 있고 큐브가 포함되지 않는 경우 더 나은 성능을 얻을 수 있습니다.  
  
 이 자습서에서는 관계형 데이터 웨어하우스 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]를 데이터 원본으로 사용합니다. 모든 데이터 마이닝 개체를 데이터 마이닝에만 사용되는 `BasicDataMining`이라는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스로 배포합니다.  
  
 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 새 프로젝트에 **localhost** 인스턴스를 사용합니다. 명명된 인스턴스나 다른 서버를 사용할 경우에는 먼저 프로젝트를 만들고 연 다음 인스턴스 이름을 변경해야 합니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 참조 하세요 [Analysis Services 프로젝트 만들기](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md)합니다.  
  
### <a name="to-create-an-analysis-services-project"></a>Analysis Services 프로젝트를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 엽니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 선택합니다.  
  
3.  **프로젝트 형식** 창에서 **비즈니스 인텔리전스 프로젝트** 가 선택되어 있는지 확인합니다.  
  
4.  **템플릿** 창에서 **Analysis Services 다차원 및 데이터 마이닝 프로젝트**를 선택합니다.  
  
5.  에 **이름을** 상자에서 새 프로젝트의 이름을 `BasicDataMining`입니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>데이터 마이닝 개체가 저장되는 인스턴스를 변경하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **프로젝트** 메뉴에서 **속성**을 선택합니다.  
  
2.  **속성 페이지** 창 왼쪽의 **구성 속성**에서 **배포**를 클릭합니다.  
  
3.  **속성 페이지** 창 오른쪽의 **대상**에서 **서버** 이름이 **localhost**인지 확인합니다. 다른 인스턴스를 사용할 경우에는 해당 인스턴스의 이름을 입력합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [데이터 원본 만들기 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Analysis Services 프로젝트 만들기&#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
