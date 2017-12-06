---
title: "스크립트 파일 (AccessToSQL) 만들기 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/17/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 64dfe192-965c-49d4-a3ea-848fbc5f619f
caps.latest.revision: "21"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: Inactive
ms.openlocfilehash: 2cdefc64512ba0b4b86c6c71b9b59885359ddc7f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="creating-script-files-accesstosql"></a>스크립트 파일 (AccessToSQL) 만들기
첫 번째 스크립트 파일을 만드는 것 SSMA 콘솔 응용 프로그램을 시작 하기 전에 고 변수 값 파일을 만들고 서버 연결 파일을 필요한 경우 단계입니다.  
  
스크립트 파일 세 가지 섹션으로 viz 나눌 수 있습니다.. 하십시오:  
  
1.  **config:** 콘솔 응용 프로그램에 대 한 구성 매개 변수를 설정할 수 있습니다.  
  
2.  **서버:** 소스/대상 서버 정의 설정할 수 있습니다. 이 값은 별도 서버 연결 파일에 될 수도 있습니다.  
  
3.  **스크립트 명령:** SSMA 워크플로 명령을 실행할 수 있습니다.  
  
각 섹션 아래에서 자세히 설명 되어 있습니다.  
  
## <a name="configuring-access-console-settings"></a>액세스 콘솔 설정 구성  
스크립트의 구성 콘솔 스크립트 파일에 표시 됩니다.  
  
설정 구성 노드와에 지정 된 요소를 경우 즉, 전역 설정으로 모든 스크립트 명령에 적용할 수 있는 합니다. 이러한 구성 요소도 설정할 수 있습니다 각 명령 내에서 스크립트 명령 섹션에서 사용자가을 전역 설정을 재정의할 경우.  
  
사용자 구성 가능한 옵션은 다음과 같습니다.  
  
