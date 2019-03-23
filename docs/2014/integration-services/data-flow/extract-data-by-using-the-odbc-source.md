---
title: ODBC 원본을 사용하여 데이터 추출 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8ecb517174c8cd8189ad2f7382c774df3545620
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376121"
---
# <a name="extract-data-by-using-the-odbc-source"></a>ODBC 원본을 사용하여 데이터 추출
  이 절차에서는 ODBC 원본을 사용하여 데이터를 추출하는 방법을 설명합니다. ODBC 원본을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크가 이미 들어 있어야 합니다.  
  
### <a name="to-extract-data-using-an-odbc-source"></a>ODBC 원본을 사용하여 데이터를 추출하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 ODBC 원본을 디자인 화면으로 끌어 옵니다.  
  
3.  ODBC 원본을 두 번 클릭합니다.  
  
4.  **ODBC 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 기존 ODBC 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다.  
  
5.  데이터 액세스 방법을 선택합니다.  
  
    -   **테이블 이름**: 데이터베이스의 테이블 또는 뷰를 선택하거나 ODBC 연결 관리자가 연결될 테이블을 식별하는 정규식을 입력합니다.  
  
         이 목록에는 처음 1000개의 테이블만 포함되어 있습니다. 데이터베이스에 포함되어 있는 테이블이 1000개를 넘는 경우 테이블 이름의 시작 부분을 입력하거나 와일드카드(*)를 통해 이름의 일부를 입력하여 사용할 테이블을 표시합니다.  
  
    -   **SQL 명령**: SQL 명령을 입력 하거나 클릭 **찾아보기** 텍스트 파일에서 SQL 쿼리를 로드 합니다.  
  
6.  **미리 보기** 를 클릭하면 ODBC 원본에 의해 추출된 최대 200개의 데이터 행을 볼 수 있습니다.  
  
7.  외부 및 출력 열 사이의 매핑을 업데이트하려면 **열** 을 클릭하고 **외부 열** 목록에서 다른 열을 선택합니다.  
  
8.  필요에 따라 **출력 열** 목록에서 값을 편집하여 출력 열의 이름을 업데이트합니다.  
  
9. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../odbc-source-editor-connection-manager-page.md)   
 [ODBC 원본 편집기&#40;열 페이지&#41;](../odbc-source-editor-columns-page.md)   
 [ODBC 원본 편집기&#40;오류 출력 페이지&#41;](../odbc-source-editor-error-output-page.md)  
  
  
