---
title: "데이터 프로필 뷰어 F1 도움말 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], viewer
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 39ade61624fcf412178c1fd7260e4082df1585e1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="data-profile-viewer-f1-help"></a>데이터 프로필 뷰어 F1 도움말
  데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 볼 수 있습니다.  
  
 데이터 프로필 뷰어를 사용하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요. 데이터 프로필 뷰어에서 분석하는 프로필 출력을 만드는 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **열기**  
 데이터 프로파일링 태스크의 출력을 포함하는 저장된 파일을 찾아보려면 클릭합니다.  
  
 **프로필** 창  
 출력에 포함된 프로필을 보려면 **프로필** 창에서 트리를 확장합니다. 해당 프로필의 결과를 보려면 프로필을 선택합니다.  
  
 **메시지** 창  
 상태 메시지를 표시합니다.  
  
 **드릴다운** 창  
 데이터 프로파일링 태스크에 사용되는 데이터 원본을 사용할 수 있는 경우 출력의 값과 일치하는 데이터의 행을 표시합니다.  
  
 예를 들어 US State 열에 대한 열 값 분포 프로필의 출력을 보는 경우 **세부 값 분포** 창에 "WA"에 대한 행이 포함될 수 있습니다. 드릴다운 창에서 주 열의 값이 "WA"인 데이터의 행을 보려면 **세부 값 분포** 창에서 해당 행을 두 번 클릭합니다.  
  
## <a name="dynamic-options"></a>동적 옵션  
  
### <a name="profile-type--column-length-distribution-profile"></a>프로필 유형 = 열 길이 분포 프로필  
  
#### <a name="column-length-distribution-profile---column-pane"></a>열 길이 분포 프로필- \<열 > 창  
 **최소 길이**  
 이 열의 값에 대한 최소 길이를 표시합니다.  
  
 **최대 길이**  
 이 열의 값에 대한 최대 길이를 표시합니다.  
  
 **선행 공백 무시**  
 이 프로필이 True 또는 False의 **IgnoreLeadingSpaces** 값으로 계산되었는지 여부를 표시합니다. 이 속성은 데이터 프로파일링 태스크 편집기의 **프로필 요청** 페이지에서 설정했습니다.  
  
 **후행 공백 무시**  
 이 프로필이 True 또는 False의 **IgnoreTrailingSpaces** 값으로 계산되었는지 여부를 표시합니다. 이 속성은 데이터 프로파일링 태스크 편집기의 **프로필 요청** 페이지에서 설정했습니다.  
  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
#### <a name="detailed-length-distribution-pane"></a>세부 길이 분포 창  
 **길이**  
 프로파일링된 열에서 찾은 열 길이를 표시합니다.  
  
 **개수**  
 프로파일링된 열의 값에 **길이** 열에 표시된 길이가 지정된 행 수를 표시합니다.  
  
 **백분율**  
 프로파일링된 열의 값에 **길이** 열에 표시된 길이가 지정된 행의 비율을 표시합니다.  
  
### <a name="profile-type--column-null-ratio-profile"></a>프로필 유형 = 열 Null 비율 프로필  
  
#### <a name="column-null-ratio-profile---column-pane"></a>열 Null 비율 프로필- \<열 > 창  
 **Null 개수**  
 프로파일링된 열에 Null 값이 있는 행 수를 표시합니다.  
  
 **Null 백분율**  
 프로파일링된 열에 Null 값이 있는 행의 비율을 표시합니다.  
  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
### <a name="profile-type--column-pattern-profile"></a>프로필 유형 = 열 패턴 프로필  
  
#### <a name="column-pattern-profile---column-pane"></a>열 패턴 프로필- \<열 > 창  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
#### <a name="pattern-distribution-pane"></a>패턴 분포 창  
 **Pattern**  
 프로파일링된 열에 대해 계산된 패턴을 표시합니다.  
  
 **백분율**  
 값이 **패턴** 열에 표시된 패턴과 일치하는 행의 비율을 표시합니다.  
  
### <a name="profile-type--column-statistics-profile"></a>프로필 유형 = 열 통계 프로필  
  
#### <a name="column-statistics-profile---column-pane"></a>열 통계 프로필- \<열 > 창  
 **최소**  
 프로파일링된 열에서 찾은 최소값을 표시합니다.  
  
 **최대값**  
 프로파일링된 열에서 찾은 최대값을 표시합니다.  
  
 **평균값**  
 프로파일링된 열에서 찾은 값의 평균을 표시합니다.  
  
 **표준 편차**  
 프로파일링된 열에서 찾은 값의 표준 편차를 표시합니다.  
  
