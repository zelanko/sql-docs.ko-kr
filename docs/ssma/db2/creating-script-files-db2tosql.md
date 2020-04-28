---
title: 스크립트 파일 만들기 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ec23d188-b890-49b8-9a88-446df96269e4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 324aff21d677c213148922f7e06f267e08740c13
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67989842"
---
# <a name="creating-script-files-db2tosql"></a>스크립트 파일 만들기 (DB2ToSQL)
SSMA 콘솔 응용 프로그램을 시작 하기 전의 첫 번째 단계는 스크립트 파일을 만드는 것이 고, 필요한 경우 변수 값 파일 및 서버 연결 파일을 만드는 것입니다.  
  
스크립트 파일은 시각화.., 다음의 세 가지 섹션으로 나눌 수 있습니다.  
  
1.  **구성:** 사용자가 콘솔 응용 프로그램에 대 한 구성 매개 변수를 설정할 수 있습니다.  
  
2.  **서버:** 사용자가 원본/대상 서버 정의를 설정할 수 있도록 합니다. 이는 별도의 서버 연결 파일에 있을 수도 있습니다.  
  
3.  **스크립트-명령:** 사용자가 SSMA 워크플로 명령을 실행할 수 있습니다.  
  
각 섹션은 아래에 자세히 설명 되어 있습니다.  
  
## <a name="configuring-db2-console-settings"></a>DB2 콘솔 설정 구성  
스크립트의 구성은 콘솔 스크립트 파일에 표시 됩니다.  
  
구성 노드에 지정 된 요소가 있으면 전역 설정으로 설정 됩니다. 즉, 모든 스크립트 명령에 적용 됩니다. 사용자가 전역 설정을 재정의 하려는 경우 스크립트 명령 섹션의 각 명령 내에서 이러한 구성 요소를 설정할 수도 있습니다.  
  
사용자가 구성할 수 있는 옵션은 다음과 같습니다.  
  
1.  **출력 창 공급자:** 메시지 표시 안 함 특성이 ' t r u e '로 설정 된 경우 명령 관련 메시지가 콘솔에 표시 되지 않습니다. 특성 설명은 아래에 제공 되어 있습니다.  
  
    -   destination: 출력이 파일이 나 stdout에 인쇄 되어야 하는지 여부를 지정 합니다. 이는 기본적으로 false입니다.  
  
    -   파일 이름: 파일의 경로입니다 (선택 사항).  
  
    -   메시지 표시 안 함: 콘솔에서 메시지를 표시 하지 않습니다. 이는 기본적으로 ' f a l s e '입니다.  
  
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
  
