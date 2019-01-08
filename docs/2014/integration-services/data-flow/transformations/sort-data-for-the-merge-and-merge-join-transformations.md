---
title: 병합 및 병합 조인 변환을 위한 데이터 정렬 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- sort attributes [Integration Services]
- output columns [Integration Services]
ms.assetid: 22ce3f5d-8a88-4423-92c2-60a8f82cd4fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6f20391528b56bedca42e62ff9ae1f54111f3604
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751535"
---
# <a name="sort-data-for-the-merge-and-merge-join-transformations"></a>병합 및 병합 조인 변환을 위한 데이터 정렬
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 병합 및 병합 조인 변환에는 정렬된 데이터를 입력해야 합니다. 입력 데이터는 물리적으로 정렬되어야 하며 출력 및 원본의 출력 열 또는 업스트림 변환에 정렬 옵션이 설정되어야 합니다. 정렬 옵션은 데이터가 정렬되었음을 나타내지만 데이터가 실제로 정렬되지 않은 경우에는 병합 또는 병합 조인 작업의 결과를 예측할 수 없습니다.  
  
## <a name="sorting-the-data"></a>데이터 정렬  
 다음 방법 중 하나를 사용하여 이러한 데이터를 정렬할 수 있습니다.  
  
-   원본에서 데이터를 로드하는 데 사용되는 명령문에 ORDER BY 절을 사용합니다.  
  
-   데이터 흐름에서 병합 또는 병합 조인 변환 앞에 정렬 변환을 삽입합니다.  
  
 데이터가 문자열 데이터인 경우 병합 및 병합 조인 변환은 둘 다 Windows 데이터 정렬을 사용하여 문자열 값이 정렬된 것으로 간주합니다. 병합 및 병합 조인 변환에 Windows 데이터 정렬을 사용하여 정렬된 문자열 값을 제공하려면 다음 절차를 사용합니다.  
  
#### <a name="to-provide-string-values-that-are-sorted-by-using-windows-collation"></a>Windows 데이터 정렬을 사용하여 정렬되는 문자열 값을 제공하려면  
  
-   정렬 변환을 사용하여 데이터를 정렬합니다.  
  
     정렬 변환은 Windows 데이터 정렬을 사용하여 문자열 값을 정렬합니다.  
  
     -또는-  
  
-   먼저 Transact-SQL CAST 연산자를 사용하여 `varchar` 값을 `nvarchar` 값으로 캐스팅한 다음 Transact-SQL ORDER BY 절을 사용하여 데이터를 정렬합니다.  
  
    > [!IMPORTANT]  
    >  ORDER BY 절은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬을 사용하여 문자열 값을 정렬하므로 ORDER BY 절만 단독으로 사용할 수는 없습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬을 사용하면 Windows 데이터 정렬을 사용하는 것과 다른 순서로 데이터가 정렬되므로 병합 또는 병합 조인 변환이 예기치 않은 결과를 생성할 수 있습니다.  
  
## <a name="setting-sort-options-on-the-data"></a>데이터 정렬 옵션 설정  
 병합 및 병합 조인 변환에 데이터를 제공하는 원본이나 업스트림 변환에 두 가지 중요한 정렬 속성을 설정해야 합니다.  
  
-   데이터가 정렬되었는지 여부를 나타내는 출력의 `IsSorted` 속성. 이 속성을 `True`로 설정해야 합니다.  
  
    > [!IMPORTANT]  
    >  `IsSorted` 속성의 값을 `True`로 설정해도 데이터가 정렬되지는 않습니다. 이 속성은 데이터가 이전에 정렬되었다는 정보를 다운스트림 구성 요소에 제공하기만 합니다.  
  
