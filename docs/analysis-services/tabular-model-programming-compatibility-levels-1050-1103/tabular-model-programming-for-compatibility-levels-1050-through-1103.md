---
title: Analysis Services 테이블 형식 모델 프로그래밍 호환성 수준 1050 ~ 1103에 대 한 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe2ce43ffb5d2c5be0afb39931f231d2f0d24e14
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025294"
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>호환성 수준 1050~1103에 대한 테이블 형식 모델 프로그래밍
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  테이블 형식 모델은 분석 및 보고 애플리케이션에서 사용되는 Analysis Services 데이터를 모델링하는 데 관계형 구문을 사용합니다. 이러한 모델은 테이블 형식 모드에 맞게 구성된 Analysis Service 인스턴스에서 실행되며 이때 요청 시 데이터를 집계하고 계산하는 빠른 테이블 검색 및 스토리지용 메모리 내 분석 엔진을 사용합니다.  
  
 사용자 지정 BI 솔루션의 요구 사항이 테이블 형식 모델 데이터베이스에서 가장 잘 충족되는 경우 임의의 Analysis Services 클라이언트 라이브러리 및 프로그래밍 인터페이스를 사용하여 Analysis Services 인스턴스의 테이블 형식 모델과 애플리케이션을 통합할 수 있습니다. 코드에 포함된 MDX 또는 DAX를 사용하여 테이블 형식 모델 데이터를 쿼리하고 계산할 수 있습니다.  
  
 호환성 수준 1050-1103, 특정 모델의 Analysis Services의 이전 버전에서 만든 테이블 형식 모델 AMO, ADOMD.NET, XMLA 또는 OLE DB에서 프로그래밍 방식으로 작업 하는 개체는 테이블 형식 모두에 대해 기본적으로 동일 하 고 다차원 솔루션입니다. 특히, 호환성 수준 1050 ~ 1103 테이블 형식 모델에 대 한 다차원 모델에 정의 된 개체 메타 데이터도 사용 됩니다.  
  
 SQL Server 2016 부터는 테이블 형식 모델 작성 하거나 수 테이블 형식 메타 데이터를 사용 하 여 모델을 정의 하는 1200 이상 호환성 수준으로 업그레이드 합니다. 이 수준에서 메타 데이터 및 프로그래밍 기능은 근본적으로 다릅니다. 참조 [테이블 형식 모델 프로그래밍 호환성 수준 1200 이상](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) 하 고 [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md) 자세한 내용은 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [비즈니스 인텔리전스에 대한 CSDL 주석&#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
 [수준 1050 ~ 1103 호환성에서 테이블 형식 개체 모델 이해](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [CSDL용 BI 주석에 대한 기술 참조](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl)  
  

[IMDEmbeddedData 인터페이스](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
