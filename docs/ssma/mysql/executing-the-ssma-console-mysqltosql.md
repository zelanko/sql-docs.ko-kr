---
title: SSMA 콘솔 (MySQLToSQL) 실행 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
caps.latest.revision: 25
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fb0022b9e4dd222fd3d19ed4dc3e6d03fc740bb
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="executing-the-ssma-console-mysqltosql"></a>SSMA 콘솔 (MySQLToSQL)를 실행합니다.
Microsoft 파일 명령을 실행 및 제어 SSMA 활동을 스크립트의 강력한 집합 제공 합니다.  
  
콘솔 응용 프로그램은이 섹션의 열거형으로 특정 표준 스크립트 파일 명령을 사용합니다.  
  
## <a name="project--script-file-commands"></a>프로젝트 스크립트 파일 명령  
**Command**  
  
create-new-project:   
                   새 SSMA 프로젝트를 만듭니다.  
  
프로젝트 명령을 처리 프로젝트 만들기, 열기, 저장 하 고 프로젝트를 종료 합니다.  
  
**스크립트**  
  
1.  `project-folder` 만든 가져오기 프로젝트의 폴더를 나타냅니다.  
  
2.  `project-name` 프로젝트의 이름을 나타냅니다. {string}  
  
3.  `overwrite-if-exists`선택적 특성 기존 프로젝트를 덮어써야 하는 경우를 나타냅니다. {부울}  
  
4.  `project-type:`선택적 특성입니다. 프로젝트 형식 즉, "sql server 2005" 프로젝트 또는 프로젝트 "sql server 2008" 또는 "sql server 2012" 또는 "sql server 2014" 프로젝트 또는 "sql azure" 프로젝트를 나타냅니다. 기본값은 "sql server 2008"입니다.  
  
**구문 예제:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type==”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”   (optional)  
  
/>  
```  
' 덮어쓰기-이미 있는 경우-' 특성은 **false** 기본적으로 합니다.  
  
' 프로젝트 type' 특성은 **sql-서버-2008** 기본적으로 합니다.  
  
**Command**  
  
프로젝트 열기:   
                  기존 프로젝트를 엽니다.  
  
**스크립트**  
  
1.  `project-folder` 만든 가져오기 프로젝트의 폴더를 나타냅니다. 이 명령은 지정 된 폴더가 존재 하지 않는 경우 실패 합니다.  {string}  
  
2.  `project-name` 프로젝트의 이름을 나타냅니다. 이 명령은 지정 된 프로젝트가 존재 하지 않는 경우 실패 합니다.  {string}  
  
**구문 예제:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> MySQL 콘솔에 대 한 SSMA 응용 프로그램 이전 버전과 호환성을 지원합니다. SSMA의 이전 버전에서 만든 프로젝트를 열 수 있습니다.  
  
**Command**  
  
프로젝트 저장: 마이그레이션 프로젝트에 저장 합니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
프로젝트 닫기  
                  : 마이그레이션 프로젝트를 닫습니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
프로젝트 닫기  
                  : 마이그레이션 프로젝트를 닫습니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
' If 수정 ' 특성은 선택 사항 **무시** 기본적으로 합니다.  
  
## <a name="database-connection-script-file-commands"></a>데이터베이스 연결 스크립트 파일 명령  
데이터베이스 연결 명령을 데이터베이스에 연결할 수 있습니다.  
  
1.  **찾아보기** UI의 기능을 콘솔에서 지원 되지 않습니다.  
  
2.  **windows 인증** 및 **포트** SQL Azure에 연결할 때 매개 변수가 적용 됩니다.  
  
3.  스크립트 파일 만들기 '에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md)합니다.  
  
**Command**  
  
connect-source-database  
  
-   원본 데이터베이스에 수행 하 고 원본 데이터베이스에만 메타 데이터의 높은 수준의 메타 데이터를 로드 합니다.  
  
-   원본에 대 한 연결을 설정할 수 없는 경우 오류가 생성 되 고 콘솔 응용 프로그램에서 더 이상 실행  
  
**스크립트**  
  
서버 정의 서버 연결 파일 또는 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 이름 특성에서 검색 됩니다.  
  
**구문 예제:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
force-load-source/target-database  
  
-   원본 메타 데이터를 로드합니다.  
  
-   마이그레이션 프로젝트 오프 라인으로 작업을 수행 하는 데 유용 합니다.  
  
-   소스/대상에 대 한 연결을 설정할 수 없는 경우 오류가 생성 되 고 콘솔 응용 프로그램에서 더 이상 실행  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드 명령줄 매개 변수로 필요합니다.  
  
**구문 예제:**  
  
```xml  
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
1.  원본 데이터베이스에 다시 연결 되지만 원본 데이터베이스 연결 명령과 달리 모든 메타 데이터를 로드 하지 않습니다.  
  
