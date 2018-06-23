---
title: '14 단원: 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 2b9bf4afde77cc0438e097c14f6b3743c7da427d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181195"
---
# <a name="lesson-14-deploy"></a>14단원: 배포
  이 단원에서는 테이블 형식 모드로 실행되는 Analysis Services의 배포 서버 인스턴스를 지정하고 배포할 모델의 이름을 지정하여 배포 속성을 구성합니다. 그 다음에는 모델을 해당 인스턴스에 배포합니다. 모델을 배포한 후 사용자는 보고 클라이언트 응용 프로그램을 사용하여 모델에 연결할 수 있습니다. 자세한 내용은 [테이블 형식 모델 솔루션 배포&#40;SSAS 테이블 형식&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md)를 참조하세요.  
  
 이 단원에 소요되는 예상 시간: **5분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [13단원: Excel에서 분석](lesson-12-analyze-in-excel.md)을 완료해야 합니다.  
  
## <a name="deploy-the-model"></a>모델 배포  
  
#### <a name="to-configure-deployment-properties"></a>배포 속성을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 **솔루션 탐색기**에서 **Adventure Works Internet Sales Tabular Model** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **속성**을 클릭합니다.  
  
2.  **AW Internet Sales Tabular Model 속성 페이지** 대화 상자에서 **배포 서버**아래의 **서버** 속성에 테이블 형식 모드로 실행 중인 Analysis Services 인스턴스의 이름을 입력합니다. 나중에 이 인스턴스에 모델을 배포하게 됩니다.  
  
    > [!IMPORTANT]  
    >  원격 Analysis Services 인스턴스에 배포하려면 해당 인스턴스에 대한 관리자 권한이 있어야 합니다.  
  
3.  확인 된 **쿼리 모드** 속성이로 설정 되어 **메모리**합니다.  
  
    > [!NOTE]  
    >  이 자습서를 사용하여 만든 모델은 DirectQuery 모드에서는 지원되지 않습니다.  
  
4.  에 **데이터베이스** 속성, 유형 `Adventure Works Internet Sales Model`합니다.  
  
5.  에 **큐브** Name 속성을 입력 `Adventure Works Internet Sales Model`합니다.  
  
6.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 테이블 형식 모델을 배포하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **빌드** 메뉴를 클릭한 다음 **AW Internet Sales Tabular Model 배포**를 클릭합니다.  
  
     배포 대화 상자가 나타나고 메타데이터 및 모델에 포함된 각 테이블의 배포 상태가 표시됩니다.  
  
## <a name="conclusion"></a>결론  
 축하합니다. 첫 번째 Analysis Services 테이블 형식 모델을 제작하고 배포했습니다. 이 자습서에서는 테이블 형식 모델을 만들기 위해 수행해야 하는 대부분의 일반적인 태스크를 완료하는 과정을 안내했습니다. 이제 Adventure Works Internet Sales Model이 배포되었으므로 SQL Server Management Studio를 사용하여 모델을 관리하고 처리 스크립트와 백업 계획을 만들 수 있습니다. 사용자는 Microsoft Excel이나 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 같은 보고 클라이언트 응용 프로그램을 사용하여 모델에 연결할 수 있습니다.  
  
## <a name="additional-resources"></a>추가 리소스  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 보고서를 지원하는 테이블 형식 모델 속성에 대한 자세한 내용은 [파워 뷰 보고 속성&#40;SSAS 테이블 형식&#41;](tabular-models/properties-ssas-tabular.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [기본 데이터 모델링 및 배포 속성 구성 &#40;SSAS 테이블 형식&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [테이블 형식 모델 데이터베이스 &#40;SSAS 테이블 형식&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  