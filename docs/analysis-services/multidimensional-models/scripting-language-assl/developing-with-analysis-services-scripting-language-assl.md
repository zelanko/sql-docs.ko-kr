---
title: Services Scripting Language (ASSL) 분석을 사용 하 여 개발 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c113e07099ed96abdb0eb5f62c8517ee422d3cc7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208481"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>ASSL(Analysis Services Scripting Language)을 사용하여 개발
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ASSL(Analysis Services Scripting Language)은 서버에서 Analysis Services 구조를 직접 만들고 관리하기 위한 개체 정의 언어 및 명령 언어를 추가하는 XMLA에 대한 확장 프로그램입니다. 사용자 지정 응용 프로그램에서 ASSL을 사용하여 XMLA 프로토콜로 Analysis Services와 통신할 수 있습니다. ASSL은 두 부분으로 구성됩니다.  
  
-   DDL(데이터 정의 언어) - 개체 정의 언어라고도 하며 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스와 해당 인스턴스에 포함되는 데이터베이스 및 데이터베이스 개체를 정의하고 설명합니다.  
  
-   명령 언어와 같은 동작 명령을 보내는 **만들기**, **Alter**, 또는 **프로세스**, Analysis Services 인스턴스에 있습니다. 이 명령 언어를 [XML for Analysis &#40;XMLA&#41; 참조](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)합니다.  
  
 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]에서 다차원 솔루션을 설명하는 ASSL을 보려면 프로젝트 수준에서 View Code 명령을 사용합니다. XMLA 쿼리 편집기를 사용하여 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 ASSL 스크립트를 만들거나 편집할 수도 있습니다. 작성하는 스크립트는 서버에서 개체를 관리하거나 명령을 실행하는 데 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ASSL 개체 및 개체 특징](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [ASSL XML 표기 규칙](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
