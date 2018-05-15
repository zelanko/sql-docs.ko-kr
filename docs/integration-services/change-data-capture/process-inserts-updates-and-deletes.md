---
title: 삽입, 업데이트 및 삭제 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ebb06339c623d918a55dd4aee04957a60b09b572
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="process-inserts-updates-and-deletes"></a>삽입, 업데이트 및 삭제 처리
  변경 데이터를 증분 로드하는 Integration Services 패키지의 데이터 흐름에서 두 번째 태스크는 삽입, 업데이트 및 삭제를 구분하는 것입니다. 그런 다음 적절한 명령을 사용하여 대상에 해당 작업을 적용할 수 있습니다.  
  
> [!NOTE]  
>  변경 데이터를 증분 로드하는 패키지의 데이터 흐름을 디자인하는 첫 번째 태스크는 변경 데이터를 검색하는 쿼리를 실행하는 원본 구성 요소를 구성하는 것입니다. 이 구성 요소에 대한 자세한 내용은 [변경 데이터 검색 및 이해](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)를 참조하세요. 변경 데이터를 증분 로드하는 패키지를 만드는 전체 프로세스에 대한 설명은 [변경 데이터 캡처&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)를 참조하세요.  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>값을 연결하여 삽입, 업데이트 및 삭제 구분  
 변경 데이터를 검색하는 쿼리 예에서 **cdc.fn_cdc_get_net_changes_<capture_instance>** 함수는 **__$operation**이라는 메타데이터의 열만 반환합니다. 이 메타데이터 열은 변경을 발생시킨 작업을 나타내는 서수 값을 포함합니다.  
  
> [!NOTE]  
>  **cdc.fn_cdc_get_net_changes_<capture_instance>** 함수를 호출하는 쿼리에 대한 자세한 내용은 [변경 데이터 검색을 위한 함수 만들기](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)를 참조하세요.  
  
 서수 값을 해당 작업에 일치시키는 것은 작업의 니모닉을 사용하는 것만큼 쉽지 않습니다. 예를 들어 'D'로 쉽게 삭제 작업을 나타내고 'I'로 삽입 작업을 나타낼 수 있습니다. [변경 데이터 검색을 위한 함수 작성](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)항목에서 만든 쿼리 예는 서수 값을 새 열에 반환되는 문자열 값으로 변환합니다. 다음 코드 세그먼트에서는 이 변환을 보여 줍니다.  
  
```sql
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>조건부 분할 변환을 구성하여 직접 삽입, 업데이트 및 삭제 전송  
 변경 데이터 행을 직접 세 개의 출력 중 하나로 전송하려면 조건부 분할 변환이 가장 적합합니다. 변환에서는 각 행의 **CDC_OPERATION** 열 값만 검사하여 변경이 삽입, 업데이트, 삭제 중 어느 작업이었는지 확인합니다.  
  
> [!NOTE]  
>  CDC_OPERATION 열은 **__$operation** 열의 숫자 값에서 파생된 문자열 값을 포함합니다.  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>조건부 분할 변환을 사용하여 처리를 위해 삽입, 업데이트 및 삭제를 분할하려면  
  
1.  **데이터 흐름** 탭에서 조건부 분할 변환을 추가합니다.  
  
2.  OLE DB 원본의 출력을 조건부 분할 변환에 연결합니다.  
  
3.  **조건부 분할 변환 편집기**의 아래쪽 창에 다음 세 줄을 입력하여 세 개의 출력을 지정합니다.  
  
    1.  조건 `CDC_OPERATION == "I"` 가 있는 줄을 입력하여 삽입된 행을 삽입의 출력으로 전송합니다.  
  
    2.  조건 `CDC_OPERATION == "U"` 가 있는 줄을 입력하여 업데이트된 행을 업데이트의 출력으로 전송합니다.  
  
    3.  조건 `CDC_OPERATION == "D"` 가 있는 줄을 입력하여 삭제된 행을 삭제의 출력으로 전송합니다.  
  
## <a name="next-step"></a>다음 단계  
 처리를 위해 행을 분할한 후 다음 단계는 대상에 변경 내용을 적용하는 것입니다.  
  
 **다음 항목:** [대상에 변경 내용 적용](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>참고 항목  
 [조건부 분할 변환](../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [조건부 분할 변환을 사용하여 데이터 집합 분할](../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
