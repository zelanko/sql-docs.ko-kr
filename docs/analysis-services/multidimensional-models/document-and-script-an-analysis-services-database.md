---
title: "Analysis Services 데이터베이스 문서화 및 스크립트 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ceb4145368b88ecc523dc7c5a3b96406bb383c4a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="document-and-script-an-analysis-services-database"></a>Analysis Services 데이터베이스 문서화 및 스크립트
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]이후에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 배포를 사용할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스에 포함 된 개체 또는 데이터베이스의 메타 데이터를 출력 하려면 XML for Analysis (XMLA) 스크립트로 합니다. 이 스크립트를 새로운 **XMLA 쿼리 편집기** 창, 파일 또는 클립보드로 출력할 수 있습니다. XMLA에 대한 자세한 내용은 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)를 참조하세요.  
  
 생성된 XMLA 스크립트는 ASSL([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 사용하여 스크립트에 포함된 개체를 정의합니다. CREATE 스크립트를 생성한 경우 결과 XMLA 스크립트는 인스턴스에서 전체 **데이터베이스 구조를 만드는 데 사용할 수 있는 XMLA** Create [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다. ALTER 스크립트를 생성한 경우 결과 XMLA 스크립트는 기존 **데이터베이스 구조를 스크립트 생성 시의 데이터베이스 상태로 복원하는 데 사용할 수 있는 XMLA** Alter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다.  
  
 생성된 XMLA 스크립트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 다음과 같은 방법으로 사용할 수 있습니다.  
  
-   모든 데이터베이스 개체 및 사용 권한을 다시 만들 수 있는 백업 스크립트 유지 관리  
  
-   데이터베이스 개발 코드 만들기 또는 업데이트  
  
-   기존 스키마로부터 테스트 또는 개발 환경 만들기  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 데이터베이스 수정 또는 삭제](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [요소 &#40; 만들기 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
