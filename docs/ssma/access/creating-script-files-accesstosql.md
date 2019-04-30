---
title: 스크립트 파일 (AccessToSQL) 만들기 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 64dfe192-965c-49d4-a3ea-848fbc5f619f
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 5258a95b713da0ec1fe526e94ce11c6e5e0b595c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138775"
---
# <a name="creating-script-files-accesstosql"></a>스크립트 파일 (AccessToSQL) 만들기
첫 번째 스크립트 파일을 만들 때 SSMA 콘솔 응용 프로그램을 시작 하기 전에 고 변수 값 파일을 만들고 서버 연결 파일에 필요한 경우 단계입니다.  
  
스크립트 파일의 세 가지 섹션으로 보도 나눌 수 있습니다. 합니다.  
  
1.  **config:** 콘솔 응용 프로그램에 대 한 구성 매개 변수를 설정할 수 있습니다.  
  
2.  **서버:** 사용자를를 원본/대상 서버 정의 설정할 수 있습니다. 이 별도 서버 연결 파일에 있을 수도 있습니다.  
  
3.  **script-commands:** SSMA 워크플로 명령을 실행할 수 있습니다.  
  
각 섹션 아래에서 자세히 설명 되어 있습니다.  
  
## <a name="configuring-access-console-settings"></a>액세스 콘솔 설정 구성  
스크립트의 구성 콘솔 스크립트 파일에 표시 됩니다.  
  
설정 된 요소의 지정 된 경우 구성 노드에서를 모든 스크립트 명령에 적용할 수는 전역 설정 즉, 하는 것입니다. 이러한 구성 요소도 설정할 수 있습니다 각 명령 내에서 스크립트 명령 섹션에서 사용자가 전역 설정을 재정의 하려는 경우.  
  
사용자 구성 가능한 옵션은 다음과 같습니다.  
  
1.  **출력 창 공급자:** 메시지 표시 안 함 특성은 'true', 명령 별으로 설정 된 경우 메시지가 콘솔에 표시 되지 않습니다. 특성 설명은 다음과 같습니다.  
  
    -   대상: 출력 파일 또는 stdout에 인쇄 해야 하는지 여부를 지정 합니다. 이 옵션은 기본적으로 false입니다.  
  
    -   파일 이름: (선택 사항) 파일의 경로입니다.  
  
    -   표시 안 함-메시지: 콘솔에 메시지를 표시 하지 않습니다. 이 기본적으로 ' false'.  
  
    **예제:**  
  
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
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **데이터 마이그레이션 연결 공급자:** 이 지정 하는 원본/대상 서버 데이터 마이그레이션에 대 한 것으로 간주 하는 것입니다.  원본-사용-마지막으로 사용한 마지막으로 사용 되는 원본 서버 데이터 마이그레이션에 사용 됨을 나타냅니다. 마찬가지로 대상-사용-마지막으로 사용한 마지막으로 사용 되는 대상 서버 데이터 마이그레이션에 사용 됨을 나타냅니다. 사용자 특성 원본 서버 또는 대상 서버를 사용 하 여 (원본 또는 대상) 서버를 지정할 수도 있습니다.  
  
    하나 또는 다른 지정 된 특성 즉, 사용할 수 있습니다.  
  
    - 원본-사용-마지막으로 사용한 = "true" (기본값) 또는 원본 서버 = "source_servername"  
  
    - 대상-사용-마지막으로 사용한 = "true" (기본값) 또는 대상 서버 "target_servername" =  
  
    **예제:**  
  
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
  
3.  **사용자 입력된 팝업 합니다.** 따라서 개체는 데이터베이스에서 로드 될 때 오류를 처리 합니다. 오류 발생 시 콘솔으로 계속 됩니다. 사용자 지정 및 사용자 입력된 모드를 제공 합니다.  
  
    모드는 다음과 같습니다.  
  
    -   **요청-사용자-** continue('yes') 또는 ('no') 오류가 발생 하 라는 메시지입니다.  
  
    -   **오류-** 콘솔에서 오류를 표시 하 고 실행을 중지 합니다.  
  
    -   **계속-** 콘솔 실행을 진행 합니다.  
  
    기본 모드가 **오류**합니다.  
  
    **예제:**  
  
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
  
