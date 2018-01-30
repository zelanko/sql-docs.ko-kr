---
title: "테이블 형식 모델 | Microsoft Docs"
ms.custom: 
ms.date: 01/29/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: edeea89c1d767364f4f087d0f4b2e6d566895c52
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2018
---
# <a name="tabular-models"></a>테이블 형식 모델
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]테이블 형식 모델은 메모리 내 또는 백 엔드 관계형 데이터 원본에서 데이터에 직접 액세스 하는 DirectQuery 모드에서 실행 되는 Analysis Services 데이터베이스입니다.  
  
 이 모델은 기본적으로 메모리 내에서 실행됩니다. 최신 상태 압축 알고리즘과 다중 쿼리 프로세서를 사용 하 여 분석 엔진 배달 대 한 빠른 액세스 테이블 형식 모델 개체와 데이터를 Power BI 및 Excel과 같은 클라이언트 응용 프로그램을 보고 하 여 합니다.  
  
 DirectQuery는 모델이 너무 커서 메모리 내에 포함할 수 없거나 데이터 휘발성으로 인해 적절한 처리 전략을 적용할 수 없는 경우 대신 사용 가능한 쿼리 모드입니다. 이번 릴리스에서는 추가 데이터 원본이 지원되고, DirectQuery 모델의 계산된 테이블 및 열을 처리하는 기능이 제공되며, 백 엔드 데이터베이스로 전송되는 DAX 식을 통한 행 수준 보안이 보장되고, 쿼리 최적화로 인해 이전 버전보다 처리량이 더 높아져 DirectQuery가 메모리 내 모델과 더욱 근접한 기능을 제공합니다.
  
 모델, 테이블, 관계 및 HAX 식을 만들 수 있는 디자인 화면을 제공하는 테이블 형식 모델 프로젝트 템플릿을 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 테이블 형식 모델을 작성합니다. 여러 원본에서 데이터를 가져온 다음 관계, 계산된 테이블/열, 측정값, KPI, 계층 및 변환을 추가하여 모델을 보강할 수 있습니다.  
  
 SQL Server Analysis Services 인스턴스의 테이블 형식 서버 모드용으로 구성 하거나 모델 Azure Analysis Services에 다음 배포할 수 있습니다. 다차원 모델 처럼 SQL Server Management Studio에서 배포 된 테이블 형식 모델을 관리할 수 있습니다. 이러한 모델을 처리 최적화를 위해 분할하거나, 역할 기반 보안을 사용하여 행 수준 보안을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [테이블 형식 모델 솔루션](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) -이 섹션의 항목을 만들고 테이블 형식 모델 솔루션 배포에 대해 설명 합니다.
  
 [테이블 형식 모델 데이터베이스](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) -이 섹션의에서 항목에서는 배포 된 테이블 형식 모델 솔루션을 관리에 대해 설명 합니다.
  
 [테이블 형식 모델 데이터 액세스](../../analysis-services/tabular-models/tabular-model-data-access.md) -이 섹션의에서 항목에서는 테이블 형식 모델 솔루션 배포에 연결에 대해 설명 합니다.
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services의 새로운 기능](../../analysis-services/what-s-new-in-analysis-services.md)   
 [테이블 형식 및 다차원 솔루션 비교](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [도구 및 Analysis Services에서 사용 되는 응용 프로그램](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
