---
title: "Analysis Management Objects (AMO)를 사용 하 여 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 41a8625ba173af8ce47cc52a9dac9ca21aa01b41
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="developing-with-analysis-management-objects-amo"></a>AMO(Analysis Management Objects)를 사용하여 개발
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Analysis Management Objects (AMO)가 실행 중인 인스턴스를 관리 하 여 응용 프로그램 프로그래밍 방식으로 액세스 하는 개체의 전체 라이브러리 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.

이 섹션에서는 주요 개체, 주요 개체를 사용하는 방법과 시기 및 주요 개체의 상호 관련 방식에 중점을 두어 AMO 개념에 대해 설명합니다. 특정 개체나 클래스에 대 한 자세한 내용은 다음을 참조 합니다.

- [Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx), 참조 설명서
- [Analysis Services Management Objects (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29), Bing.com 일반 검색으로 합니다.


 **SQL Server 2016의에서 새로운 기능**

AMO는 SQL Server 2016에서 여러 어셈블리로 리팩터링 되었습니다. 제네릭 클래스와 같은 서버, 데이터베이스 및 역할에는 **Microsoft.AnalysisServices.Core** Namespace입니다. 다차원 전용 Api에 남아 [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720.aspx)합니다.

사용자 지정 스크립트와 AMO의 이전 버전에 대해 작성 된 응용 프로그램은 수정 하지 않으면 작업할 계속 됩니다. 그러나 스크립트가 있는 응용 프로그램 SQL Server 2016를 대상으로 하는 구체적으로, 또는 사용자 지정 솔루션을 다시 작성 하는 경우 해야 프로젝트에 새 어셈블리 및 네임 스페이스를 추가 합니다.

## <a name="see-also"></a>관련 항목:
[스크립팅 언어 &#40; Analysis Services를 사용 하 여 개발 ASSL &#41; ](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) 
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
