---
title: 결과 창에서 데이터 작업(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5f3dffc7661fc5843dcd220f27beb1117a85729
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63313768"
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>결과 창에서 데이터 작업(Visual Database Tools)
  쿼리나 뷰를 실행하면 결과 창에 그 결과가 표시됩니다. 이러한 결과를 사용하여 작업할 수 있습니다. 예를 들어 행을 추가 및 삭제하고 데이터를 입력 또는 변경하며 수많은 결과 집합 사이를 쉽게 이동할 수 있습니다.  
  
 다음은 결과 집합을 효율적으로 사용하고 문제를 방지하는 데 도움이 되는 정보입니다.  
  
## <a name="returning-the-results-set"></a>결과 집합 반환  
 쿼리나 뷰의 결과를 반환할 수 있고 결과 창만 열지 또는 모든 창을 열지 선택할 수 있습니다. 두 경우 모두 쿼리 및 뷰 디자이너에서 쿼리나 뷰가 열립니다. 둘 사이의 차이점은 결과 창만 열리거나 아니면 옵션 대화 상자에서 선택한 모든 창이 열린다는 점뿐입니다. 기본적으로는 네 개의 창(결과, SQL, 다이어그램 및 조건)이 모두 열립니다.  
  
 자세한 내용은 [쿼리 열기&#40;Visual Database Tools&#41;](visual-database-tools.md)를 참조하세요.  
  
 다른 결과 집합을 반환하거나 다른 순서로 레코드를 반환하도록 쿼리나 뷰의 디자인을 변경하려면 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)에 나열된 항목을 참조하세요.  
  
 결과 집합을 모두 반환할지 아니면 일부만 반환할지 결정하는 데는 두 가지 방법을 사용할 수 있습니다. 즉, 실행 중인 쿼리를 중지하거나 반환할 결과의 양을 미리 선택한 다음 쿼리를 실행하면 됩니다.  
  
## <a name="navigating-in-the-results-pane"></a>결과 창에서 탐색  
 결과 창의 아래쪽에 있는 탐색 모음을 사용하면 레코드를 빠르게 탐색할 수 있습니다.  
  
 이 탐색 모음에는 첫 번째 레코드와 마지막 레코드, 다음 레코드와 이전 레코드 또는 특정 레코드로 이동하기 위한 단추가 있습니다.  
  
 특정 레코드로 이동하려면 탐색 모음의 입력란에 원하는 행 번호를 입력한 다음 Enter 키를 누릅니다.  
  
 쿼리 및 뷰 디자이너에서 바로 가기 키를 사용하는 방법에 대한 자세한 내용은 [쿼리 및 뷰 디자이너에서 탐색&#40;Visual Database Tools&#41;](navigate-in-the-query-and-view-designer-visual-database-tools.md)을 참조하세요.  
  
## <a name="committing-changes-to-the-database"></a>데이터베이스에 변경 내용 커밋  
 결과 창에는 낙관적 동시성 제어가 사용되므로 표에는 완전한 실시간 보기 대신 데이터베이스의 데이터 복사본이 표시됩니다. 따라서 사용자가 행에서 포커스를 옮긴 후에만 변경 내용이 데이터베이스에 커밋됩니다. 이와 같은 방식으로 여러 사용자가 동시에 데이터베이스를 사용하여 작업할 수 있습니다. 충돌이 발생하는 경우(예: 현재 사용자가 변경한 것과 동일한 행을 다른 사용자가 변경하고 현재 사용자가 커밋하기 전에 이를 먼저 데이터베이스에 커밋한 경우)에는 충돌 사실과 해결 방법을 제안하는 메시지가 표시됩니다.  
  
## <a name="undo-changes-using-esc"></a>Esc 키를 사용하여 변경 취소  
 변경 내용을 데이터베이스에 커밋하지 않은 경우에만 변경 내용을 실행 취소할 수 있습니다. 레코드에서 포커스를 옮기지 않았거나 레코드에서 포커스를 옮기려 했지만 변경 내용을 커밋할 수 없다는 오류 메시지가 표시되는 경우에는 데이터가 커밋되지 않습니다. 이와 같이 변경 내용이 커밋되지 않은 경우 Esc 키를 사용하여 변경 내용을 실행 취소할 수 있습니다.  
  
 한 행의 변경 내용을 모두 실행 취소하려면 해당 행에서 편집하지 않은 셀로 이동한 다음 Esc 키를 누릅니다.  
  
 편집한 특정 셀의 변경 내용을 실행 취소하려면 해당 셀로 이동한 다음 Esc 키를 누릅니다.  
  
## <a name="adding-or-deleting-data-in-the-database"></a>데이터베이스에서 데이터 추가 또는 삭제  
 데이터베이스 디자인의 작동 방식을 확인하기 위해 데이터베이스에 샘플 데이터를 추가해 볼 수 있습니다. 이러한 샘플 데이터는 결과 창에 직접 입력하거나 메모장 또는 Excel 같은 다른 프로그램에서 복사하여 결과 창에 붙여넣을 수 있습니다.  
  
 결과 창에 행을 복사하여 붙여넣을 수 있을 뿐만 아니라 새 레코드를 추가하거나 기존 레코드를 수정 또는 삭제할 수도 있습니다. 자세한 내용은 [결과 창에서 새 행 추가&#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md), [결과 창에서 행 삭제&#40;Visual Database Tools&#41;](delete-rows-in-the-results-pane-visual-database-tools.md) 및 [결과 창에서 행 편집&#40;Visual Database Tools&#41;](edit-rows-in-the-results-pane-visual-database-tools.md)을 참조하세요.  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>NULL 값 및 빈 셀 사용을 위한 팁  
 빈 행을 클릭하여 새 레코드를 추가하는 경우 모든 열의 초기 값은 *NULL*입니다. 열에 null 값이 허용되면 그대로 둘 수 있습니다.  
  
 null 이외의 값을 null로 바꾸려면 대문자로 NULL을 입력합니다. 그러면 이 단어가 결과 창에 기울임 글꼴로 표시됩니다. 이는 사용자가 입력한 값이 문자열이 아닌 null 값으로 인식됨을 의미합니다.  
  
 "null"이라는 문자열을 입력하려면 이 단어를 따옴표 없이 입력합니다. 소문자가 하나라도 포함되어 있으면 그 값은 null 값이 아닌 문자열로 취급됩니다.  
  
 이진 데이터 형식의 열에 대한 값은 기본적으로 NULL 값입니다. 이러한 값은 결과 창에서 변경할 수 없습니다.  
  
 null을 사용하는 대신 빈 공백을 입력하려면 기존 텍스트를 삭제하고 다른 셀로 포커스를 옮깁니다.  
  
## <a name="validating-data"></a>데이터 유효성 확인  
 쿼리 및 뷰 디자이너에서는 열 속성을 기준으로 몇 가지 종류의 데이터에 대한 유효성을 확인할 수 있습니다. 예를 들어, float 데이터 형식의 열에 "abc"를 입력하면 오류가 발생하고 변경 내용이 데이터베이스에 커밋되지 않습니다.  
  
 결과 창에서 작업하는 동안 다이어그램 창을 열고 테이블 또는 테이블 반환 개체의 열 이름 위에 커서를 놓으면 열의 데이터 형식을 바로 확인할 수 있습니다.  
  
> [!NOTE]  
>  결과 창에 표시할 수 있는 텍스트 데이터 형식의 최대 길이는 2,147,483,647입니다.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>결과 집합과 쿼리 정의의 동기화 상태 유지  
 쿼리나 뷰의 결과에 대한 작업을 수행하는 동안 결과 창의 레코드가 쿼리 정의와 동기화되지 않을 수 있습니다. 예를 들어, 테이블에서 다섯 개의 열 중 네 개의 열에 대한 쿼리를 실행한 다음 다이어그램 창을 사용하여 다섯 번째 열을 쿼리 정의에 추가하는 경우 이 다섯 번째 열의 데이터는 결과 창에 자동으로 추가되지 않습니다. 결과 창에 새 쿼리 정의가 반영되도록 하려면 쿼리를 다시 실행해야 합니다.  
  
 결과 창의 오른쪽 아래 모퉁이에 경고 아이콘과 "쿼리가 변경되었습니다."라는 텍스트가 표시되고 이 창의 왼쪽 위 모퉁이에도 아이콘이 표시되므로 결과 집합과 쿼리 정의가 동기화되지 않은 경우 그 사실을 쉽게 확인할 수 있습니다.  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>여러 사용자가 변경한 내용 조정  
 쿼리나 뷰의 결과에 대한 작업을 수행하는 동안 동일한 데이터베이스를 사용하여 작업하는 다른 사용자가 해당 레코드를 변경할 수 있습니다.  
  
 이 경우 충돌이 발생한 셀에서 포커스를 옮길 때 해당 사실을 알리는 메시지가 표시됩니다. 그러면 다른 사용자의 변경 내용을 무시하거나, 다른 사용자의 변경 내용으로 내 결과 창을 업데이트하거나, 충돌하는 변경 내용을 조정하지 않은 채로 결과 창을 계속 편집할 수 있습니다. 충돌하는 변경 내용을 조정하지 않으면 내가 변경한 내용을 데이터베이스에 커밋할 수 없습니다.  
  
## <a name="limitations-in-the-results-pane"></a>결과 창의 제한 사항  
  
### <a name="what-can-not-be-updated"></a>업데이트할 수 없는 항목  
 다음은 결과 창의 데이터를 사용하여 작업을 성공적으로 수행하는 데 도움이 되는 정보입니다.  
  
-   두 개 이상의 테이블이나 뷰의 열이 포함된 쿼리는 업데이트할 수 없습니다.  
  
-   데이터베이스 제약 조건에서 허용하는 경우에만 뷰를 업데이트할 수 있습니다.  
  
-   저장 프로시저를 통해 반환된 결과는 업데이트할 수 없습니다.  
  
-   GROUP BY, DISTINCT 또는 TO XML 절을 사용하는 쿼리나 뷰는 업데이트할 수 없습니다.  
  
-   테이블 반환 함수를 통해 반환되는 결과는 다음과 같은 몇 가지 경우에만 업데이트할 수 있습니다.  
  
-   쿼리 식의 결과인 열의 데이터  
  
-   공급자가 성공적으로 변환하지 못한 데이터  
  
### <a name="what-can-not-be-represented-fully"></a>완전히 표현할 수 없는 항목  
 데이터베이스에서 결과 창으로 반환되는 내용은 현재 사용 중인 데이터 원본의 공급자를 통해 주로 제어됩니다. 모든 데이터베이스 관리 시스템의 데이터를 결과 창에서 항상 변환할 수 있는 것은 아닙니다. 이와 같은 예외적인 경우는 다음과 같습니다.  
  
-   결과 창에서 작업하는 대부분의 사용자에게는 일반적으로 이진 데이터 형식이 유용하지 않으며 이러한 데이터를 다운로드하는 데도 아주 많은 시간이 필요할 수 있습니다. 따라서 * \<이진 데이터>* 또는 *Null*로 표시 됩니다.  
  
-   경우에 따라 전체 자릿수와 소수 자릿수가 유지되지 않을 수 있습니다. 예를 들어 결과 창에서 전체 자릿수를 27까지 지원하는데 데이터의 전체 자릿수가 더 큰 데이터 형식인 경우 데이터를 자르거나 * \<>데이터를 읽을 수 없는 *것으로 표시 될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Visual Database Tools를 &#40;쿼리를 사용 하 여 기본 작업을 수행&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [검색 조건 지정&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
