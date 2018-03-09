---
title: "ODBC 대상을 사용하여 데이터 로드 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9675d9f901f47a08cb18ea725e272f054eeb17ac
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="load-data-by-using-the-odbc-destination"></a>ODBC 대상을 사용하여 데이터 로드
  이 절차에서는 ODBC 대상을 사용하여 데이터를 로드하는 방법을 보여 줍니다. ODBC 대상을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-load-data-using-an-odbc-destination"></a>ODBC 대상을 사용하여 데이터를 로드하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 ODBC 대상을 디자인 화면으로 끌어 옵니다.  
  
3.  데이터 흐름 구성 요소의 사용 가능한 출력을 ODBC 대상의 입력으로 끌어 옵니다.  
  
4.  ODBC 대상을 두 번 클릭합니다.  
  
5.  **ODBC 대상 편집기** 대화 상자의 **연결 관리자** 페이지에서 기존 ODBC 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
6.  데이터 액세스 방법을 선택합니다.  
  
    -   **테이블 이름 - 일괄 처리**: 일괄 처리 모드에서 작업하도록 ODBC 대상을 구성하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 **일괄 처리 크기**를 설정할 수 있습니다.  
  
    -   **테이블 이름 - 행 단위**: 각 행을 한 번에 하나씩 대상 테이블에 삽입하도록 ODBC 대상을 구성하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 데이터가 한 번에 한 행씩 테이블로 로드됩니다.  
  
7.  **테이블 또는 뷰 이름** 필드의 목록에서 데이터베이스의 가용 테이블 또는 뷰를 선택하거나 테이블을 식별하는 정규식을 입력합니다. 이 목록에는 처음 1000개의 테이블만 포함됩니다. 데이터베이스에 포함되어 있는 테이블이 1000개를 넘는 경우 테이블 이름의 시작 부분을 입력하거나 와일드카드(*)를 통해 이름의 일부를 입력하여 사용할 테이블을 표시합니다.  
  
8.  **미리 보기** 를 클릭하여 ODBC 대상에서 선택한 테이블의 데이터 행을 200개까지 볼 수 있습니다.  
  
9. **매핑** 을 클릭한 후 **사용 가능한 입력 열** 목록의 열을 **사용 가능한 대상 열** 목록의 열로 끌어서 매핑합니다.  
  
10. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다.  
  
11. **확인**을 클릭합니다.  
  
12. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 대상 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 대상 편집기&#40;매핑 페이지&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  
