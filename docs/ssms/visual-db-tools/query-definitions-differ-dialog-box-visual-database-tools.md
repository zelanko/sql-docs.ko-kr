---
title: 쿼리 정의 다름 대화 상자
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 01e45f907f85ed02443502e899e11181a73f20ab
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255318"
---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>쿼리 정의 다름 대화 상자(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 대화 상자에는 다이어그램 창과 조건 창에서 쿼리를 그래픽 방식으로 표현할 수 없고 SQL 창에서만 쿼리를 편집할 수 있다는 메시지가 나타납니다.  
  
SQL 창에서 SQL 문을 입력하거나 편집한 다음 다른 창으로 이동하거나 쿼리를 확인하거나 쿼리를 실행하려 할 때 다음 조건 중 하나라도 충족되면 이 대화 상자가 나타납니다.  
  
-   SQL 문이 불완전하거나 하나 이상의 구문 오류가 포함된 경우  
  
-   SQL 문이 유효하지만 그래픽 창에서 이 SQL 문을 지원하지 않는 경우(예: 통합 쿼리)  
  
-   SQL 문이 유효하지만 현재 사용 중인 데이터 연결에만 한정된 구문이 포함된 경우  
  
> [!TIP]  
> 문이 유효한지 여부는 **쿼리** 도구 모음의 **SQL 문 확인** 단추를 사용하여 확인할 수 있습니다.  
  
이 대화 상자에는 SQL 문을 표현할 수 없는 이유가 표시되고 작업을 어떻게 진행할지 묻는 메시지가 나타납니다.  
  
> [!NOTE]  
> 다이어그램 창과 조건 창을 숨기면 **쿼리 정의 다름** 대화 상자가 나타나지 않습니다.  
  
## <a name="options"></a>옵션  
**무시 단추**  
이 단추를 선택하면 SQL 문을 받아들여 계속 편집하거나 실행하도록 지정할 수 있습니다. 문을 받아들이면 다이어그램 창과 조건 창이 흐리게 표시됩니다. 이는 SQL 창의 문을 해당 창에서 표현하지 않는다는 사실을 나타냅니다.  
  
**실행 취소 단추**  
이 단추를 선택하면 SQL 창에 대한 변경 내용을 취소할 수 있습니다.  
  
> [!NOTE]  
> 문이 올바르지만 쿼리 및 뷰 디자이너에서 그래픽 방식으로 나타낼 수 없는 경우 다이어그램 창과 조건 창에 이 문이 표현되지 않더라도 문을 실행할 수 있습니다. 예를 들어, 통합 쿼리를 입력한 경우 문을 실행할 수 있지만 다른 창에는 표현되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자이너 도구&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
