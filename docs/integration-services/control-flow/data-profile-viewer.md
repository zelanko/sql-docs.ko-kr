---
title: "데이터 프로필 뷰어 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 78476021d8f54edb0f26748e6d610f9590bee037
ms.contentlocale: ko-kr
ms.lasthandoff: 08/11/2017

---
# <a name="data-profile-viewer"></a>데이터 프로필 뷰어(Data Profile Viewer)
  데이터 프로파일링 프로세스의 다음 단계는 데이터 프로필을 보고 분석하는 것입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 내에서 데이터 프로파일링 태스크를 실행하고 데이터 프로필을 계산한 후에 이러한 프로필을 볼 수 있습니다. 데이터 프로파일링 태스크를 설정하고 실행하는 방법은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  출력 파일에는 데이터베이스와 해당 데이터베이스에 포함된 데이터에 대한 중요 데이터가 포함될 수 있습니다. 이 파일을 보다 안전하게 보호하는 방법에 대한 제안 사항은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
## <a name="data-profiles"></a>데이터 프로필  
 데이터 프로필을 보려면 데이터 프로파일링 태스크를 구성하여 해당 출력을 파일로 보낸 다음 독립 실행형 데이터 프로필 뷰어를 사용합니다. 데이터 프로필 뷰어를 열려면 다음 중 하나를 수행합니다.  
  
-   **디자이너에서** 데이터 프로파일링 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 태스크를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다. **데이터 프로파일링 태스크 편집기** 의 **일반** 페이지에서 **프로필 뷰어 열기**를 클릭합니다.  
  
-   폴더에서  *\<드라이브 >*: \Program Files (x86) | Files\Microsoft SQL Server\110\DTS\Binn 프로그램의 경우 DataProfileViewer.exe를 실행 합니다.  
  
 이 뷰어는 여러 창을 사용하여 선택적 세부 정보 및 드릴다운 기능과 함께 요청한 프로필과 계산된 결과를 표시합니다.  
  
 **프로필** 창  
 **프로필** 창에는 데이터 프로필 태스크에서 요청된 프로필이 표시됩니다. 프로필의 계산된 결과를 보려면 **프로필** 창에서 프로필을 선택합니다. 그러면 결과가 뷰어의 다른 창에 나타납니다.  
  
 **결과** 창  
 **결과** 창에는 단일 행을 통해 프로필의 계산된 결과가 요약됩니다. 예를 들어 **열 길이 분포 프로필**을 요청하면 이 행에 최소 및 최대 길이와 행 수가 포함됩니다. 대부분의 프로필에 대해 **결과** 창에서 이 행을 선택하여 선택적 **세부 정보** 창에서 추가 세부 정보를 확인할 수 있습니다.  
  
 **세부 정보** 창  
 대부분의 프로필 유형에 대해 **세부 정보** 창에는 **결과** 창에서 선택한 프로필 결과에 대한 추가 정보가 표시됩니다. 예를 들어 **열 길이 분포 프로필**을 요청하면 **세부 정보** 창에 발견된 각 열 길이가 표시됩니다. 또한 이 창에는 열 값에 해당 열 길이가 지정된 행의 개수 및 비율이 표시됩니다.  
  
 둘 이상의 열에 대해 계산되는 세 개의 프로필 유형(후보 키, 함수 종속성 및 값 포함)이 있을 경우 **세부 정보** 창에는 예상 관계 위반이 표시됩니다. 예를 들어 후보 키 프로필을 요청하면 세부 정보 창에 후보 키의 고유성을 위반하는 중복 값이 표시됩니다.  
  
 프로필을 계산하는 데 사용된 데이터 원본을 사용할 수 있는 경우 **세부 정보** 창에서 행을 두 번 클릭하여 **드릴다운** 창에서 일치하는 데이터 행을 확인할 수 있습니다.  
  
 **드릴다운** 창  
 다음 조건에 해당하는 경우 **세부 정보** 창에서 행을 두 번 클릭하여 **드릴다운** 창에서 일치하는 데이터 행을 확인할 수 있습니다.  
  
-   프로필을 계산하는 데 사용되는 데이터 원본을 사용할 수 있습니다.  
  
