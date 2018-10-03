---
title: 데이터 흐름에 데이터 뷰어를 추가 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab1e8476a7ddb05ff129417ba0493aae90a12852
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059933"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>데이터 흐름에 데이터 뷰어 추가
  이 항목에서는 데이터 흐름에 데이터 뷰어를 추가 및 구성하는 방법에 대해 설명합니다. 데이터 뷰어는 두 데이터 흐름 구성 요소 간에 이동하는 데이터를 표시합니다. 예를 들어 데이터 뷰어는 데이터 흐름 변환으로 데이터가 수정되기 전의 데이터 원본에서 추출한 데이터를 표시할 수 있습니다.  
  
 경로는 하나의 데이터 흐름 구성 요소의 출력을 다른 구성 요소의 입력에 연결함으로써 데이터 흐름의 구성 요소를 연결합니다.  
  
 패키지에 데이터 뷰어를 추가하려면 패키지에 데이터 흐름 태스크 및 최소한 두 개 이상의 연결된 데이터 흐름 구성 요소가 포함되어 있어야 합니다.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>데이터 흐름에 데이터 뷰어를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 이 아직 활성화되어 있지 않으면 탭을 클릭합니다.  
  
4.  데이터 흐름 태스크를 클릭하여 데이터 뷰어를 첨부할 데이터 흐름을 선택하고 **데이터 흐름** 탭을 클릭합니다.  
  
5.  두 데이터 흐름 구성 요소 간 경로를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
6.  **일반** 페이지에서 경로 속성을 보고 편집할 수 있습니다. 예를 들어 **PathAnnotation** 드롭다운 목록에서 경로 옆에 표시되는 주석을 선택할 수 있습니다.  
  
7.  **메타데이터** 페이지에서 열 메타데이터를 보고 메타데이터를 클립보드로 복사할 수 있습니다.  
  
8.  **데이터 뷰어** 페이지에서 **데이터 뷰어 사용**을 클릭합니다.  
  
9. 표시할 열 영역에서 데이터 뷰어에 표시할 열을 선택합니다. 기본적으로 사용 가능한 열이 모두 선택되어 **표시된 열** 목록에 나열됩니다. 사용하지 않을 열을 선택하고 왼쪽 화살표를 클릭하여 **사용되지 않은 열** 목록으로 이동합니다.  
  
    > [!NOTE]  
    >  표에서 DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET 데이터 형식을 나타내는 값은 ISO 8601 형식 문자열로 표시되고 `T` 구분 기호는 공백 구분 기호로 대체됩니다. DT_DATE 및 DT_FILETIME 데이터 형식을 나타내는 값은 7자리의 소수 자릿수 초를 갖습니다. DT_FILETIME 데이터 형식은 3자리의 소수 자릿수 초만 저장하기 때문에 표에는 나머지 4자리가 0으로 표시됩니다. DT_DBTIMESTAMP 데이터 형식을 나타내는 값은 3자리의 소수 자릿수 초를 갖습니다. DT_DBTIME2, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET 데이터 형식을 나타내는 값의 경우 소수 자릿수 초의 자릿수는 열의 데이터 형식에 대해 지정된 소수 자릿수에 해당합니다. ISO 8601 형식에 대한 자세한 내용은 [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md)을 참조하십시오. 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](data-flow/integration-services-data-types.md)을 참조하세요.  
  
10. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 변환](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](data-flow/integration-services-paths.md)   
 [데이터 흐름](data-flow/data-flow.md)   
 [데이터 흐름 디버깅](troubleshooting/debugging-data-flow.md)  
  
  
