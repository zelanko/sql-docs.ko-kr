---
title: Business Intelligence (CSDLBI)에 대 한 CSDL 주석 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 72559f9d1282f9d95ba2a875023e7a89a1afcfe1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>비즈니스 인텔리전스에 대한 CSDL 주석(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 CSDLBI(비즈니스 인텔리전스 포함 개념 스키마 정의 언어) 주석이라는 XML 형식으로 테이블 형식 모델 정의를 표현할 수 있도록 합니다. 이 항목에서는 CSDLBI의 개요와 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 모델에서 CSDLBI를 사용하는 방법을 설명합니다.  
  
## <a name="understanding-the-role-of-csdl"></a>CSDL의 역할 이해  
 CSDL(개념 스키마 데이터 언어)은 엔터티, 관계 및 함수를 설명하는 XML 기반 언어입니다. CSDL은 엔터티 데이터 프레임워크의 일부로 정의됩니다. BI 주석은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 사용하여 데이터 모델링을 지원하도록 설계된 확장 프로그램입니다.  
  
 CSDL이 엔터티 데이터 프레임워크와 호환되기는 하지만 엔터티 관계 모델을 이해하거나 모델을 기반으로 테이블 형식 모델이나 보고서를 작성할 수 있는 특수한 도구가 있어야 할 필요는 없습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]와 같은 클라이언트 도구 또는 AMO와 같은 API를 사용하여 모델을 작성하고 모델을 서버에 배포합니다.  
  
 CSDLBI 스키마는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]와 같은 클라이언트의 모델 정의 요청에 대한 응답으로 Analysis Services 서버에서 생성됩니다. 클라이언트 응용 프로그램에서 모델 데이터를 호스팅하는 Analysis Services 서버에 XML 쿼리를 보냅니다. 서버는 CSDLBI 주석을 사용하여 모델의 엔터티 정의가 포함된 XML 메시지를 응답으로 보냅니다. 그러면 보고 클라이언트는 이 정보를 토대로 모델에서 사용할 수 있는 필드, 집계 및 측정값을 표시합니다. CSDLBI 주석은 데이터의 그룹화, 정렬 및 서식 지정 방법에 대한 정보도 제공합니다.  
  
 CSDLBI에 대 한 일반 정보를 참조 하십시오. [CSDLBI 개념](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)합니다.  
  
### <a name="working-with-csdl"></a>CSDL 작업  
 특정 테이블 형식 모델을 나타내는 CSDLBI 주석 집합은 단순 및 복합 엔터티 컬렉션이 포함된 XML 문서입니다. 엔터티는 계산 열, 측정값 또는 KPI에 포함된 테이블(또는 차원), 열(특성), 연결(관계) 및 수식을 정의합니다.  
  
 이러한 개체를 직접 수정할 수는 없으며 테이블 형식 모델을 사용할 수 있도록 제공된 클라이언트 도구 및 API(응용 프로그래밍 인터페이스)를 사용해야 합니다.  
  
 모델을 호스팅하는 서버에 DISCOVER 요청을 보내 모델의 CSDL을 얻을 수 있습니다. 이 요청은 서버 및 모델을 지정하고 선택적으로 뷰 또는 큐브 뷰를 지정하여 정규화해야 합니다. 반환되는 메시지는 XML 문자열입니다. 일부 요소는 언어별로 다르며, 현재 연결 언어에 따라 다른 값을 반환할 수 있습니다. 자세한 내용은 참조 [DISCOVER_CSDL_METADATA 행 집합](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)합니다.  
  
### <a name="csdlbi-versions"></a>CSDLBI 버전  
 엔터티 데이터 프레임워크의 원래 CSDL 사양은 모델링을 지원하는 데 필요한 대부분의 엔터티와 속성을 제공합니다. BI 주석은 테이블 형식 모델의 특별 요구 사항, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]와 같은 클라이언트에 필요한 보고 속성, 다차원 모델에 필요한 추가 메타데이터를 지원합니다. 이 단원에서는 각 버전의 업데이트를 설명합니다.  
  
 **CSDLBI 1.0**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델을 지원하기 위한 CSDL 스키마에 대한 초기 추가 기능 집합에는 데이터 모델링, 사용자 지정 계산 및 향상된 프레젠테이션을 지원하는 주석이 포함되었습니다.  
  
-   테이블 형식 모델을 지원하는 새로운 요소 및 속성. 예를 들어, 모델을 채우는 데 사용되는 데이터베이스 쿼리 유형을 지정하기 위한 속성이 추가되었습니다.  
  
-   새로운 특성 및 기존 엔터티에 대한 확장.  예를 들어, Association 요소는 관계를 지원하도록 확장되었습니다.  
  
-   시각화 및 탐색 속성, 예를 들어, 사용자 지정 정렬 필드, 기본 이미지를 지원하기 위한 속성이 추가되었습니다.  
  
 **CSDLBI 1.1**  
  
 이 버전의 CSDLBI 스키마에는 다차원 데이터베이스(예: OLAP 큐브)를 지원하는 추가 기능이 포함됩니다. 새로운 요소와 속성은 다음과 같습니다.  
  
-   엔터티인 차원에 대한 지원.  
  
-   계층에 대한 지원.  
  
-   ROLAP 파티션 제공.  
  
-   번역에 대한 지원.  
  
-   큐브 뷰에 대한 지원.  
  
 CSDLBI 주석은의 개별 요소에 대 한 자세한 내용은 참조 하십시오. [csdl 용 BI 주석에 대 한 기술 참조](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)합니다. 핵심 CSDL 사양에 대 한 정보를 참조 하십시오.는 [CSDL 사양](http://go.microsoft.com/fwlink/?LinkId=205855) msdn 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 개념](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)   
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