1.  **출력 창 공급자:** 표시 하지 않는 메시지 특성이 'true', 명령 별으로 설정 된 경우 메시지가 콘솔에 표시 되지 않습니다. 특성 설명은 다음과 같습니다.  
  
    -   대상: 출력 파일 또는 stdout에 인쇄 해야 하는지 여부를 지정 합니다. 이 옵션은 기본적으로 false입니다.  
  
    -   파일 이름: (선택 사항) 파일의 경로입니다.  
  
    -   메시지 표시 안 함: 콘솔에 메시지를 표시 하지 않습니다. 이 옵션은 기본적으로 ' false'입니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **데이터 마이그레이션 연결 공급자:** 이 있는 지정 데이터 마이그레이션에 대 한 것으로 간주 되려면 소스/대상 서버를 사용 합니다.  소스-사용-최근에 사용 된 마지막으로 사용 되는 원본 서버 데이터 마이그레이션에 사용 됨을 나타냅니다. 마찬가지로 대상-사용-최근에 사용 된 마지막으로 사용 되는 대상 서버 데이터 마이그레이션에 사용 됨을 나타냅니다. 사용자 특성 원본 서버 또는 대상 서버를 사용 하 여 서버 (원본 또는 대상) 지정할 수도 있습니다.  
  
    하나 또는 다른 지정 된 특성 즉, 사용할 수 있습니다.  
  
    - 소스-사용-마지막으로 사용한 = "true" (기본값) 또는 소스 서버 "source_servername" =  
  
    - 대상-사용-마지막으로 사용한 = "true" (기본값) 또는 대상 서버 "target_servername" =  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="target_1"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="source_1"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **사용자 입력 팝업:** 개체는 데이터베이스에서 로드 되는 경우 이렇게 하면 오류를 처리 합니다. 오류 발생 시 콘솔 계속 사용자 지정 및 사용자 입력된 모드를 제공 합니다.  
  
    모드는 다음과 같습니다.  
  
    -   **요청-사용자-** continue('yes') 또는 오류 ('아니요')으로 사용자에 게 묻는 메시지를 표시 합니다.  
  
    -   **오류-** 콘솔에서 오류를 표시 하 고 실행을 중지 합니다.  
  
    -   **계속-** 콘솔 실행을 계속 진행 합니다.  
  
    기본 모드는 **오류**합니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="target_0">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **공급자를 다시 연결:** 이 사용자 연결 오류가 발생할 경우 다시 연결 설정을 설정할 수 있습니다. 이 소스와 대상 서버에 대해 설정할 수 있습니다.  
  
    다시 연결 모드는 같습니다.  
  
    -   서버에 다시 연결-마지막-사용: 마지막으로 최대 5 번 사용 되는 서버를 다시 연결 하면 연결이 활성화 되지 않습니다.  
  
    -   생성 한 오류: 연결이 활성화 하는 경우 오류가 생성 됩니다.  
  
    기본 모드는 **생성 한 오류**합니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
     <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                        on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *또는*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="target_0">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **변환기 덮어쓰기 공급자:** 이 대상에 존재 하는 개체를 처리할 사용자를 통해 메타 베이스 합니다. 가능한 작업은 다음과 같습니다.  
  
    -   오류: 콘솔에서 오류를 표시 하 고 실행을 중지 합니다.  
  
    -   덮어쓰기: 기존 개체 값을 덮어씁니다. 이 작업은 기본적으로 수행 됩니다.  
  
    -   건너뛸: 콘솔 데이터베이스에 이미 있는 개체를 건너뜁니다  
  
    -   사용자 확인: 사용자 입력에 대 한 요청 ('예 '/' 아니요')  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error|skip|overwrite|ask-user>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <convert-schema object-name="ssma.TT1">  
  
      <object-overwrite action="<error|skip|overwrite|ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **실패 한 필수 구성 요소 공급자:** 명령을 처리 하는 데 필요한 모든 필수 구성 요소를 처리 하는 사용자 수 있습니다. 기본적으로 strict 모드는 'false'. 'True', 예외를 설정 된 경우 필수 구성 요소를 충족 하지 못하여 생성 됩니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true|false>"/>  
  
    </output-providers>  
    ```  
  
7.  **중지 작업:** 사용자가 다음 작업을 중지 하려고 하는 경우 중간 작업 중 **' Ctrl + C'** 바로 가기 키를 사용할 수 있습니다. SSMA 콘솔 액세스에 대 한 대기 작업을 완료 하 고 콘솔 실행을 종료 합니다.  
  
    그런 다음 실행을 즉시 중지 해야 할 경우 **' Ctrl + C'** 갑자기 종료 SSMA 콘솔 응용 프로그램에 대 한 바로 가기 키를 다시 누르면 합니다.  
  
8.  **진행률 공급자:** 각 콘솔 명령이 진행 중임을 알립니다. 이 옵션은 기본적으로 비활성화 됩니다. 진행률 보고 특성을 구성 합니다.  
  
    -   off  
  
    -   모든 1%  
  
    -   모든 2%  
  
    -   매 5%  
  
    -   매 10%  
  
    -   모든 20%  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
     <progress-reporting enable="<true|false>"           (optional)  
  
                         report-messages="<true|false>"  (optional)  
  
                         report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off" (optional)/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true|false>"              (optional)  
  
        report-messages="<true|false>"     (optional)  
  
        report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off"     (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **로 거 자세한 정도:** 로그 자세한 정도 수준으로 설정 합니다. 이 UI에 모든 범주 옵션와 일치합니다. 기본적으로 로그 세부 정보 표시 수준 "error"입니다.  
  
    로 거 수준의 옵션은 다음과 같습니다.  
  
    -   심각한 오류: 심각한 오류만 메시지가 기록 됩니다.  
  
    -   오류: 오류 및 심각한 오류 메시지만 로깅됩니다.  
  
    -   경고: 디버그 및 정보 메시지를 제외한 모든 수준에서 기록 됩니다.  
  
    -   정보: 디버그 메시지가 기록 되는 점을 제외 하 고 모든 수준입니다.  
  
    -   디버그: 기록 된 메시지의 모든 수준입니다.  
  
    > [!NOTE]  
    > 모든 수준에서 필수 메시지가 기록 됩니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **암호화 된 암호 재정의:** 'true', 일반 텍스트 암호를 지정 된 없으면 서버 연결 파일의 서버 정의 섹션에 스크립트 파일에 존재 하는 경우에 저장 된 암호화 된 암호 저장소를 보호 하는 재정의 합니다. 일반 텍스트에 지정 된 암호가 사용자 암호를 입력 하 라는 메시지가 표시 됩니다.  
  
    다음 두 가지 경우에 발생합니다.  
  
    1.  경우 옵션을 재정의 **false**, 검색의 순서가 됩니다 보호 된 저장소-&gt;스크립트 파일-&gt;서버 연결 파일-&gt; 묻는 메시지 표시 합니다.  
  
    2.  경우 옵션을 재정의 **true**, 검색의 순서가 됩니다 스크립트 파일-&gt;서버 연결 파일-&gt;묻는 메시지 표시 합니다.  
  
    **예:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
구성할 수 없는 옵션이입니다.  
  
-   **최대 다시 연결 시도 횟수:** 설정 된 연결이 시간 초과 되거나 네트워크 오류로 인해 중단, 서버는 다시 연결 하는 데 필요 합니다. 회 시도의 최대 수 **5** , 그 후 다시 시도 횟수는 콘솔으로 다시 연결을 자동으로 수행 합니다. 자동 다시 연결은 시설에 스크립트를 다시 실행 하 여 활동을 줄일 수 있습니다.  
  
## <a name="server-connection-parameters"></a>서버 연결 매개 변수  
스크립트 파일 또는 서버 연결 파일에 서버 연결 매개 변수를 정의할 수 있습니다. 참조 하십시오는 [서버 연결 파일 &#40; 만들기 AccessToSQL &#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) 자세한 내용은 섹션.  
  
## <a name="script-commands"></a>스크립트 명령  
스크립트 파일은 XML 형식의 마이그레이션 워크플로 명령 시퀀스를 포함 합니다. SSMA 콘솔 응용 프로그램 마이그레이션 스크립트 파일에 표시 되는 명령이 순서 대로 처리 합니다.  
  
예를 들어 Access 데이터베이스의 특정 테이블의 일반적인 데이터 마이그레이션을의 계층 구조를 따릅니다: 데이터베이스-&gt; 테이블입니다.  
  
스크립트 파일에 있는 모든 명령을 올바르게 실행 되는지, SSMA 콘솔 응용 프로그램 종료 되 고 사용자에 게 컨트롤을 반환 합니다. 스크립트 파일의 내용이 자세한 또는 작은 정적 변수 정보를 포함 한 [변수 값 파일](http://msdn.microsoft.com/808595c3-8ef1-40bd-a93e-5cf237950e08) 또는 변수 값에 대 한 스크립트 파일 내 별도 섹션입니다.  
  
**예:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="$project_folder$"  
  
                        project-name="$project_name$"  
  
                        overwrite-if-exists="true"/>  
  
    <connect-source-database server="source_2"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
템플릿 변수 값 파일과 서버 연결 파일 (에 대 한 다양 한 시나리오 실행 중), 3 개의 스크립트 파일로 구성 된 제품 디렉터리의 샘플 콘솔 스크립트 폴더에 제공 됩니다.  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
관련성에 대 한 그 안에 표시 매개 변수 변경 후 템플릿 (파일)를 실행할 수 있습니다.  
  
스크립트 명령의 전체 목록은에 있습니다 [SSMA 콘솔 &#40; 실행 AccessToSQL &#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="script-file-validation"></a>스크립트 파일 유효성 검사  
사용자는 스키마 정의 파일에 대해 스크립트 파일의 유효성을 검사할 쉽게 수 **'A2SSConsoleScriptSchema.xsd'** '스키마' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계
운영 콘솔에 다음 단계는 [변수 값 파일 만들기 &#40; AccessToSQL &#41; ](../../ssma/access/creating-variable-value-files-accesstosql.md).  
  
## <a name="see-also"></a>참고 항목  
[변수 값 파일 &#40; 만들기 AccessToSQL &#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