2.  오류가 생성 됩니다 (다시) 원본과 연결을 설정할 수 없는 경우와 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
1.  대상 SQL Server 또는 SQL Azure 데이터베이스에 연결 하 고 대상 데이터베이스의 높은 수준의 메타 데이터는 있지만 메타 데이터가 아니라를 완전히 로드 합니다.  
  
2.  대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
**스크립트**  
  
서버 정의 검색 하는 서버 연결 파일 또는 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 이름 특성에서  
  
**구문 예제:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
1.  대상 데이터베이스에 다시 연결 되지만 연결 대상 데이터베이스 명령과 달리 모든 메타 데이터를 로드 하지 않습니다.  
  
2.  오류가 생성 됩니다 (다시) 대상에 대 한 연결을 설정할 수 없는 경우와 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>보고서 스크립트 파일 명령  
SSMA 콘솔의 다양 한 작업의 성능에는 보고서를 생성 하는 보고서 명령입니다.  
  
**Command**  
  
generate-assessment-report  
  
1.  원본 데이터베이스에서 평가 보고서를 생성합니다.  
  
2.  이 명령을 실행 하기 전에 원본 데이터베이스 연결을 수행 하지 않는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
3.  또한 명령 실행 하는 동안 원본 데이터베이스 서버에 연결 하지 못한 콘솔 응용 프로그램을 종료 발생 합니다.  
  
**스크립트**  
  
