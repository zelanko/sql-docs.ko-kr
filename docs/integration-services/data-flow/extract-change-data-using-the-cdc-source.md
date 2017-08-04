---
title: "CDC 원본을 사용 하 여 변경 데이터 추출 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 343efa882f37276c6921edc72d2bf1e615ff1a18
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="extract-change-data-using-the-cdc-source"></a>CDC 원본을 사용하여 변경 데이터 추출
  CDC 원본을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 CDC 제어 태스크가 이미 들어 있어야 합니다.  
  
 CDC 제어 태스크에 대한 자세한 내용은 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)를 참조하십시오.  
  
 CDC 원본에 대한 자세한 내용은 [CDC Source](../../integration-services/data-flow/cdc-source.md)을 참조하십시오.  
  
### <a name="to-extract-change-data-using-a-cdc-source"></a>CDC 원본을 사용하여 변경 데이터를 추출하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 CDC 원본을 디자인 화면으로 끌어 옵니다.  
  
4.  CDC 원본을 두 번 클릭합니다.  
  
5.  **CDC 원본 편집기** 대화 상자의 **연결 관리자** 페이지에 있는 목록에서 기존 ADO.NET 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다. 연결은 읽을 변경 테이블을 포함하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결이어야 합니다.  
  
6.  변경 내용을 처리할 **CDC 테이블** 을 선택합니다.  
  
7.  읽을 CDC 테이블이 있는 **CDC 캡처 인스턴스** 의 이름을 선택하거나 입력합니다.  
  
     캡처된 원본 테이블에는 스키마 변경을 통해 테이블 정의의 원활한 전환을 처리하도록 하나 또는 두 개의 캡처된 인스턴스가 포함되어 있을 수 있습니다. 캡처할 원본 테이블에 대해 두 개 이상의 캡처 인스턴스가 정의되어 있으면 여기에서 사용할 캡처 인스턴스를 선택합니다. 테이블 [schema]에 대 한 기본 캡처 인스턴스 이름입니다. [table] \<스키마 > _\<테이블 > 했지만 해당 사용 중인 실제 캡처 인스턴스 이름은 다를 수 있습니다. 읽은 실제 테이블은 CDC 테이블인 **cdc.\< 캡처 인스턴스 > _CT**합니다.  
  
8.  처리 요구를 처리할 최적의 처리 모드를 선택합니다. 가능한 옵션은 아래와 같습니다.  
  
    -   **모두**: **업데이트 전** 값이 없는 현재 CDC 범위의 변경 내용을 반환합니다.  
  
    -   **이전 값이 포함된 모두**: 이전 값(**업데이트 전**)을 포함한 현재 CDC 처리 범위의 변경 내용을 반환합니다. 각 업데이트 작업에 대해 두 행이 있습니다. 이 중 한 행에는 업데이트 전 값이 포함되어 있고 다른 한 행에는 업데이트 후 값이 포함되어 있습니다.  
  
    -   **순 변경 내용**: 현재 CDC 처리 범위에서 수정된 원본 행당 하나의 변경 행만 반환합니다. 원본 행이 여러 번 업데이트된 경우에는 결합된 변경 내용이 생성됩니다. 예를 들어 삽입+업데이트는 단일 업데이트로 생성되고 업데이트+삭제는 단일 삭제로 생성됩니다. 순 변경 내용 처리 모드에서 작업할 경우 단일 원본 행이 두 개 이상의 출력에 나타나므로 변경 내용을 삭제, 삽입 및 업데이트 출력으로 분할하고 해당 출력을 병렬로 처리할 수 있습니다.  
  
    -   **업데이트 마스크를 사용한 순**:이 모드는 일반 Net 모드와 유사 하지만 이름 패턴이 인 부울 열도 추가 **__ $\<열 이름 >\__Changed** 행을 변경 하는 현재에서 변경 된 열을 나타내는입니다.  
  
    -   **병합을 사용한 순 변경 내용**: 이 모드는 일반적인 순 변경 내용 모드와 비슷하지만 삽입 및 업데이트 작업을 사용할 경우 단일 병합 작업으로 병합됩니다(UPSERT).  
  
9. 현재 CDC 컨텍스트에 대한 CDC 상태를 유지 관리하는 SSIS 문자열 패키지 변수를 선택합니다. CDC 상태 변수에 대한 자세한 내용은 [상태 변수 정의](../../integration-services/data-flow/define-a-state-variable.md)를 참조하세요.  
  
10. **__$reprocessing** 이라는 특수 출력 열을 만들려면 **재처리 표시기 열 포함**확인란을 선택합니다. CDC 처리 범위가 초기 처리 범위(초기 로드 기간에 해당하는 LSN의 범위)와 겹치거나 이전 실행의 오류 발생 후 CDC 처리 범위가 다시 처리되는 경우 이 열 값은 **true** 입니다. 이 표시기 열을 사용하면 변경 내용을 다시 처리할 때 SSIS 개발자가 오류를 다르게 처리할 수 있습니다. 예를 들어 존재하지 않는 행의 삭제와 중복 키에 대해 실패한 삽입과 같은 동작은 무시할 수 있습니다.  
  
     자세한 내용은 [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md)을(를) 참조하세요.  
  
11. 외부 및 출력 열 사이의 매핑을 업데이트하려면 **열** 을 클릭하고 **외부 열** 목록에서 다른 열을 선택합니다.  
  
12. 필요에 따라 **출력 열** 목록에서 값을 삭제하여 출력 열의 값을 업데이트합니다.  
  
13. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다.  
  
14. **미리 보기** 를 클릭하면 CDC 원본에 의해 추출된 최대 200개의 데이터 행을 볼 수 있습니다.  
  
15. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CDC 원본 편집기 &#40; 연결 관리자 페이지 &#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [CDC 원본 편집기 &#40; 열 페이지 &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [CDC 원본 편집기 &#40; 오류 출력 페이지 &#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  
