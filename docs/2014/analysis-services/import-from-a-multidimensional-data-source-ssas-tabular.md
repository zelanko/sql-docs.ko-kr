---
title: 가져오기-다차원 데이터 원본 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 666b7fdf5af10b6726a1e1d7a2aaafa075bf8777
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080562"
---
# <a name="import-from-a-multidimensional-data-source-ssas-tabular"></a>다차원 데이터 원본에서 가져오기(SSAS 테이블 형식)
  Analysis Services 큐브 데이터베이스를 테이블 형식 모델의 데이터 원본으로 사용할 수 있습니다. Analysis Services 큐브에서 데이터를 가져오려면 MDX 쿼리를 정의하여 가져올 데이터를 선택해야 합니다  
  
 SQL Server Analysis Services 데이터베이스에 포함된 모든 데이터를 모델로 가져올 수 있습니다. 차원의 일부 또는 전체를 추출하거나, 큐브에서 현재 연도의 매월 판매량 합계 등과 같은 집계 및 조각을 가져올 수 있습니다. 하지만 큐브에서 가져오는 모든 데이터는 일반 데이터여야 합니다. 따라서 여러 차원을 따라 측정값을 검색하는 쿼리를 정의하는 경우 데이터를 가져올 때 각 차원이 별개의 열이 됩니다.  
  
 Analysis Services 큐브는 SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]버전이어야 합니다.  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>Analysis Services 큐브에서 데이터를 가져오려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 **모델** 메뉴를 클릭한 다음 **데이터 원본에서 가져오기**를 클릭합니다.  
  
2.  **데이터 원본에 연결** 페이지에서 **Microsoft Analysis Services**를 선택하고 **다음**을 클릭합니다.  
  
3.  테이블 가져오기 마법사의 단계별 지침을 따릅니다. **MDX 쿼리 지정** 페이지에서 MDX 쿼리를 지정할 수 있습니다. MDX 쿼리 디자이너를 사용하려면 MDX 쿼리 지정 페이지에서 **디자인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 가져오기&#40;SSAS 테이블 형식&#41;](import-data-ssas-tabular.md)   
 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