1.  `assessment-report-folder:` 평가 보고서 저장을 수행할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
2.  `object-name:` 평가 보고서 생성 (은 개별 개체 이름이 나 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
3.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
4.  `assessment-report-overwrite:` 이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
5.  `write-summary-report-to:` 요약 보고서가 생성 하는 위치 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **AssessmentReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    보고서를 만드는 두 가지 추가 하위 범주에 있습니다.  
  
    -   `report-errors` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>마이그레이션 스크립트 파일 명령  
마이그레이션 명령 소스 스키마에 대상 데이터베이스 스키마를 변환 및 대상 서버에 데이터를 마이그레이션합니다.  
  
마이그레이션 명령에 대 한 설정 기본 콘솔 출력은 보고 하지 않으려면 자세한 오류 사용 하 여 '전체' 출력 보고서: 소스 개체 트리의 루트 노드에서 요약 합니다.  
  
**Command**  
  
convert-schema  
  
1.  소스에서 대상 스키마로 스키마 변환을 수행합니다.  
  
2.  이 명령을 실행 하기 전에 원본 또는 대상 데이터베이스 연결을 수행 하지 않으면 명령 실행 하는 동안 소스 또는 대상 데이터베이스 서버에 연결할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
**스크립트**  
  
1.  `conversion-report-folder:` 평가 보고서 저장을 수행할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
2.  `object-name:` 스키마 (은 indivdual 개체 이름이 나 그룹 개체 이름)을 변환 하기 위한 것으로 간주 하는 개체를 지정 합니다.  
  
3.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
4.  `conversion-report-overwrite:` 이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
5.  `write-summary-report-to:` 요약 보고서가 생성 하는 위치 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **SchemaConversionReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    요약 보고서 작성에는 두 개의 추가 하위 범주에 있습니다.  
  
    -   `report-errors` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
데이터 마이그레이션  
  
1.  대상에는 원본 데이터를 마이그레이션합니다.  
  
**스크립트**  
  
1.  `object-name:` 마이그레이션에 대 한 것으로 간주 원본 개체를 지정 합니다 (이 있을 수 있음 indivdual 개체 이름이 나 그룹 개체 이름)는 데이터입니다.  
  
2.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
3.  `write-summary-report-to:` 요약 보고서가 생성 하는 위치 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **DataMigrationReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    보고서를 만드는 두 가지 추가 하위 범주에 있습니다.  
  
    -   `report-errors` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose` (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
또는  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>마이그레이션 준비 스크립트 파일 명령  
마이그레이션 준비 명령은 원본 및 대상 데이터베이스 간에 스키마 매핑을 시작합니다.  
  
**Command**  
  
map-schema  
  
원본 데이터베이스와 대상 스키마의 스키마 매핑.  
  
**스크립트**  
  
1.  `source-schema` 마이그레이션할를 소스 스키마를 지정 합니다.  
  
2.  `sql-server-schema` 대상 스키마를 원하는 위치로 마이그레이션할 수를 지정 합니다.  
  
**구문 예제:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>관리 효율성 스크립트 파일 명령  
원본 데이터베이스와 대상 데이터베이스 개체를 동기화 하는 데 도움이 관리 효율성 명령.  
  
> [!NOTE]  
> 마이그레이션 명령에 대 한 설정 기본 콘솔 출력은 보고 하지 않으려면 자세한 오류 사용 하 여 '전체' 출력 보고서: 소스 개체 트리의 루트 노드에서 요약 합니다.  
  
**Command**  
  
동기화 대상  
  
1.  대상 데이터베이스와 대상 개체를 동기화합니다.  
  
2.  이 명령은 원본 데이터베이스에 대해 실행 될 경우 오류가 발생 합니다.  
  
3.  이 명령을 실행 하기 전에 대상 데이터베이스 연결을 수행 하지 않으면 명령 실행 중에 대상 데이터베이스 서버에 연결할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
**스크립트**  
  
1.  `object-name:` 대상 데이터베이스 (은 indivdual 개체 이름이 나 그룹 개체 이름)와 동기화 하기 위한 것으로 간주 하는 개체를 지정 합니다.  
  
2.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
3.  `on-error:` 동기화 오류 경고 또는 오류로 지정할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` 에 대 한 동기화 작업 (특성 선택 사항) 폴더 경로 지정 하는 경우에 다음 파일 이름으로 오류 보고서의 위치를 지정 **TargetSynchronizationReport.XML** 만들어집니다.  
  
**구문 예제:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
또는  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Command**  
  
refresh-from-database  
  
1.  데이터베이스의 원본 개체를 새로 고칩니다.  
  
2.  이 명령은 대상 데이터베이스에 대해 실행 될 경우 오류가 생성 됩니다.  
  
**스크립트**  
  
1.  `object-name:` (이 있을 수 있음 indivdual 개체 이름이 나 그룹 개체 이름)는 원본 데이터베이스에서 새로 고침에 대 한 것으로 간주 원본 개체를 지정 합니다.  
  
2.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
3.  `on-error:` 동기화 오류 경고 또는 오류로 지정할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
4.  `report-errors-to:` 에 대 한 동기화 작업 (특성 선택 사항) 폴더 경로 지정 하는 경우에 다음 파일 이름으로 오류 보고서의 위치를 지정 **SourceDBRefreshReport.XML** 만들어집니다.  
  
하나 또는 여러 메타 베이스 노드 명령줄 매개 변수로 필요합니다.  
  
**구문 예제:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
또는  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>스크립트 생성 스크립트 파일 명령  
이중 작업을 수행 하는 스크립트 생성 명령을: 콘솔; 스크립트 파일에 출력을 절약할 및 T-SQL 출력을 콘솔 또는 지정한 매개 변수를 기준으로 파일을 기록 합니다.  
  
**Command**  
  
save-as-script  
  
개체의 스크립트 때 언급 된 파일에 저장 하는 데 사용 메타 베이스 = 대상, 여기서에서는 스크립트 하 고 대상 데이터베이스에서 실행 하는 동일한 동기화 명령에 대 한 대안입니다.  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드 명령줄 매개 변수로 필요합니다.  
  
1.  `object-name:` 해당 스크립트를 저장할는 개체를 지정 합니다. (이 있을 수 있음 indivdual 개체 이름이 나 그룹 개체 이름)  
  
2.  `object-type:` 지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
3.  `metabase:` 원본 인지를 지정 하거나 메타 베이스를 대상 지정 합니다.  
  
4.  `destination:` 경로나 파일 이름이 제공 되지 않으면 다음 파일 이름 (object_name 특성 값) 형식.out에 스크립트 저장 되도록에 있는 폴더를 지정 합니다.  
  
5.  `overwrite:` true 인 경우 다음 덮어씁니다 파일 이름이 같은 존재 합니다. (True/false) 값을 가질 수 있습니다.  
  
**구문 예제:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>”  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>”  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
convert-sql-statement  
  
1.  `context` 스키마 이름을 지정합니다.  
  
2.  `destination` 출력 파일에 저장할지 여부를 지정 합니다.  
  
    이 특성을 지정 하지 않으면 변환된 된 T-SQL 문이 콘솔에 표시 됩니다. (선택 사항 특성)  
  
3.  `conversion-report-folder` 평가 보고서 저장을 수행할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
4.  `conversion-report-overwrite` 이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
5.  `write-converted-sql-to` 파일 (또는) 변환 된 T-SQL 저장 될 여기서는 폴더 경로 지정 합니다. 폴더 경로와 함께 지정 된 경우는 `sql-files` 특성을 각 소스 파일에는 해당 대상 지정된 된 폴더 아래에 생성 되는 T-SQL 파일 포함 됩니다. 폴더 경로와 함께 지정 된 경우는 `sql` 특성을 변환 된 T-SQL은 지정된 된 폴더 아래 Result.out 라는 파일에 기록 됩니다.  
  
6.  `sql` 변환 될 하나 이상의 문을 MySQL sql 문을 지정 수 수 구분 되는 사용 하는 ";"  
  
7.  `sql-files` T-SQL 코드를 변환할 수 있는 sql 파일의 경로 지정 합니다.  
  
8.  `write-summary-report-to` 요약 보고서가 생성 하는 위치 경로 지정 합니다. 폴더 경로 지정 된 경우에 다음 이름으로 파일 **ConvertSQLReport.XML** 만들어집니다. (선택 사항 특성)  
  
    보고서 작성에 2 viz 하위 범주를 추가 합니다..,:  
  
    -   -오류를 보고 (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로).  
  
    -   자세한 정보 (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로).  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드 명령줄 매개 변수로 필요합니다.  
  
**구문 예제:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
      <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
또는  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
또는  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>다음 단계  
명령줄 옵션에 대 한 자세한 내용은 참조 하십시오. [SSMA 콘솔에서 명령줄 옵션 &#40;MySQLToSQL&#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) 합니다.  
  
샘플 콘솔 스크립트 파일에 대 한 자세한 내용은 참조 하십시오. [샘플 콘솔 스크립트 파일을 작업할 &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
다음 단계에서는 프로젝트 요구 사항에 따라 달라 집니다.  
  
1.  암호 또는 내보내기 지정 하기 위한 암호 가져오기 /를 참조 하십시오 [암호 관리 &#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md)합니다.  
  
2.  보고서를 생성 하는 것에 대 한 참조 [보고서 생성 &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)합니다.  
  
3.  콘솔에서 문제를 해결 하는 것에 대 한 참조 [문제 해결 &#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md)합니다.  
  
