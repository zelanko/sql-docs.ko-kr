---
title: CDC 원본 편집기 (오류 출력 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cc9a22330adc00566f18250feba330046c468c0f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079087"
---
# <a name="cdc-source-editor-error-output-page"></a>CDC 원본 편집기(오류 출력 페이지)
  **CDC 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택할 수 있습니다.  
  
 CDC 원본에 대한 자세한 내용은 [CDC Source](data-flow/cdc-source.md)을 참조하십시오.  
  
## <a name="task-list"></a>작업 목록  
 **CDC 원본 편집기 오류 출력 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 CDC 원본이 있는 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 CDC 원본을 두 번 클릭합니다.  
  
3.  **CDC 원본 편집기**에서 **오류 출력**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **CDC 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
 **오류**  
 CDC 원본에서 흐름의 오류를 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **잘림**  
 CDC 원본에서 흐름의 잘림을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 사용되지 않습니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 CDC 원본에서 선택한 모든 셀을 처리하는 방법을 선택합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="error-handling-options"></a>오류 처리 옵션  
 다음 옵션을 사용하여 CDC 원본에서 오류 및 잘림을 처리하는 방법을 구성할 수 있습니다.  
  
 **구성 요소 실패**  
 오류 또는 잘림이 발생하면 데이터 흐름 태스크가 실패합니다. 이것이 기본 동작입니다.  
  
 **오류 무시**  
 오류 또는 잘림이 무시되고 데이터 행이 CDC 원본 출력으로 전달됩니다.  
  
 **흐름 리디렉션**  
 오류 또는 잘림 데이터 행이 CDC 원본의 오류 출력으로 전달됩니다. 이 경우에는 CDC 원본 오류 처리가 사용됩니다. 자세한 내용은 [CDC Source](data-flow/cdc-source.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CDC 원본 편집기 &#40;연결 관리자 페이지&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [CDC 원본 편집기 &#40;열 페이지&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)  
  
  