2.  **데이터 마이그레이션 연결 공급자:** 데이터 마이그레이션을 고려 하 여 원본/대상 서버를 지정 합니다.  원본-사용-마지막으로 사용 된 원본 서버가 데이터 마이그레이션에 사용 됨을 나타냅니다. 유사 대상-사용-마지막으로 사용 된 대상 서버가 데이터 마이그레이션에 사용 됨을 나타냅니다. 또한 사용자는 원본 서버 또는 대상 서버 특성을 사용 하 여 서버 (원본 또는 대상)를 지정할 수 있습니다.  
  
    하나 또는 다른 지정 된 특성만 사용할 수 있습니다. 예:  
  
    -   원본-사용-마지막으로 사용 됨 = "true" (기본값) 또는 원본-서버 = "source_servername"  
  
    -   대상별-last used = "true" (기본값) 또는 target-server = "target_servername"  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **사용자 입력 팝업:** 이렇게 하면 개체가 데이터베이스에서 로드 될 때 오류를 처리할 수 있습니다. 사용자가 입력 모드를 제공 하 고 오류가 발생 하는 경우 사용자가 지정 하면 콘솔이 진행 됩니다.  
  
    모드는 다음과 같습니다.  
  
    -   **ask-사용자-** 사용자에 게 계속 (' 예 ') 또는 오류 (' 아니요 ')를 표시 합니다.  
  
    -   **오류-** 콘솔에 오류가 표시 되 고 실행이 중단 됩니다.  
  
    -   **계속-** 콘솔은 실행을 계속 진행 합니다.  
  
    기본 모드는 **오류**입니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **다시 연결 공급자:** 이를 통해 사용자는 연결 실패 재시도가 다시 연결 설정을 지정할 수 있습니다. 이는 원본 서버와 대상 서버 둘 다에 대해 설정할 수 있습니다.  
  
    다시 연결 모드는 다음과 같습니다.  
  
    -   마지막으로 사용 된 서버-서버: 연결이 활성화 되어 있지 않으면 최대 5 번 사용 된 마지막 서버에 다시 연결 하려고 시도 합니다.  
  
    -   -오류 생성: 연결이 활성화 되어 있지 않으면 오류가 발생 합니다.  
  
    기본 모드는 **오류 생성**입니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
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
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **변환기 덮어쓰기 공급자:** 이를 통해 사용자는 대상 메타 베이스에 이미 있는 개체를 처리할 수 있습니다. 가능한 작업은 다음과 같습니다.  
  
    -   오류: 콘솔에서 오류를 표시 하 고 실행을 중단 합니다.  
  
    -   overwrite: 기존 개체 값을 덮어씁니다. 이 작업은 기본적으로 수행 됩니다.  
  
    -   skip: 콘솔에서 데이터베이스에 이미 있는 개체를 건너뜁니다.  
  
    -   ask-user: 사용자에 게 입력 하 라는 메시지를 표시 합니다 (' yes '/' no ').  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **실패 한 필수 구성 요소 공급자:** 이를 통해 사용자는 명령을 처리 하는 데 필요한 모든 필수 구성 요소를 처리할 수 있습니다. 기본적으로 strict 모드는 ' f a l s e '입니다. ' T r u e '로 설정 된 경우 필수 조건에 맞지 않으면 예외가 생성 됩니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **작업 중지:** 중간 작업 중에 사용자가 작업을 중지 하려는 경우에는 **' Ctrl + C '** 바로 가기 키를 사용할 수 있습니다. D b 2 용 SSMA 콘솔은 작업이 완료 될 때까지 기다리거나 콘솔 실행을 종료 합니다.  
  
    사용자가 즉시 실행을 중지 하려는 경우 SSMA 콘솔 응용 프로그램의 갑작스러운 종료를 위해 **' Ctrl + C '** 바로 가기 키를 다시 누를 수 있습니다.  
  
