---
title: Analysis Services 데이터베이스 문서화 및 스크립트 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 645499bc5311f74ba689b3cd48d2516c01d384fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="document-and-script-an-analysis-services-database"></a>Analysis Services 데이터베이스 문서화 및 스크립트
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스가 배포되면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터베이스 또는 데이터베이스에 포함된 개체의 메타데이터를 XMLA(XML for Analysis) 스크립트로 출력할 수 있습니다. 이 스크립트를 새로운 **XMLA 쿼리 편집기** 창, 파일 또는 클립보드로 출력할 수 있습니다. XMLA에 대한 자세한 내용은 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)를 참조하세요.  
  
 생성된 XMLA 스크립트는 ASSL([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 사용하여 스크립트에 포함된 개체를 정의합니다. CREATE 스크립트를 생성한 경우 결과 XMLA 스크립트는 인스턴스에서 전체 **데이터베이스 구조를 만드는 데 사용할 수 있는 XMLA** Create [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다. ALTER 스크립트를 생성한 경우 결과 XMLA 스크립트는 기존 **데이터베이스 구조를 스크립트 생성 시의 데이터베이스 상태로 복원하는 데 사용할 수 있는 XMLA** Alter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다.  
  
 생성된 XMLA 스크립트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 다음과 같은 방법으로 사용할 수 있습니다.  
  
-   모든 데이터베이스 개체 및 사용 권한을 다시 만들 수 있는 백업 스크립트 유지 관리  
  
-   데이터베이스 개발 코드 만들기 또는 업데이트  
  
-   기존 스키마로부터 테스트 또는 개발 환경 만들기  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 데이터베이스 수정 또는 삭제](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter 요소 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Create 요소 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
