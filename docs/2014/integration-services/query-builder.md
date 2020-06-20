---
title: 쿼리 작성기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1a393352f7ec0f9384ed2d30b2909c9d9f2c1dc0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964623"
---
# <a name="query-builder"></a>쿼리 작성기
  **쿼리 작성기** 대화 상자를 사용하여 SQL 실행 태스크, OLE DB 원본 및 대상, 조회 변환에서 사용할 쿼리를 만들 수 있습니다.  
  
 쿼리 작성기를 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   **쿼리의 그래픽 표시 또는 SQL 명령 작업** 쿼리 작성기에는 쿼리를 그래픽으로 표시하는 창과 쿼리의 SQL 텍스트를 표시하는 텍스트 창이 있습니다. 그래픽 창이나 텍스트 창에서 작업할 수 있습니다. 쿼리 작성기는 항상 최신 상태를 유지하도록 뷰를 동기화합니다.  
  
-   **관련 테이블 조인** 둘 이상의 테이블을 쿼리에 추가하면 쿼리 작성기는 테이블이 관련되는 방법과 적절한 조인 명령을 생성하는 방법을 자동으로 결정합니다.  
  
-   **데이터베이스 쿼리 또는 업데이트** 쿼리 작성기에서 Transact-SQL SELECT 문을 사용하여 데이터를 반환하고 데이터베이스에서 레코드를 업데이트, 추가 또는 삭제하는 쿼리를 만들 수 있습니다.  
  
-   **즉시 결과를 보고 편집** 쿼리를 실행하고 레코드 집합을 표 형태로 처리하여 데이터베이스의 레코드를 스크롤하고 편집할 수 있습니다.  
  
 **쿼리 작성기** 대화 상자의 그래픽 도구를 사용하면 끌어서 놓기 작업을 통해 쿼리를 만들 수 있습니다. 기본적으로 쿼리 작성기 대화 상자에서 SELECT 쿼리를 생성하지만 사용자가 INSERT, UPDATE 또는 DELETE 쿼리를 작성할 수도 있습니다. 모든 유형의 SQL 문은 **쿼리 작성기** 대화 상자에서 구문을 분석하고 실행할 수 있습니다. 패키지의 SQL 문에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 쿼리](integration-services-ssis-queries.md)를 참조하세요.  
  
 Transact-SQL 언어와 해당 구문에 대한 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)를 참조하세요.  
  
 쿼리에 변수를 사용하여 입력 매개 변수에 값을 제공하고 출력 매개 변수의 값을 캡처하며 반환 코드를 저장할 수도 있습니다. 패키지에서 사용하는 쿼리에서 변수를 사용하는 방법에 대한 자세한 내용은 [SQL 실행 태스크](control-flow/execute-sql-task.md), [OLE DB 원본](data-flow/ole-db-source.md) 및 [Integration Services&#40;SSIS&#41; 쿼리](integration-services-ssis-queries.md)를 참조하세요. SQL 실행 태스크에서 변수를 사용하는 방법에 대한 자세한 내용은 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) 및 [SQL 실행 태스크의 결과 집합](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)을 참조하세요.  
  
 조회 및 유사 항목 조회 변환에서도 매개 변수와 반환 코드에 변수를 사용할 수 있습니다. OLE DB 원본에 대한 정보는 이러한 두 변환에도 적용됩니다.  
  
## <a name="options"></a>옵션  
 **]**  
 도구 모음을 사용하여 데이터 세트를 관리하고, 표시할 창을 선택하고, 쿼리 함수를 제어할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**다이어그램 창 표시/숨기기**|**다이어그램** 창을 표시하거나 숨깁니다.|  
|**표 형태 창 표시/숨기기**|**표 형태** 창을 표시하거나 숨깁니다.|  
|**SQL 창 표시/숨기기**|**SQL** 창을 표시 하거나 숨깁니다.|  
|**결과 창 표시/숨기기**|**결과** 창을 표시하거나 숨깁니다.|  
|**실행**|쿼리를 실행합니다. 결과는 결과 창에 표시됩니다.|  
|**SQL 검증**|SQL 문이 유효한지 여부를 확인합니다.|  
|**오름차순 정렬**|표 형태 창에서 선택한 열의 출력 행을 오름차순으로 정렬합니다.|  
|**내림차순 정렬**|표 형태 창에서 선택한 열의 출력 행을 내림차순으로 정렬합니다.|  
|**필터 제거**|표 형태 창에서 열 이름을 선택한 다음 **필터 제거** 를 클릭하여 해당 열에 대한 정렬 조건을 제거합니다.|  
|**Group By 사용**|쿼리에 GROUP BY 기능을 추가합니다.|  
|**테이블 추가**|쿼리에 새 테이블을 추가합니다.|  
  
 **쿼리 정의**  
 쿼리 정의에서는 쿼리를 정의 및 테스트할 수 있는 도구 모음 및 창을 사용할 수 있습니다.  
  
|창|Description|  
|----------|-----------------|  
|**다이어그램** 창|쿼리를 다이어그램에 표시합니다. 다이어그램은 쿼리에 포함된 테이블과 이러한 테이블의 조인 방법을 보여 줍니다. 쿼리 출력에 열을 추가하거나 제거하려면 테이블에서 해당 열의 옆에 있는 확인란을 선택하거나 선택을 취소합니다.<br /><br /> 쿼리에 테이블을 추가하면 쿼리 작성기에서 테이블의 키에 따라 테이블을 기반으로 테이블 간의 조인을 만듭니다. 조인을 추가하려면 한 테이블의 필드를 다른 테이블의 필드로 끌어 놓습니다. 조인을 관리하려면 해당 조인을 마우스 오른쪽 단추로 클릭한 다음 메뉴 옵션을 선택합니다.<br /><br /> **다이어그램** 창을 마우스 오른쪽 단추로 클릭 하 여 테이블을 추가 또는 제거 하 고, 모든 테이블을 선택 하 고, 창을 표시 하거나 숨깁니다.|  
|**표 형태** 창|쿼리를 표에 표시합니다. 이 창을 사용하여 쿼리에서 열을 추가 및 제거하고 각 열의 설정을 변경할 수 있습니다.|  
|**SQL** 창|쿼리를 SQL 텍스트로 표시합니다. **다이어그램** 창 및 **표 형태** 창에서 변경한 내용은 이 창에 나타나고 여기에서 변경한 내용은 **다이어그램** 창 및 **표 형태** 창에 나타납니다.|  
|**결과** 창|도구 모음에서 **실행** 을 클릭하면 쿼리 결과가 표시됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL 실행 태스크](control-flow/execute-sql-task.md)   
 [OLE DB 소스](data-flow/ole-db-source.md)   
 [OLE DB 대상](data-flow/ole-db-destination.md)   
 [조회 변환](data-flow/transformations/lookup-transformation.md)   
 [SSIS&#41; 쿼리 Integration Services &#40;](integration-services-ssis-queries.md)   
 [Integration Services 패키지의 MERGE](control-flow/merge-in-integration-services-packages.md)  
  
  
