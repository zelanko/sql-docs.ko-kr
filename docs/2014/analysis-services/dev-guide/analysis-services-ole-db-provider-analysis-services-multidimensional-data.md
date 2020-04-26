---
title: Analysis Services OLE DB Provider (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services OLE DB Provider
ms.assetid: cdeecd50-1d91-4162-a4a2-01c7799b02a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0af68d7aa25d00f257399ade415e0287dd275fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62732189"
---
# <a name="analysis-services-ole-db-provider-analysis-services---multidimensional-data"></a>Analysis Services OLE DB 공급자(Analysis Services - 다차원 데이터)
  Analysis Services OLE DB Provider는와 상호 작용 하 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 응용 프로그램에 대 한 인터페이스입니다. 다차원 데이터와 상호 작용하는 클라이언트 애플리케이션을 구축하는 데 사용됩니다. 또한 이 공급자는 다차원 데이터 및 관계형 데이터의 온/오프라인 데이터 마이닝 분석을 제공하며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 일부로 포함됩니다. 타사 클라이언트 애플리케이션에서 재배포할 수 있습니다.  
  
 Analysis Services OLE DB 공급자는 큐브 또는 데이터 마이닝 모델에 연결하고, 큐브 또는 데이터 마이닝 모델을 쿼리하고, 스키마 정보를 검색하는 등의 태스크를 수행하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 와 상호 작용하는 주요한 방법입니다.  
  
 독립 실행형 공급자인 Analysis Services OLE DB 공급자는 관계형/다차원 원본에서 로컬 큐브 파일과 마이닝 모델을 만들 수 있는 클라이언트 애플리케이션을 제공합니다. 클라이언트 애플리케이션은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스를 실행하는 대규모 실제 서버와 상호 작용 없이도 MDX(Multidimensional Expressions)를 사용하여 로컬 큐브에 연결하고 쿼리를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [다차원 모델 데이터 액세스 &#40;Analysis Services 다차원 데이터&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