### <a name="profile-type--column-value-distribution-profile"></a>프로필 유형 = 열 값 분포 프로필  
  
#### <a name="column-value-distribution-profile---column-pane"></a>열 값 분포 프로필- \<열 > 창  
 **고유 값 수**  
 프로파일링된 열에서 찾은 고유 값의 개수를 표시합니다.  
  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
#### <a name="detailed-value-distribution-pane"></a>세부 값 분포 창  
 **Value**  
 프로파일링된 열에서 찾은 고유 값을 표시합니다.  
  
 **개수**  
 프로파일링된 열에 **값** 열에 표시된 값이 있는 행 수를 표시합니다.  
  
 **백분율**  
 프로파일링된 열에 **값** 열에 표시된 값이 있는 행의 비율을 표시합니다.  
  
### <a name="profile-type--candidate-key-profile"></a>프로필 유형 = 후보 키 프로필  
  
#### <a name="candidate-key-profile---table-pane"></a>후보 키 프로필- \<테이블 > 창  
 **키 열**  
 프로파일링에 대해 후보 키로 선택된 열을 표시합니다.  
  
 **키 수준**  
 후보 키 열 또는 열 조합의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 중복 값이 있음을 나타냅니다.  
  
#### <a name="key-violations-pane"></a>키 위반 창  
 **\<column1 >, \<열 2 > 등입니다.**  
 프로파일링된 열에서 찾은 중복 값을 표시합니다.  
  
 **개수**  
 지정된 열에 첫 번째 열에 표시된 값이 있는 행 수를 표시합니다.  
  
### <a name="profile-type--functional-dependency-profile"></a>프로필 유형 = 함수 종속성 프로필  
  
#### <a name="functional-dependency-profile-pane"></a>함수 종속성 프로필 창  
 **결정 열**  
 결정 열로 선택된 열을 표시합니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서는 우편 번호가 결정 열입니다.  
  
 **종속 열**  
 종속 열로 선택된 열을 표시합니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서는 주가 종속 열입니다.  
  
 **함수 종속성 수준**  
 열 간 함수 종속성의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 결정 값이 종속 값을 결정하지 않는 경우가 있음을 나타냅니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서 이는 일부 주 값이 잘못되었음을 나타낼 수 있습니다.  
  
#### <a name="functional-dependency-violations-pane"></a>함수 종속성 위반 창  
  
> [!NOTE]  
>  데이터에서 잘못된 값의 비율이 높으면 함수 종속성 프로필에서 예기치 않은 결과가 발생할 수 있습니다. 예를 들어 Postal Code 값 "98052"에 대한 State 값이 행의 90%에 대해 "WI"인 경우 프로필은 올바른 주 값 "WA"를 포함하는 행을 위반으로 보고합니다.  
  
 **\<결정 열 이름 >**  
 이 함수 종속성 위반 인스턴스에서 결정 열 또는 열 조합의 값을 표시합니다.  
  
 **\<종속 열 이름 >**  
 이 함수 종속성 위반 인스턴스에서 종속 열의 값을 표시합니다.  
  
 **지원 개수**  
 결정 열 값이 종속 열을 결정하는 행 수를 표시합니다.  
  
 **위반 개수**  
 결정 열 값이 종속 열을 결정하지 않는 행 수를 표시합니다. (이 종속 값에 표시 된 값은이 행은  **\<종속 열 이름 >** 열입니다.)  
  
 **지원 백분율**  
 결정 열이 종속 열을 결정하는 행의 비율을 표시합니다.  
  
### <a name="profile-type--value-inclusion-profile"></a>프로필 유형 = 값 포함 프로필  
  
#### <a name="value-inclusion-profile-pane"></a>값 포함 프로필 창  
 **하위 집합측 열**  
 상위 집합 열에 있는지 여부를 확인하기 위해 프로파일링된 열 또는 열 조합을 표시합니다.  
  
 **상위 집합측 열**  
 하위 집합 열의 값을 포함하는지 여부를 확인하기 위해 프로파일링된 열 또는 열 조합을 표시합니다.  
  
 **포함 수준**  
 열 간 겹침의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 하위 집합 값이 상위 집합 값에 없는 경우가 있음을 나타냅니다.  
  
#### <a name="inclusion-violations-pane"></a>포함 위반 창  
 **\<column1 >, \<열 2 > 등입니다.**  
 상위 집합 열에서 찾지 못한 하위 집합 열의 값을 표시합니다.  
  
 **개수**  
 지정된 열에 첫 번째 열에 표시된 값이 있는 행 수를 표시합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)   
 [데이터 프로 파일링 태스크 및 뷰어](../../integration-services/control-flow/data-profiling-task-and-viewer.md)  
  
  
