---
title: 여러 테이블의 증분 로드 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],multiple tables
ms.assetid: 39252dd5-09c3-46f9-a17b-15208cfd336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1549b8fa0979bba109c84485a89384722c82e7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62835409"
---
# <a name="perform-an-incremental-load-of-multiple-tables"></a>여러 테이블의 증분 로드 수행
  [변경 데이터 캡처를 사용하여 증분 로드 개선](change-data-capture-ssis.md)항목의 다이어그램에서는 한 테이블에서만 증분 로드를 수행하는 기본 패키지를 보여 줍니다. 그러나 한 테이블을 로드하는 작업은 여러 테이블을 증분 로드하는 작업만큼 일반적이지 않습니다.  
  
 여러 테이블을 증분 로드할 때 일부 단계는 모든 테이블에 대해 한 번만 수행해야 하며 다른 단계는 각 원본 테이블에 대해 반복해야 합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 이러한 단계를 구현하는 데에는 다음과 같은 여러 옵션이 있습니다.  
  
-   부모 패키지 및 자식 패키지 사용  
  
-   단일 패키지에서 여러 데이터 흐름 태스크 사용  
  
## <a name="loading-multiple-tables-by-using-a-parent-package-and-multiple-child-packages"></a>부모 패키지 및 여러 자식 패키지를 사용하여 여러 테이블 로드  
 부모 패키지를 사용하여 한 번만 수행되어야 하는 단계를 수행할 수 있습니다. 자식 패키지는 각 원본 테이블에 대해 수행되어야 하는 단계를 수행합니다.  
  
#### <a name="to-create-a-parent-package-that-performs-those-steps-that-only-have-to-be-done-once"></a>한 번만 수행되어야 하는 단계를 수행하는 부모 패키지를 만들려면  
  
1.  부모 패키지를 만듭니다.  
  
2.  제어 흐름에서 SQL 실행 태스크나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식을 사용하여 엔드포인트를 계산합니다.  
  
     엔드포인트를 계산하는 방법의 예는 [변경 데이터의 간격 지정](specify-an-interval-of-change-data.md)을 참조하세요.  
  
3.  필요한 경우 For 루프 컨테이너를 사용하여 선택한 기간에 대한 변경 데이터가 준비될 때까지 실행을 지연합니다.  
  
     이러한 For 루프 컨테이너의 예는 [변경 데이터의 준비 여부 확인](determine-whether-the-change-data-is-ready.md)을 참조하세요.  
  
4.  여러 패키지 실행 태스크를 사용하여 로드할 각 테이블에 대해 자식 패키지를 실행합니다. 부모 패키지 변수 구성을 사용하여 부모 패키지에서 계산된 엔드포인트를 각 자식 패키지에 전달합니다.  
  
     자세한 내용은 [패키지 실행 태스크](../control-flow/execute-package-task.md) 및 [자식 패키지에서 변수 및 매개 변수의 값 사용](../use-the-values-of-variables-and-parameters-in-a-child-package.md)을 참조하세요.  
  
#### <a name="to-create-child-packages-to-perform-those-steps-that-have-to-be-done-for-each-source-table"></a>각 원본 테이블에 대해 수행되어야 하는 단계를 수행하는 자식 패키지를 만들려면  
  
1.  각 원본 테이블에 대해 자식 패키지를 만듭니다.  
  
2.  제어 흐름에서 스크립트 태스크나 SQL 실행 태스크를 사용하여 변경 내용을 쿼리하는 데 사용할 SQL 문을 조합합니다.  
  
     쿼리를 조합하는 방법의 예는 [변경 데이터에 대한 쿼리 준비](prepare-to-query-for-the-change-data.md)를 참조하세요.  
  