8.  **진행률 공급자:** 각 콘솔 명령의 진행 상황을 알려 줍니다. 이 옵션은 기본적으로 사용하지 않도록 설정되어 있습니다. 진행률 보고 특성은 다음과 같이 구성 됩니다.  
  
    -   끄기  
  
    -   매-1%  
  
    -   매-2%  
  
    -   매-5%  
  
    -   매-10%  
  
    -   매-20%  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      progress-reporting   enable="<true/false>"            (optional)  
  
                           report-messages="<true/false>"   (optional)  
  
                           report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *또는*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"              (optional)  
  
        report-messages="<true/false>"     (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **로 거 자세한 정도:** 로그의 자세한 정도 수준을 설정 합니다. 이는 UI의 모든 범주 옵션과 일치 합니다. 기본적으로 로그의 자세한 정도 수준은 "오류"입니다.  
  
    로 거 수준 옵션은 다음과 같습니다.  
  
    -   심각한 오류: 치명적 오류 메시지만 로깅됩니다.  
  
    -   오류: 오류 및 치명적 오류 메시지만 로깅됩니다.  
  
    -   경고: 디버그 및 정보 메시지를 제외한 모든 수준이 로깅됩니다.  
  
    -   정보: 디버그 메시지를 제외한 모든 수준이 기록 됩니다.  
  
    -   디버그: 로깅되는 모든 메시지의 수준입니다.  
  
    > [!NOTE]  
    > 필수 메시지는 모든 수준에서 기록 됩니다.  
  
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
  
10. **암호화 된 암호 재정의:** 서버 연결 파일이 나 스크립트 파일의 서버 정의 섹션에 지정 된 일반 텍스트 암호는 ' t r u e ' 인 경우 보호 된 저장소에 저장 된 암호화 된 암호 (있는 경우)를 재정의 합니다. 일반 텍스트로 암호를 지정 하지 않으면 사용자에 게 암호를 입력 하 라는 메시지가 표시 됩니다.  
  
    여기에는 다음 두 가지 경우가 발생 합니다.  
  
    1.  Override 옵션이 **false**인 경우 검색 순서는 저장소-&gt;스크립트 파일-&gt;서버 연결 파일-프롬프트 사용자로&gt; 보호 됩니다.  
  
    2.  Override 옵션이 **true**인 경우 검색 순서는 스크립트 파일-&gt;서버 연결 파일-&gt;프롬프트 사용자입니다.  
  
    **예제:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
구성할 수 없는 옵션은 다음과 같습니다.  
  
-   **최대 다시 연결 시도 횟수:** 설정 된 연결의 시간이 초과 되거나 네트워크 오류로 인해 중단 되는 경우 서버를 다시 연결 해야 합니다. 다시 연결 시도는 다시 시도 횟수가 최대 **5 개** 까지 허용 되며, 그 후에는 콘솔에서 자동으로 다시 연결을 수행 합니다. 자동 다시 연결 기능을 통해 스크립트를 다시 실행 하는 작업이 줄어듭니다.  
  
## <a name="server-connection-parameters"></a>서버 연결 매개 변수  
서버 연결 매개 변수는 스크립트 파일 또는 서버 연결 파일에서 정의할 수 있습니다. 자세한 내용은 [서버 연결 파일 &#40;만들기&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) 섹션을 참조 하세요.  
  
## <a name="script-commands"></a>스크립트 명령  
스크립트 파일에는 XML 형식의 마이그레이션 워크플로 명령 시퀀스가 포함 되어 있습니다. SSMA 콘솔 응용 프로그램은 스크립트 파일에 표시 되는 명령 순서에 따라 마이그레이션을 처리 합니다.  
  
예를 들어 DB2 데이터베이스의 특정 테이블에 대 한 일반적인 데이터 마이그레이션은 Schema&gt; 테이블의 계층 구조를 따릅니다.  
  
스크립트 파일의 모든 명령이 성공적으로 실행 되 면 SSMA 콘솔 응용 프로그램이 종료 되 고 사용자에 게 컨트롤이 반환 됩니다. 스크립트 파일의 내용은 변수 값 [파일 &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md) 또는 변수 값에 대 한 스크립트 파일 내의 별도 섹션에 포함 된 변수 정보를 사용 하 여 정적입니다.  
  
**예제:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
3 개의 스크립트 파일 (다양 한 시나리오를 실행 하는 경우), 변수 값 파일 및 서버 연결 파일로 구성 된 템플릿은 product 디렉터리의 Sample Console Scripts 폴더에 제공 됩니다.  
  
-   AssessmentReportGenerationSample  
  
-   ConversionAndDataMigrationSample  
  
-   SqlStatementConversionSample  
  
-   VariableValueFileSample  
  
-   ServersConnectionFileSample  
  
관련성을 위해 여기에 표시 된 매개 변수를 변경한 후 템플릿 (파일)을 실행할 수 있습니다.  
  
스크립트 전체 목록- [SSMA 콘솔 &#40;DB2ToSQL를 실행](../../ssma/db2/executing-the-ssma-console-db2tosql.md) 하 여 찾을 수 있습니다&#41;  
  
## <a name="script-file-validation"></a>스크립트 파일 유효성 검사  
사용자는 ' 스키마 ' 폴더에서 사용 가능한 스키마 정의 파일 **' O2SSConsoleScriptSchema '** 에 대해 스크립트 파일의 유효성을 쉽게 검사할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
콘솔 운영의 다음 단계에서는 [DB2ToSQL&#41;&#40;변수 값 파일을 만듭니다 ](../../ssma/db2/creating-variable-value-files-db2tosql.md).  
  
## <a name="see-also"></a>참고 항목  
[DB2ToSQL&#41;&#40;변수 값 파일 만들기](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