4.  **공급자를 다시 연결 합니다.** 이 연결 오류 시 다시 연결 설정을 지정할 수 있습니다. 이 소스와 대상 서버에 대해 설정할 수 있습니다.  
  
    다시 연결 모드는 다음과 같습니다.  
  
    -   reconnect-to-last-used-server: 연결이 활성 상태인 경우 마지막 최대 5 번 사용 하는 서버를 다시 연결 하려고 합니다.  
  
    -   생성을-오류: 연결이 활성 상태인 경우 오류가 생성 됩니다.  
  
    기본 모드가 **오류를 생성**합니다.  
  
    **예제:**  
  
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
  
5.  **변환기가 공급자를 덮어씁니다.** 사용자가 대상에 존재 하는 개체를 처리할 수 있도록이 메타 베이스 합니다. 가능한 작업은 다음과 같습니다.  
  
    -   오류: 콘솔 오류를 표시 하 고 실행을 중지 합니다.  
  
    -   덮어쓰기: 기존 개체 값을 덮어씁니다. 이 작업은 기본적으로 수행 됩니다.  
  
    -   skip: 콘솔은 데이터베이스에 이미 존재 하는 개체를 건너뛰고  
  
    -   요청 사용자: 입력 하 라는 ('예 '/' 아니요')  
  
    **예제:**  
  
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
  
6.  **실패 한 필수 구성 요소 공급자:** 따라서 사용자는 명령을 처리 하는 데 필요한 모든 필수 구성 요소를 처리할 수 있습니다. 기본적으로 strict 모드는 'f a l'입니다. 'True', 예외를 설정 하면 필수 구성 요소를 충족 하기 위해 실패에 대 한 생성을 가져옵니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true|false>"/>  
  
    </output-providers>  
    ```  
  
7.  **작업을 중지 합니다.** 사용자가 다음 작업을 중지 하려는 경우 중간 작업 중 **' Ctrl + C'** 바로 가기 키를 사용할 수 있습니다. SSMA 콘솔 액세스에 대 한 작업이 완료 되기를 대기 하 고 콘솔 실행을 종료 합니다.  
  
    사용자가 즉시 그런 다음 실행을 중지 하려는 경우 **' Ctrl + C'** 갑작스러운 종료 SSMA 콘솔 응용 프로그램에 대 한 바로 가기 키를 다시 누르면 수 있습니다.  
  
8.  **진행률 공급자:** 각 콘솔 명령의 진행률을 알립니다. 이 기본적으로 비활성화 됩니다. 진행률 보고 특성을 구성 합니다.  
  
    -   off  
  
    -   every-1%  
  
    -   every-2%  
  
    -   every-5%  
  
    -   every-10%  
  
    -   every-20%  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
     <progress-reporting enable="<true|false>"           (optional)  
  
                         report-messages="<true|false>"  (optional)  
  
                         report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off" (optional)/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true|false>"              (optional)  
  
        report-messages="<true|false>"     (optional)  
  
        report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **로 거 자세한 정도:** 집합 세부 정보 표시 수준을 로그입니다. 이 UI에서 모든 범주 옵션을 사용 하 여 해당합니다. 기본적으로 로그의 자세한 정도 수준에는 "error"입니다.  
  
    로 거 수준의 옵션은 다음과 같습니다.  
  
    -   -오류: 심각한 오류 메시지만 로깅됩니다.  
  
    -   오류: 오류 및 심각한 오류 메시지만 로깅됩니다.  
  
    -   경고: 디버그 및 정보 메시지를 제외한 모든 수준은 로깅됩니다.  
  
    -   정보: 디버그 메시지를 제외한 모든 수준은 로깅됩니다.  
  
    -   debug: 기록 된 메시지의 모든 수준입니다.  
  
    > [!NOTE]  
    > 모든 수준에서 필수 메시지가 기록 됩니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </...All commands...>  
    ```  
  