3.  각 자식 패키지에서 단일 데이터 흐름 태스크를 사용하여 변경 데이터를 로드하고 대상에 적용합니다. 다음 단계에 설명된 대로 데이터 흐름을 구성합니다.  
  
    1.  데이터 흐름에서 원본 구성 요소를 사용하여 선택한 엔드포인트 범위에 포함되는 변경 테이블의 변경 내용을 쿼리합니다.  
  
         변경 테이블을 쿼리하는 방법의 예는 [변경 데이터 검색 및 이해](retrieve-and-understand-the-change-data.md)를 참조하세요.  
  
    2.  조건부 분할 변환을 사용하여 적절한 처리를 위해 삽입, 업데이트 및 삭제를 다른 출력으로 전송합니다.  
  
         이 변환을 구성하여 출력을 전송하는 방법의 예는 [삽입, 업데이트 및 삭제 처리](process-inserts-updates-and-deletes.md)를 참조하세요.  
  
    3.  대상 구성 요소를 사용하여 대상에 삽입을 적용합니다. 또한 OLE DB 명령 변환에 매개 변수가 있는 UPDATE 및 DELETE 문을 사용하여 대상에 업데이트 및 삭제를 적용합니다.  
  
         이 변환을 사용하여 업데이트 및 삭제를 적용하는 방법의 예는 [대상에 변경 내용 적용](apply-the-changes-to-the-destination.md)을 참조하세요.  
  
## <a name="loading-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>단일 패키지에서 여러 데이터 흐름 태스크를 사용하여 여러 테이블 로드  
 로드할 각 원본 테이블에 대한 별도의 데이터 흐름 태스크를 포함하는 단일 패키지를 사용할 수도 있습니다.  
  
#### <a name="to-load-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>단일 패키지에서 여러 데이터 흐름 태스크를 사용하여 여러 테이블을 로드하려면  
  
1.  단일 패키지를 만듭니다.  
  
2.  제어 흐름에서 SQL 실행 태스크나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식을 사용하여 엔드포인트를 계산합니다.  
  
     엔드포인트를 계산하는 방법의 예는 [변경 데이터의 간격 지정](specify-an-interval-of-change-data.md)을 참조하세요.  
  
3.  필요한 경우 For 루프 컨테이너를 사용하여 선택한 간격에 대한 변경 데이터가 준비될 때까지 실행을 지연합니다.  
  
     이러한 For 루프 컨테이너의 예는 [변경 데이터의 준비 여부 확인](determine-whether-the-change-data-is-ready.md)을 참조하세요.  
  
4.  스크립트 태스크나 SQL 실행 태스크를 사용하여 변경 내용을 쿼리하는 데 사용할 SQL 문을 조합합니다.  
  
     쿼리를 조합하는 방법의 예는 [변경 데이터에 대한 쿼리 준비](prepare-to-query-for-the-change-data.md)를 참조하세요.  
  
5.  여러 데이터 흐름 태스크를 사용하여 각 원본 테이블에서 변경 데이터를 로드하고 대상에 적용합니다. 다음 단계에 설명된 대로 각 데이터 흐름 태스크를 구성합니다.  
  
    1.  각 데이터 흐름에서 원본 구성 요소를 사용하여 선택한 엔드포인트 범위에 포함되는 변경 테이블의 변경 내용을 쿼리합니다.  
  
         변경 테이블을 쿼리하는 방법의 예는 [변경 데이터 검색 및 이해](retrieve-and-understand-the-change-data.md)를 참조하세요.  
  
    2.  조건부 분할 변환을 사용하여 적절한 처리를 위해 삽입, 업데이트 및 삭제를 다른 출력으로 전송합니다.  
  
         이 변환을 구성하여 출력을 전송하는 방법의 예는 [삽입, 업데이트 및 삭제 처리](process-inserts-updates-and-deletes.md)를 참조하세요.  
  
    3.  대상 구성 요소를 사용하여 대상에 삽입을 적용합니다. 또한 OLE DB 명령 변환에 매개 변수가 있는 UPDATE 및 DELETE 문을 사용하여 대상에 업데이트 및 삭제를 적용합니다.  
  
         이 변환을 사용하여 업데이트 및 삭제를 적용하는 방법의 예는 [대상에 변경 내용 적용](apply-the-changes-to-the-destination.md)을 참조하세요.  
  
  
