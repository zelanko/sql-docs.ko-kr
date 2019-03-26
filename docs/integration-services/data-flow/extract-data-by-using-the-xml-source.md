---
title: XML 원본을 사용하여 데이터 추출 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe29c2bff8c3eb45fc987993714a035f6d4889d5
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270625"
---
# <a name="extract-data-by-using-the-xml-source"></a>XML 원본을 사용하여 데이터 추출
  XML 원본을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크가 이미 들어 있어야 합니다.  
  
### <a name="to-extract-data-using-an-xml-source"></a>XML 원본을 사용하여 데이터를 추출하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 XML 원본을 디자인 화면으로 끌어 옵니다.  
  
4.  XML 원본을 두 번 클릭합니다.  
  
5.  **XML 원본 편집기**의 **연결 관리자** 페이지에서 데이터 액세스 모드를 선택합니다.  
  
    -   **XML 파일 위치** 액세스 모드의 경우 **찾아보기** 를 클릭하여 XML 파일이 들어 있는 폴더를 찾습니다.  
  
    -   **변수를 사용한 XML 파일** 액세스 모드의 경우 XML 파일의 경로가 들어 있는 사용자 정의 변수를 선택합니다.  
  
    -   **변수를 사용한 XML 데이터** 액세스 모드의 경우 XML 데이터가 들어 있는 사용자 정의 변수를 선택합니다.  
  
    > [!NOTE]  
    >  XML 원본이 포함된 데이터 흐름 태스크의 범위나 패키지 범위에 변수가 정의되어 있어야 하며, 변수에 문자열 데이터 형식이 들어 있어야 합니다.  
  
6.  XML 문서에 스키마 정보가 포함되는 경우 선택적으로 **인라인 스키마 사용** 을 선택합니다.  
  
7.  XML 파일에 대해 외부 XSD(XML 스키마 정의 언어) 스키마를 지정하려면 다음 중 하나를 수행하십시오.  
  
    -   **찾아보기** 를 클릭하여 기존 XSD 파일을 찾습니다.  
  
    -   **XSD 생성** 을 클릭하여 XML 파일로부터 XSD를 만듭니다.  
  
8.  출력 열의 이름을 업데이트하려면 **열** 을 클릭하고 **출력 열** 목록에서 값을 편집합니다.  
  
9. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다. 자세한 내용은 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 원본](../../integration-services/data-flow/xml-source.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../integration-services/control-flow/data-flow-task.md)  
  
  
