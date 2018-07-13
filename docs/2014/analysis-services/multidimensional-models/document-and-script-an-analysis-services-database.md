---
title: Analysis Services 데이터베이스 문서화 및 스크립트 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d46180c78befec8a55f03d2064aaa6b94e2ba6a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165496"
---
# <a name="document-and-script-an-analysis-services-database"></a>Analysis Services 데이터베이스 문서화 및 스크립트
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스가 배포되면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터베이스 또는 데이터베이스에 포함된 개체의 메타데이터를 XMLA(XML for Analysis) 스크립트로 출력할 수 있습니다. 이 스크립트를 새로운 **XMLA 쿼리 편집기** 창, 파일 또는 클립보드로 출력할 수 있습니다. XMLA에 대 한 자세한 내용은 참조 하세요. [Analysis Services Scripting Language &#40;ASSL&#41; 참조](../scripting/analysis-services-scripting-language-assl-for-xmla.md)합니다.  
  
 생성된 XMLA 스크립트는 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 사용하여 스크립트에 포함된 개체를 정의합니다. CREATE 스크립트를 생성한 경우 결과 XMLA 스크립트는 인스턴스에서 전체 **데이터베이스 구조를 만드는 데 사용할 수 있는 XMLA** Create [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다. ALTER 스크립트를 생성한 경우 결과 XMLA 스크립트는 기존 **데이터베이스 구조를 스크립트 생성 시의 데이터베이스 상태로 복원하는 데 사용할 수 있는 XMLA** Alter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다.  
  
 생성된 XMLA 스크립트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 다음과 같은 방법으로 사용할 수 있습니다.  
  
-   모든 데이터베이스 개체 및 사용 권한을 다시 만들 수 있는 백업 스크립트 유지 관리  
  
-   데이터베이스 개발 코드 만들기 또는 업데이트  
  
-   기존 스키마로부터 테스트 또는 개발 환경 만들기  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 데이터베이스 수정 또는 삭제](modify-or-delete-an-analysis-services-database.md)   
 [Alter 요소 &#40;XMLA&#41;](../xmla/xml-elements-commands/alter-element-xmla.md)   
 [요소를 만들 &#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md)  
  
  