-   데이터를 볼 수 있는 권한이 있습니다.  
  
 데이터 프로필 뷰어에서는 드릴다운 요청에 대한 원본 데이터베이스에 연결하기 위해 Windows 인증과 현재 사용자의 자격 증명을 사용합니다. 데이터 프로필 뷰어에서는 데이터 프로파일링 태스크를 실행한 패키지에 저장된 연결 정보를 사용하지 않습니다.  
  
> [!IMPORTANT]  
>  데이터 프로필 뷰어에서 사용할 수 있는 드릴다운 기능은 원래 데이터 원본에 라이브 쿼리를 보냅니다. 이러한 쿼리를 사용하면 서버 성능이 저하될 수 있습니다.  
>   
>  최근에 만들어지지 않은 출력 파일에서 드릴다운하는 경우 드릴다운 쿼리에서 원래 출력이 계산된 행 집합과 다른 행 집합을 반환할 수도 있습니다.  
  
 데이터 프로필 뷰어의 사용자 인터페이스에 대한 자세한 내용은 [Data Profile Viewer F1 Help](../../integration-services/control-flow/data-profile-viewer-f1-help.md)을 참조하십시오.  
  
## <a name="data-profile-viewer-f1-help"></a>데이터 프로필 뷰어 F1 도움말
  데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 볼 수 있습니다.  
  
 데이터 프로필 뷰어를 사용하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요. 데이터 프로필 뷰어에서 분석하는 프로필 출력을 만드는 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요.  
  
### <a name="static-options"></a>정적 옵션  
 **열기**  
 데이터 프로파일링 태스크의 출력을 포함하는 저장된 파일을 찾아보려면 클릭합니다.  
  
 **프로필** 창  
 출력에 포함된 프로필을 보려면 **프로필** 창에서 트리를 확장합니다. 해당 프로필의 결과를 보려면 프로필을 선택합니다.  
  
 **메시지** 창  
 상태 메시지를 표시합니다.  
  
 **드릴다운** 창  
 데이터 프로파일링 태스크에 사용되는 데이터 원본을 사용할 수 있는 경우 출력의 값과 일치하는 데이터의 행을 표시합니다.  
  
 예를 들어 US State 열에 대한 열 값 분포 프로필의 출력을 보는 경우 **세부 값 분포** 창에 "WA"에 대한 행이 포함될 수 있습니다. 드릴다운 창에서 주 열의 값이 "WA"인 데이터의 행을 보려면 **세부 값 분포** 창에서 해당 행을 두 번 클릭합니다.  
  
### <a name="dynamic-options"></a>동적 옵션  
  
#### <a name="profile-type--column-length-distribution-profile"></a>프로필 유형 = 열 길이 분포 프로필  
  
##### <a name="column-length-distribution-profile---column-pane"></a>열 길이 분포 프로필- \<열 > 창  
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
  
##### <a name="detailed-length-distribution-pane"></a>세부 길이 분포 창  
 **길이**  
 프로파일링된 열에서 찾은 열 길이를 표시합니다.  
  
 **개수**  
 프로파일링된 열의 값에 **길이** 열에 표시된 길이가 지정된 행 수를 표시합니다.  
  
 **백분율**  
 프로파일링된 열의 값에 **길이** 열에 표시된 길이가 지정된 행의 비율을 표시합니다.  
  
#### <a name="profile-type--column-null-ratio-profile"></a>프로필 유형 = 열 Null 비율 프로필  
  
##### <a name="column-null-ratio-profile---column-pane"></a>열 Null 비율 프로필- \<열 > 창  
 **Null 개수**  
 프로파일링된 열에 Null 값이 있는 행 수를 표시합니다.  
  
 **Null 백분율**  
 프로파일링된 열에 Null 값이 있는 행의 비율을 표시합니다.  
  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
#### <a name="profile-type--column-pattern-profile"></a>프로필 유형 = 열 패턴 프로필  
  
##### <a name="column-pattern-profile---column-pane"></a>열 패턴 프로필- \<열 > 창  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
##### <a name="pattern-distribution-pane"></a>패턴 분포 창  
 **Pattern**  
 프로파일링된 열에 대해 계산된 패턴을 표시합니다.  
  
 **백분율**  
 값이 **패턴** 열에 표시된 패턴과 일치하는 행의 비율을 표시합니다.  
  