10. **암호화 된 암호를 재정의 합니다.** 'True', 서버 연결 파일의 서버 정의 섹션에서 또는 스크립트 파일에 존재 하는 경우 보호 된 저장소에 저장 된 암호화 된 암호 재정의에서 일반 텍스트 암호 지정 합니다. 암호가 일반 텍스트로 지정 된 경우 암호를 입력 하는 메시지가 표시 됩니다.  
  
    다음 두 가지 경우 발생합니다.  
  
    1.  경우 옵션을 재정의 됩니다 **false**, 검색의 순서가 됩니다 보호 된 저장소-&gt;스크립트 파일-&gt;서버 연결 파일-&gt; 사용자에 게 합니다.  
  
    2.  경우 재정의 옵션은 **true**, 검색의 순서가 됩니다 스크립트 파일-&gt;서버 연결 파일-&gt;사용자에 게 합니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
구성할 수 없는 옵션이입니다.  
  
-   **최대 다시 시도 합니다.** 연결이 시간 초과 되거나 네트워크 오류로 인해 중단, 서버 때 다시 연결 해야 합니다. 다시 연결 시도의 최대 수 **5** 그 후 다시 시도 콘솔은 자동으로 다시 연결을 수행 합니다. 자동 다시 연결의 시설에서 스크립트를 다시 실행 작업을 줄일 수 있습니다.  
  
## <a name="server-connection-parameters"></a>서버 연결 매개 변수  
서버 연결 파일 또는 스크립트 파일에서 서버 연결 매개 변수를 정의할 수 있습니다. 참조 하십시오 합니다 [서버 연결 파일 만들기 &#40;AccessToSQL&#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) 대 한 자세한 내용은 섹션입니다.  
  
## <a name="script-commands"></a>스크립트 명령  
스크립트 파일은 XML 형식으로 마이그레이션 워크플로 명령 시퀀스를 포함합니다. SSMA 콘솔 응용 프로그램에 스크립트 파일에 표시 되는 명령이 순으로 마이그레이션을 처리 합니다.  
  
예를 들어, Access 데이터베이스의 특정 테이블을 일반적인 데이터 마이그레이션을 수행 하는 계층 구조를 따릅니다. 데이터베이스-&gt; 테이블입니다.  
  
스크립트 파일의 모든 명령이 성공적으로 실행 되 면 SSMA 콘솔 응용 프로그램을 종료 하 고 사용자에 게 컨트롤을 반환 합니다. 스크립트 파일의 내용이 자세한 또는 작은 정적 변수 정보를 사용 하 여 포함 된 [변수 값 파일](creating-variable-value-files-accesstosql.md) 또는 변수 값에 대 한 스크립트 파일 내에서 별도 섹션에서.  
  
**예제:**  
  
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
템플릿 변수 값 파일 및 서버 연결 파일 (에 대 한 다양 한 시나리오 실행) 3 스크립트 파일로 구성 되는 제품 디렉터리의 샘플 콘솔 스크립트 폴더에 제공 됩니다.  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
관련성에 대 한 그 안에 표시 하는 매개 변수를 변경한 후 템플릿 (파일)를 실행할 수 있습니다.  
  
스크립트 명령의 전체 목록을 찾을 수 있습니다 [SSMA 콘솔 실행 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="script-file-validation"></a>스크립트 파일 유효성 검사  
사용자 스키마 정의 파일에 대해 자신의 스크립트 파일을 쉽게 확인할 수 있습니다 **'A2SSConsoleScriptSchema.xsd'** 'Schemas' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계
운영 콘솔에서 다음 단계 [변수 값 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)합니다.  
  
## <a name="see-also"></a>참고자료  
[변수 값 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
