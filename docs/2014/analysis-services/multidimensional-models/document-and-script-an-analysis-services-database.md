---
title: Analysis Services 데이터베이스 문서화 및 스크립팅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9284073781a91b21d588684b9071e6179a815613
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075123"
---
# <a name="document-and-script-an-analysis-services-database"></a>Analysis Services 데이터베이스 문서화 및 스크립트
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스가 배포되면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터베이스 또는 데이터베이스에 포함된 개체의 메타데이터를 XMLA(XML for Analysis) 스크립트로 출력할 수 있습니다. 이 스크립트를 새로운 **XMLA 쿼리 편집기** 창, 파일 또는 클립보드로 출력할 수 있습니다. XMLA에 대 한 자세한 내용은 [Analysis Services 스크립팅 언어 &#40;인&#41; 참조](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)를 참조 하세요.  
  
 생성된 XMLA 스크립트는 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 요소를 사용하여 스크립트에 포함된 개체를 정의합니다. CREATE 스크립트를 생성한 경우 결과 XMLA 스크립트는 인스턴스에서 전체 **데이터베이스 구조를 만드는 데 사용할 수 있는 XMLA** Create [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다. ALTER 스크립트를 생성한 경우 결과 XMLA 스크립트는 기존 **데이터베이스 구조를 스크립트 생성 시의 데이터베이스 상태로 복원하는 데 사용할 수 있는 XMLA** Alter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령과 ASSL 요소를 포함합니다.  
  
 생성된 XMLA 스크립트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 다음과 같은 방법으로 사용할 수 있습니다.  
  
-   모든 데이터베이스 개체 및 사용 권한을 다시 만들 수 있는 백업 스크립트 유지 관리  
  
-   데이터베이스 개발 코드 만들기 또는 업데이트  
  
-   기존 스키마로부터 테스트 또는 개발 환경 만들기  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 데이터베이스 수정 또는 삭제](modify-or-delete-an-analysis-services-database.md)   
 [Alter Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Create 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
