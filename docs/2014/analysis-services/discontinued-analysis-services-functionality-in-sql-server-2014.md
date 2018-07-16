---
title: 지원 되지 않는 SQL Server 2014에서에서 Analysis Services 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5a2a17f11d4fd1470c25c4280bda370d49c054a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332493"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 Analysis Services 기능
  이 항목에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다.  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|범주|사용되지 않는 기능|대체 기능|  
|--------------|------------------------|-----------------|  
|로컬 큐브|InsertInto 연결 문자열 속성|로컬 큐브를 채우기 위한 원래의 연결 문자열 구문이 Create Global Cube 문으로 바뀌었습니다. 자세한 내용은 [GLOBAL CUBE Statement 만들기 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)합니다.|  
|로컬 큐브|CreateCube 연결 문자열 속성|로컬 큐브를 채우기 위한 원래의 연결 문자열 구문이 Create Global Cube 문으로 바뀌었습니다. 자세한 내용은 [GLOBAL CUBE Statement 만들기 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)합니다.|  
|데이터 마이닝|SQL Server 2000 PMML|SQL Server 2000 PMML 기능에서는 PMML 사양에서 사용할 수 없는 데이터 마이닝 알고리즘으로 제공된 고유 기능을 지원하기 위해 고유 확장 프로그램이 포함된 PMML 형식을 생성했습니다. SQL Server 2005에서는 Analysis Services에서 PMML 기능이 새로운 PMML 2.1 표준으로 업데이트되었습니다. 따라서 SQL Server 2000에 추가된 고유 확장 프로그램은 이 버전에서도 계속 지원되지만 더 이상 필요하지 않습니다.|  
|MDX 문|Create Action 문|이 문은 이전 버전과의 호환성을 위해 포함되었습니다. 이 문은 동작 개체로 바뀌었습니다. 최신 버전의 작업을 만드는 방법에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 참조 하세요 [작업 &#40;Analysis Services-Multidimensional Data&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).|  
  
## <a name="discontinued-features-in-previous-releases"></a>이전 릴리스에서 지원되지 않는 기능  
 SQL Server 2000이 더 이상 지원되지 않으므로 SQL Server 2000 Analysis Services 데이터베이스를 새 버전으로 업그레이드하는 데 사용되었던 마이그레이션 마법사는 이제 지원되지 않습니다.  
  
 SQL Server 2000 Analysis Services 데이터베이스와의 호환성을 제공했던 DSO(의사 결정 지원 개체) 라이브러리도 지원되지 않으며 SQL Server에 더 이상 포함되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 이전 버전과의 호환성](analysis-services-backward-compatibility.md)  
  
  
