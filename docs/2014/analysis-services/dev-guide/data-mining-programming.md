---
title: 데이터 마이닝 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data mining [Analysis Services], developer's guide
ms.assetid: 9fd77b16-0b89-44ce-bcf1-7c04b62499da
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1ad8f0d8e066fde6f199af26c977b5a9ba3d8917
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313291"
---
# <a name="data-mining-programming"></a>데이터 마이닝 프로그래밍
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 기본 제공 도구 및 뷰어가 사용자의 요구 사항을 충족시키지 못할 경우 사용자 고유의 확장을 코딩하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 기능을 확장할 수 있습니다. 이 경우 다음 중 하나를 선택할 수 있습니다.  
  
-   **XMLA**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 클라이언트 응용 프로그램과 통신을 위한 프로토콜로 XML for Analysis (XMLA)을 지원합니다. 추가 명령은 XML for Analysis 사양을 확장한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원됩니다.  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 데이터 정의, 데이터 조작 및 데이터 제어 지원을 위해 XMLA를 사용하므로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 제공하는 비주얼 도구를 사용하여 마이닝 구조 및 마이닝 모델을 만든 다음 DMX(Data Mining Extensions) 및 ASSL(Analysis Services Scripting Language) 스크립트를 사용하여 만든 데이터 마이닝 개체를 확장할 수 있습니다.  
  
     데이터 마이닝 개체를 XMLA 스크립트에서 전적으로 만들고 수정할 수 있으며, 사용자 고유의 응용 프로그램에서 모델에 대한 예측 쿼리를 프로그래밍 방식으로 실행할 수 있습니다.  
  
-   **Analysis Management Objects (AMO)**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 또한 타사 데이터 마이닝 공급자가 데이터 마이닝 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 통합할 수 있도록 하는 완전한 프레임워크를 제공합니다.  
  
     AMO를 사용하여 마이닝 구조와 마이닝 모델을 만들 수 있습니다. CodePlex의 다음 예제를 참조하십시오.  
  
    -   AMO Browser  
  
         지정한 SSAS 인스턴스에 연결하고 마이닝 구조 및 마이닝 모델을 비롯한 모든 서버 개체와 해당 속성을 나열합니다.  
  
    -   AMO Simple Sample  
  
         AS Simple Sample은 대부분의 주요 개체에 대한 프로그래밍 방식 액세스를 다루며 메타데이터 찾아보기 및 개체 값에 대한 액세스를 보여 줍니다.  
  
         또한 데이터 마이닝 구조 및 모델을 만들고 처리하는 방법과 기존 데이터 마이닝 모델을 찾아보는 방법도 보여 줍니다.  
  
-   **DMX**  
  
     DMX를 사용하여 명령 문, 예측 쿼리 및 메타데이터 쿼리를 캡슐화할 수 있으며, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 대한 연결을 만들었다고 가정하고 표 형식으로 결과를 반환할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 마이닝용 OLE DB](../../../2014/analysis-services/dev-guide/ole-db-for-data-mining.md)  
 데이터 마이닝 및 다차원 데이터를 지원할 수 있도록 새로운 스키마 행 집합 및 열, 마이닝 구조를 만들고 관리하는 데 사용할 수 있는 DMX(Data Mining Extensions) 언어 등 사양에 새로 추가된 사항을 설명합니다.  
  
## <a name="related-reference"></a>관련 참조  
 [ADOMD.NET을 사용하여 개발](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 ADOMD.NET 클라이언트 및 서버 프로그래밍 개체를 소개합니다.  
  
 [Analysis Management Objects를 사용 하 여 개발 &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
 AMO 프로그래밍 라이브러리를 소개합니다.  
  
 [개발 analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 XMLA(XML for Analysis) 및 해당 확장을 소개합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개발자 가이드 &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)   
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
