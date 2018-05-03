---
title: 큐브 번역 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e4d4200def774bce340af8704009c096ad128a8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cube-translations"></a>큐브 번역
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  번역은 표시된 레이블과 캡션을 한 언어에서 다른 언어로 변경하는 간단한 메커니즘입니다. 각 번역은 한 쌍의 값인 번역된 텍스트가 있는 문자열과 언어 ID가 있는 번호로 정의됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 있는 모든 개체를 번역할 수 있으며 차원의 특성 값도 번역할 수 있습니다. 클라이언트 응용 프로그램에서는 사용자가 정의한 언어 설정과 이 언어로 모든 캡션 및 레이블을 표시하는 스위치를 찾아야 합니다. 개체는 원하는 만큼 다양하게 번역할 수 있습니다.  
  
 단순 <xref:Microsoft.AnalysisServices.Translation> 개체는 언어 ID 번호와 번역된 캡션으로 구성되어 있습니다. 언어 ID 번호는는 **정수** 언어 id 번역된 캡션은 번역된 텍스트입니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 큐브 번역은 캡션 또는 표시 폴더와 같은 큐브 개체의 이름을 언어별로 나타낸 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 차원 및 멤버 이름의 번역도 지원합니다.  
  
 번역은 여러 언어를 지원할 수 있는 클라이언트 응용 프로그램에 대한 서버 지원을 제공합니다. 여러 나라의 사용자가 큐브 데이터를 보는 경우가 많습니다. 이러한 사용자가 큐브의 메타데이터를 보고 이해할 수 있도록 큐브의 여러 요소를 다른 언어로 번역할 수 있으면 매우 유용합니다. 예를 들어 프랑스에 있는 비즈니스 사용자는 프랑스어 로캘이 설정된 워크스테이션에서 큐브에 액세스하여 프랑스어로 개체 속성 값을 볼 수 있습니다. 마찬가지로 독일에 있는 비즈니스 사용자는 독일어 로캘이 설정된 워크스테이션에서 동일한 큐브에 액세스하여 독일어로 동일한 개체 속성 값을 볼 수 있습니다.  
  
 클라이언트 컴퓨터의 데이터 정렬 및 언어 정보는 LCID(로캘 ID) 형식으로 저장됩니다. 연결 시 클라이언트는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 LCID를 전달합니다. 인스턴스는 LCID를 기준으로 각 비즈니스 사용자에게 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 메타데이터를 제공할 때 사용할 번역을 결정합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 지정된 번역이 없으면 콘텐츠가 기본 언어로 클라이언트에 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차원 번역](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Analysis Services에서의 번역 지원](../../analysis-services/translation-support-in-analysis-services.md)   
 [세계화 팁 및 모범 사례 & #40; Analysis Services & #41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
