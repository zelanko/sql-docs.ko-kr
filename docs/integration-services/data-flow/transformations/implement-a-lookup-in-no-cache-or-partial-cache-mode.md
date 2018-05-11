---
title: 캐시 없음 또는 부분 캐시 모드로 조회 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4cfb1b67c43227d8fd27c2536fd762a601651786
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>캐시 없음 또는 부분 캐시 모드로 조회 구현
  부분 캐시 또는 캐시 없음 모드를 사용하여 조회 변환을 구성할 수 있습니다.  
  
-   부분 캐시  
  
     참조 데이터 집합에서 일치하는 항목이 있는 행 및 필요에 따라 데이터베이스에서 일치하는 항목이 없는 행이 캐시에 저장됩니다. 캐시의 메모리 크기를 초과하면 조회 변환은 자동으로 캐시에서 가장 사용 빈도가 낮은 행을 제거합니다.  
  
-   캐시 없음  
  
     캐시에 로드되는 데이터가 없습니다.  
  
 부분 캐시를 선택하든 캐시 없음을 선택하든 OLE DB 연결 관리자를 사용하여 참조 데이터 집합에 연결합니다. 참조 데이터 집합은 조회 변환을 실행하는 동안 테이블, 뷰 또는 SQL 쿼리를 사용하여 생성됩니다.  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>캐시 없음 또는 부분 캐시 모드로 조회 변환을 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 열고 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 조회 변환을 추가합니다.  
  
3.  원본이나 이전 변환에서 연결선을 조회 변환으로 끌어서 조회 변환을 데이터 흐름에 연결합니다.  
  
    > [!NOTE]  
    >  캐시 모드를 사용하지 않도록 구성된 조회 변환이 빈 데이터 필드가 포함된 플랫 파일에 연결되면 이러한 조회 변환의 유효성을 검사하지 못할 수 있습니다. 변환의 유효성 검사 여부는 플랫 파일의 연결 관리자가 Null 값을 유지하도록 구성되었는지 여부에 따라 결정됩니다. 조회 변환의 유효성 검사가 수행되도록 하려면 **플랫 파일 원본 편집기**의 **연결 관리자 페이지**에서 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지** 옵션을 선택합니다.  
  
4.  원본이나 이전 변환을 두 번 클릭하여 구성 요소를 구성합니다.  
  
5.  조회 변환을 두 번 클릭한 다음 **조회 변환 편집기**의 **일반** 페이지에서 **부분 캐시** 또는 **캐시 없음**을 선택합니다.  
  
6.  **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 오류 처리 옵션을 선택합니다.  
  
7.  **연결** 페이지에서, **OLE DB 연결 관리자** 목록에서 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
8.  다음 단계 중 하나를 수행합니다.  
  
    -   **테이블 또는 뷰 사용**을 클릭한 다음 테이블이나 뷰를 선택하거나, **새로 만들기** 를 클릭하여 테이블이나 뷰를 만듭니다.  
  
    -   **SQL 쿼리 결과 사용**을 클릭한 다음 **SQL 명령** 창에 쿼리를 작성합니다.  
  
         —또는—  
  
         **쿼리 작성** 을 클릭하여 **쿼리 작성기** 에서 공급하는 그래픽 도구를 사용하여 쿼리를 작성합니다.  
  
         —또는—  
  
         **찾아보기** 를 클릭하여 파일에서 SQL 문을 가져옵니다.  
  
     SQL 쿼리의 유효성을 검사하려면 **쿼리 구문 분석**을 클릭합니다.  
  
     데이터 예제를 보려면 **미리 보기**를 클릭합니다.  
  
9. **열** 페이지를 클릭한 다음 **사용 가능한 입력 열** 목록에 있는 하나 이상의 열을 **사용 가능한 조회 열** 목록에 있는 열로 끌어 옵니다.  
  
    > [!NOTE]  
    >  조회 변환은 이름과 데이터 형식이 같은 열을 자동으로 매핑합니다.  
  
    > [!NOTE]  
    >  열을 매핑하려면 데이터 형식이 일치해야 합니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
10. 다음 단계를 수행하여 출력에 조회 열을 포함시킵니다.  
  
    1.  **사용 가능한 조회 열** 목록에서 열을 선택합니다.  
  
    2.  **조회 작업** 목록에서 조회 열의 값으로 입력 열의 값을 교체하거나 새 열에 기록할지 여부를 지정합니다.  
  
11. 5단계에서 **부분 캐시** 를 선택했으면 **고급** 페이지에서 다음 캐시 옵션을 설정합니다.  
  
    -   **캐시 크기(32비트)** 목록에서 32비트 환경에 대한 캐시 크기를 선택합니다.  
  
    -   **캐시 크기(64비트)** 목록에서 64비트 환경에 대한 캐시 크기를 선택합니다.  
  
    -   참조에서 일치하는 항목이 없는 행을 캐시하려면 **일치하는 항목이 없는 행에 캐시 사용**을 선택합니다.  
  
    -   **캐시에서 할당** 목록에서 일치하는 항목이 없는 행을 저장하는 데 사용할 캐시 비율을 선택합니다.  
  
12. 참조 데이터 집합을 생성하는 SQL 문을 수정하려면 **SQL 문 수정**을 선택하고 입력란에 표시되는 SQL 문을 변경합니다.  
  
     문에 매개 변수가 포함되는 경우에는 **매개 변수** 를 클릭하여 입력 열에 매개 변수를 매핑합니다.  
  
    > [!NOTE]  
    >  이 페이지에서 지정하는 선택적 SQL 문이 **조회 변환 편집기** 의 **연결**페이지에서 지정한 테이블 이름을 재정의하고 대체합니다.  
  
13. 오류 출력을 구성하려면 **오류 출력** 페이지를 클릭하고 오류 처리 옵션을 설정합니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)를 참조하세요.  
  
14. 조회 변환의 변경 내용을 저장한 다음 패키지를 실행하려면 **확인** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
