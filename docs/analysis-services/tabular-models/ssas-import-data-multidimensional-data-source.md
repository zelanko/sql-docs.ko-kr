---
title: "다차원 데이터 원본 (SSAS 테이블 형식)에서 가져오기 | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4aaa43e745c86cd493279fe8bd875d376f8185c0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---multidimensional-data-source"></a>데이터 요금-다차원 데이터 원본 가져오기
  Analysis Services 큐브 데이터베이스를 테이블 형식 모델의 데이터 원본으로 사용할 수 있습니다. Analysis Services 큐브에서 데이터를 가져오려면 MDX 쿼리를 정의하여 가져올 데이터를 선택해야 합니다  
  
 SQL Server Analysis Services 데이터베이스에 포함된 모든 데이터를 모델로 가져올 수 있습니다. 차원의 일부 또는 전체를 추출하거나, 큐브에서 현재 연도의 매월 판매량 합계 등과 같은 집계 및 조각을 가져올 수 있습니다. 하지만 큐브에서 가져오는 모든 데이터는 일반 데이터여야 합니다. 따라서 여러 차원을 따라 측정값을 검색하는 쿼리를 정의하는 경우 데이터를 가져올 때 각 차원이 별개의 열이 됩니다.  
  
 Analysis Services 큐브는 SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]버전이어야 합니다.  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>Analysis Services 큐브에서 데이터를 가져오려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **모델** 메뉴를 클릭한 다음 **데이터 원본에서 가져오기**를 클릭합니다.  
  
2.  **데이터 원본에 연결** 페이지에서 **Microsoft Analysis Services**를 선택하고 **다음**을 클릭합니다.  
  
3.  테이블 가져오기 마법사의 단계별 지침을 따릅니다. **MDX 쿼리 지정** 페이지에서 MDX 쿼리를 지정할 수 있습니다. MDX 쿼리 디자이너를 사용하려면 MDX 쿼리 지정 페이지에서 **디자인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 가져오기&#40;SSAS 테이블 형식&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
