---
title: ODBC 원본 편집기 (열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2e7a9fb71dca2e99bebe3f23486ff6331bd843de
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387711"
---
# <a name="odbc-source-editor-columns-page"></a>ODBC 원본 편집기(열 페이지)
  **ODBC 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
 ODBC 원본에 대한 자세한 내용은 [ODBC Source](data-flow/odbc-source.md)을 참조하십시오.  
  
## <a name="task-list"></a>작업 목록  
 **ODBC 원본 편집기의 열 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 ODBC 원본이 있는 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ODBC 원본을 두 번 클릭합니다.  
  
3.  **ODBC 원본 편집기**에서 **열**을 클릭합니다.  
  
## <a name="options"></a>변수  
  
### <a name="available-external-columns"></a>사용 가능한 외부 열  
 데이터 원본에서 사용 가능한 외부 열의 목록입니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다. 원본에서 사용할 열을 선택합니다. 선택한 열이 선택 순서대로 **외부 열** 목록에 추가됩니다.  
  
 모든 열을 선택하려면 **모두 선택** 확인란을 선택합니다.  
  
### <a name="external-column"></a>외부 열  
 ODBC 원본의 데이터를 사용하는 구성 요소를 구성할 때 표시되는 순서로 된 외부(원본) 열의 뷰입니다.  
  
### <a name="output-column"></a>출력 열  
 각 출력 열의 고유 이름을 입력합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 입력한 이름은 SSIS 디자이너에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