-   열이 정렬되었는지 여부, 열의 정렬 순서 및 여러 열이 정렬된 시퀀스를 나타내는 출력 열의 `SortKeyPosition` 속성. 정렬된 데이터의 각 열에 이 속성을 설정해야 합니다.  
  
 정렬 변환을 사용하여 데이터를 정렬하면 이러한 두 속성이 병합 또는 병합 조인 변환에 필요한 값으로 설정됩니다. 즉, 출력의 `IsSorted` 속성이 `True`로 설정되고 출력 열의 `SortKeyPosition` 속성이 적절히 설정됩니다.  
  
 그러나 정렬 변환을 사용하여 데이터를 정렬하지 않는 경우에는 원본 또는 업스트림 변환에서 이러한 정렬 속성을 수동으로 설정해야 합니다. 원본 또는 업스트림 변환에서 정렬 속성을 수동으로 설정하려면 다음 절차를 수행합니다.  
  
#### <a name="to-manually-set-sort-attributes-on-a-source-or-transformation-component"></a>원본 또는 변환 구성 요소의 정렬 특성을 수동으로 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  적절한 원본 또는 업스트림 변환을 **데이터 흐름** 탭에서 찾거나 **도구 상자** 에서 디자인 화면으로 끌어 놓습니다.  
  
4.  구성 요소를 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 클릭합니다.  
  
5.  **입/출력 속성** 탭을 클릭합니다.  
  
6.  클릭  **\<구성 요소 이름 > 출력**를 설정 합니다 `IsSorted` 속성을 `True`입니다.  
  
    > [!NOTE]  
    >  수동으로 출력의 `IsSorted` 속성을 `True`로 설정했지만 데이터가 정렬되지 않았다면 패키지를 실행할 때 다운스트림 병합 또는 병합 조인 변환에 데이터가 누락되었거나 데이터 비교가 잘못되었기 때문일 수 있습니다.  
  
7.  **출력 열**을 확장합니다.  
  
8.  정렬된 것으로 표시할 열을 클릭하고 다음 지침에 따라 해당 `SortKeyPosition` 속성을 0이 아닌 정수 값으로 설정합니다.  
  
    -   정수 값은 1부터 시작하여 1씩 증가하는 숫자 시퀀스를 나타내야 합니다.  
  
    -   양의 정수 값은 오름차순 정렬을 나타냅니다.  
  
    -   음의 정수 값은 내림차순 정렬을 나타냅니다. 음수로 설정하는 경우 숫자의 절대값은 정렬 시퀀스에서 열의 순서를 결정합니다.  
  
    -   기본값인 0은 열이 정렬되지 않았음을 나타냅니다. 출력 열이 정렬에 참여하지 않는 경우 값을 0으로 둡니다.  
  
     `SortKeyPosition` 속성을 설정하는 방법을 보여 주는 예는 원본에서 데이터를 로드하는 다음 Transact-SQL 문을 참조하십시오.  
  
     `SELECT * FROM MyTable ORDER BY ColumnA, ColumnB DESC, ColumnC`  
  
     이 명령문의 경우 각 열의 `SortKeyPosition` 속성을 다음과 같이 설정합니다.  
  
    -   ColumnA의 `SortKeyPosition` 속성을 1로 설정합니다. 이는 ColumnA가 정렬할 첫째 열이며 오름차순으로 정렬됨을 나타냅니다.  
  
    -   ColumnB의 `SortKeyPosition` 속성을 -2로 설정합니다. 이는 ColumnB가 두 번째로 정렬할 열이며 내림차순으로 정렬함을 나타냅니다.  
  
    -   ColumnC의 `SortKeyPosition` 속성을 3으로 설정합니다. 이는 ColumnC가 정렬할 셋째 열이며 오름차순으로 정렬됨을 나타냅니다.  
  
9. 정렬된 각 열에 대해 8단계를 반복합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [병합 변환](merge-transformation.md)   
 [병합 조인 변환](merge-join-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)   
 [Integration Services 경로](../integration-services-paths.md)   
 [데이터 흐름 태스크](../../control-flow/data-flow-task.md)  
  
  
