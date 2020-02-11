---
title: Analysis Services Scripting Language ()를 사용 하 여 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfdce0d0db35d651d12670ffd3cb1c9437961cd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736520"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>ASSL(Analysis Services Scripting Language)을 사용하여 개발
  ASSL(Analysis Services Scripting Language)은 서버에서 Analysis Services 구조를 직접 만들고 관리하기 위한 개체 정의 언어 및 명령 언어를 추가하는 XMLA에 대한 확장 프로그램입니다. 사용자 지정 애플리케이션에서 ASSL을 사용하여 XMLA 프로토콜로 Analysis Services와 통신할 수 있습니다. ASSL은 두 부분으로 구성됩니다.  
  
-   DDL(데이터 정의 언어) - 개체 정의 언어라고도 하며 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스와 해당 인스턴스에 포함되는 데이터베이스 및 데이터베이스 개체를 정의하고 설명합니다.  
  
-   명령 언어 - `Create`, `Alter` 또는 `Process`와 같은 동작 명령을 Analysis Services 인스턴스로 보냅니다. 이 명령 언어는 [XML for Analysis &#40;XMLA&#41; 참조](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)에 설명 되어 있습니다.  
  
 
  [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]에서 다차원 솔루션을 설명하는 ASSL을 보려면 프로젝트 수준에서 View Code 명령을 사용합니다. XMLA 쿼리 편집기를 사용하여 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 ASSL 스크립트를 만들거나 편집할 수도 있습니다. 작성하는 스크립트는 서버에서 개체를 관리하거나 명령을 실행하는 데 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [개체 및 개체 특징](assl-objects-and-object-characteristics.md)   
 [XML 규칙](assl-xml-conventions.md)   
 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
