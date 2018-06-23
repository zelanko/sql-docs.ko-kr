---
title: 테이블 형식 모델 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0ceb461e-12c1-44ea-97ac-b99bf308676b
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 785e4818d635d41dc27eea8fc63b62cf63e0ff92
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182348"
---
# <a name="tabular-model-programming"></a>테이블 형식 모델 프로그래밍
  테이블 형식 모델은 분석 및 보고 응용 프로그램에서 사용되는 Analysis Services 데이터를 모델링하는 데 관계형 구문을 사용합니다. 이러한 모델은 테이블 형식 모드에 맞게 구성된 Analysis Service 인스턴스에서 실행되며 이때 요청 시 데이터를 집계하고 계산하는 빠른 테이블 검색 및 저장소용 메모리 내 분석 엔진을 사용합니다.  
  
 AMO, ADOMD.NET, XMLA 또는 OLE DB에서 사용하는 개체는 테이블 형식 및 다차원 솔루션에 대한 근본적인 프로그래밍 방식이 동일합니다. 사용자 지정 BI 솔루션의 요구 사항이 테이블 형식 모델 데이터베이스에서 가장 잘 충족되는 경우 임의의 Analysis Services 클라이언트 라이브러리 및 프로그래밍 인터페이스를 사용하여 Analysis Services 인스턴스의 테이블 형식 모델과 응용 프로그램을 통합할 수 있습니다. 코드에 포함된 MDX 또는 DAX를 사용하여 테이블 형식 모델 데이터를 쿼리하고 계산할 수 있습니다.  
  
 이 섹션에서는 프로그래밍 방식으로 테이블 형식 엔터티 및 해당 속성을 사용하여 작업하는 방법에 대해 자세히 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Business Intelligence에 대 한 CSDL 주석 &#40;CSDLBI&#41;](csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [테이블 형식 개체 모델 이해](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [CSDL용 BI 주석에 대한 기술 참조](conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
 [IMDEmbedded 인터페이스](imdembeddeddata-interface.md)  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 모델링 &#40;SSAS 테이블 형식&#41;](../tabular-models/tabular-models-ssas.md)   
 [테이블 형식 모델 디자이너 &#40;SSAS 테이블 형식&#41;](../tabular-model-designer-ssas-tabular.md)  
  
  