#### <a name="profile-type--column-statistics-profile"></a>프로필 유형 = 열 통계 프로필  
  
##### <a name="column-statistics-profile---column-pane"></a>열 통계 프로필- \<열 > 창  
 **최소**  
 프로파일링된 열에서 찾은 최소값을 표시합니다.  
  
 **최대값**  
 프로파일링된 열에서 찾은 최대값을 표시합니다.  
  
 **평균값**  
 프로파일링된 열에서 찾은 값의 평균을 표시합니다.  
  
 **표준 편차**  
 프로파일링된 열에서 찾은 값의 표준 편차를 표시합니다.  
  
#### <a name="profile-type--column-value-distribution-profile"></a>프로필 유형 = 열 값 분포 프로필  
  
##### <a name="column-value-distribution-profile---column-pane"></a>열 값 분포 프로필- \<열 > 창  
 **고유 값 수**  
 프로파일링된 열에서 찾은 고유 값의 개수를 표시합니다.  
  
 **행 개수**  
 테이블 또는 뷰의 행 수를 표시합니다.  
  
##### <a name="detailed-value-distribution-pane"></a>세부 값 분포 창  
 **Value**  
 프로파일링된 열에서 찾은 고유 값을 표시합니다.  
  
 **개수**  
 프로파일링된 열에 **값** 열에 표시된 값이 있는 행 수를 표시합니다.  
  
 **백분율**  
 프로파일링된 열에 **값** 열에 표시된 값이 있는 행의 비율을 표시합니다.  
  
#### <a name="profile-type--candidate-key-profile"></a>프로필 유형 = 후보 키 프로필  
  
##### <a name="candidate-key-profile---table-pane"></a>후보 키 프로필- \<테이블 > 창  
 **키 열**  
 프로파일링에 대해 후보 키로 선택된 열을 표시합니다.  
  
 **키 수준**  
 후보 키 열 또는 열 조합의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 중복 값이 있음을 나타냅니다.  
  
##### <a name="key-violations-pane"></a>키 위반 창  
 **\<column1 >, \<열 2 > 등입니다.**  
 프로파일링된 열에서 찾은 중복 값을 표시합니다.  
  
 **개수**  
 지정된 열에 첫 번째 열에 표시된 값이 있는 행 수를 표시합니다.  
  
#### <a name="profile-type--functional-dependency-profile"></a>프로필 유형 = 함수 종속성 프로필  
  
##### <a name="functional-dependency-profile-pane"></a>함수 종속성 프로필 창  
 **결정 열**  
 결정 열로 선택된 열을 표시합니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서는 우편 번호가 결정 열입니다.  
  
 **종속 열**  
 종속 열로 선택된 열을 표시합니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서는 주가 종속 열입니다.  
  
 **함수 종속성 수준**  
 열 간 함수 종속성의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 결정 값이 종속 값을 결정하지 않는 경우가 있음을 나타냅니다. 같은 미국 우편 번호가 항상 같은 주여야 하는 예에서 이는 일부 주 값이 잘못되었음을 나타낼 수 있습니다.  
  
##### <a name="functional-dependency-violations-pane"></a>함수 종속성 위반 창  
  
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
  
#### <a name="profile-type--value-inclusion-profile"></a>프로필 유형 = 값 포함 프로필  
  
##### <a name="value-inclusion-profile-pane"></a>값 포함 프로필 창  
 **하위 집합측 열**  
 상위 집합 열에 있는지 여부를 확인하기 위해 프로파일링된 열 또는 열 조합을 표시합니다.  
  
 **상위 집합측 열**  
 하위 집합 열의 값을 포함하는지 여부를 확인하기 위해 프로파일링된 열 또는 열 조합을 표시합니다.  
  
 **포함 수준**  
 열 간 겹침의 수준(비율)을 표시합니다. 100% 미만의 키 수준은 하위 집합 값이 상위 집합 값에 없는 경우가 있음을 나타냅니다.  
  
##### <a name="inclusion-violations-pane"></a>포함 위반 창  
 **\<column1 >, \<열 2 > 등입니다.**  
 상위 집합 열에서 찾지 못한 하위 집합 열의 값을 표시합니다.  
  
 **개수**  
 지정된 열에 첫 번째 열에 표시된 값이 있는 행 수를 표시합니다.  
  

