---
title: "SSMA 콘솔 (SybaseToSQL) 실행 | Microsoft Docs"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 998a42b80fa415537051693467b337f07c9ba381
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="executing-the-ssma-console-sybasetosql"></a>SSMA 콘솔 (SybaseToSQL)를 실행합니다.
Microsoft 파일 명령을 실행 및 제어 SSMA 활동을 스크립트의 강력한 집합 제공 합니다. 마샬링과 이후 섹션에서 자세히 설명 동일 합니다.  
  
## <a name="script-file-commands"></a>스크립트 파일 명령  
콘솔 응용 프로그램은이 섹션의 열거형으로 특정 표준 스크립트 파일 명령을 사용합니다.  
  
## <a name="project-commands"></a>프로젝트 명령  
프로젝트 명령을 처리 프로젝트 만들기, 열기, 저장 하 고 프로젝트를 종료 합니다.  
  
### <a name="create-new-project"></a>-새-프로젝트 만들기  
이 명령은 새 SSMA 프로젝트를 만듭니다.  
  
-   `project-folder`만든 가져오기 프로젝트의 폴더를 나타냅니다.  
  
-   `project-name`프로젝트의 이름을 나타냅니다. {string}  
  
-   `overwrite-if-exists`선택적 특성 기존 프로젝트를 덮어쓸지 여부를 나타냅니다. {부울}  
  
-   `project-type:`선택적 특성입니다. "Sql server 2005" 프로젝트 또는 프로젝트 "sql server 2008" 또는 "sql server 2012" 프로젝트 또는 프로젝트 "sql server 2014" 또는 "sql azure" 프로젝트 프로젝트 형식을 나타냅니다. 기본값은 "sql-서버-2008"입니다.  
  
**구문 예제:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type=”<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>”  
/>  
```  
' 덮어쓰기-이미 있는 경우-' 특성은 **false** 기본적으로 합니다.  
  
' 프로젝트 type' 특성은 **sql-서버-2008** 기본적으로 합니다.  
  
### <a name="open-project"></a>프로젝트 열기  
이 명령은 프로젝트를 엽니다.

-   `project-folder`만든 가져오기 프로젝트의 폴더를 나타냅니다. 이 명령은 지정 된 폴더가 존재 하지 않는 경우 실패 합니다.  {string}  
  
-   `project-name`프로젝트의 이름을 나타냅니다. 이 명령은 지정 된 프로젝트가 존재 하지 않는 경우 실패 합니다.  {string}  
  
**구문 예제:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA SAP ASE 콘솔 응용 프로그램에 대 한 이전 버전과 호환성을 지원합니다. SSMA의 이전 버전에서 만든 프로젝트를 열려면를 사용할 수 있습니다.  
  
### <a name="save-project"></a>프로젝트 저장  
이 명령은 마이그레이션 프로젝트를 저장합니다.  
  
**구문 예제:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>프로젝트 닫기  
이 명령은 마이그레이션 프로젝트를 닫습니다.  
  
**구문 예제:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
' If 수정 ' 특성은 선택 사항 **무시** 기본적으로 합니다.  
  
## <a name="database-connection-commands"></a>데이터베이스 연결 명령  
데이터베이스 연결 명령을 데이터베이스에 연결할 수 있습니다.  
  
> [!NOTE]  
> - **찾아보기** UI의 기능을 콘솔에서 지원 되지 않습니다.  
> - 스크립트 파일 만들기 '에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>-소스-데이터베이스 연결  
이 명령은 원본 데이터베이스에 수행 하 고 원본 데이터베이스에만 메타 데이터의 높은 수준의 메타 데이터를 로드 합니다.
  
원본에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 더 이상 실행 합니다.
  
서버 정의 서버 연결 파일 또는 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 이름 특성에서 검색 됩니다.  
  
**구문 예제:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>force-부하-원본/대상 데이터베이스  
이 명령은 원본 메타 데이터를 로드 하 고 오프 라인 마이그레이션 프로젝트에서 작업 하는 데 유용 합니다.  
  
소스/대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
이 명령은 명령줄 매개 변수로 메타 베이스 노드 하나 또는 여러 개 필요합니다.  
  
**구문 예제:**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>다시 연결-소스-데이터베이스  
이 명령은 원본 데이터베이스에 다시 연결 하지만 연결 원본 데이터베이스 명령과 달리 모든 메타 데이터를 로드 하지 않습니다.  
  
오류가 생성 됩니다 (다시) 원본과 연결을 설정할 수 없는 경우와 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
**구문 예제:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>대상 연결-데이터베이스  
이 명령은 대상 SQL Server 데이터베이스에 연결 하 고 대상 데이터베이스의 상위 수준 메타 데이터는 있지만 메타 데이터가 아니라를 완전히 로드 합니다.  
  
대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
서버 정의 서버 연결 파일 또는 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 이름 특성에서 검색 됩니다.  
  
**구문 예제:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>대상 다시 연결-데이터베이스  
  
이 명령은 대상 데이터베이스에 다시 연결 하지만 연결 대상 데이터베이스 명령과 달리 모든 메타 데이터를 로드 하지 않습니다.  
  
오류가 생성 됩니다 (다시) 대상에 대 한 연결을 설정할 수 없는 경우와 콘솔 응용 프로그램에서 더 이상 실행 합니다.  
  
**구문 예제:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>보고서 명령  
SSMA 콘솔의 다양 한 작업의 성능에는 보고서를 생성 하는 보고서 명령입니다.  
  
### <a name="generate-assessment-report"></a>-평가-보고서 생성  
  
이 명령은 원본 데이터베이스에서 평가 보고서를 생성합니다.  
  
이 명령을 실행 하기 전에 원본 데이터베이스 연결을 수행 하지 않는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
또한 명령 실행 하는 동안 원본 데이터베이스 서버에 연결 하지 못한 콘솔 응용 프로그램을 종료 발생 합니다.  
  
-   `conversion-report-folder:`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
-   `object-name:`평가 보고서 생성 (지원 개별 개체 이름 또는 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
-   `object-type:`(개체 유형 "범주"이 됩니다 개체 범주의 지정 된) 경우 개체 이름 특성에 명시 된 개체의 유형을 지정 합니다.  
  
-   `conversion-report-overwrite:`이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
-   `write-summary-report-to:`보고서를 생성할 수는 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **AssessmentReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    보고서를 만드는 두 개의 추가 하위 범주에 있습니다.  
  
    -   `report-errors`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>”             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>마이그레이션 명령  
마이그레이션 명령 소스 스키마에 대상 데이터베이스 스키마를 변환 및 대상 서버에 데이터를 마이그레이션합니다.  
  
### <a name="convert-schema"></a>스키마 변환  
이 명령은 원본에서 대상 스키마로 스키마 변환을 수행합니다.  
  
이 명령을 실행 하기 전에 원본 또는 대상 데이터베이스 연결을 수행 하지 않으면 명령 실행 하는 동안 소스 또는 대상 데이터베이스 서버에 연결할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
-   `conversion-report-folder:`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
-   `object-name:`스키마 (지원 개별 개체 이름 또는 그룹 개체 이름)을 변환 하기 위한 것으로 간주 하는 원본 개체를 지정 합니다.  
  
-   `object-type:`(개체 유형 "범주"이 됩니다 개체 범주의 지정 된) 경우 개체 이름 특성에 명시 된 개체의 유형을 지정 합니다.  
  
-   `conversion-report-overwrite:`이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
-   `write-summary-report-to:`요약 보고서가 생성 된 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **SchemaConversionReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    보고서를 만드는 두 개의 추가 하위 범주에 있습니다.  
  
    -   `report-errors`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
또는  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>데이터 마이그레이션  
이 명령은 대상에 원본 데이터를 마이그레이션합니다.  
  
-   `object-name:`마이그레이션에 대 한 것으로 간주 원본 개체를 지정 합니다. 데이터 (지원 개별 개체 이름 또는 그룹 개체 이름).  
  
-   `object-type:`(개체 유형 "범주"이 됩니다 개체 범주의 지정 된) 경우 개체 이름 특성에 명시 된 개체의 유형을 지정 합니다.  
  
-   `write-summary-report-to:`보고서를 생성할 수는 경로 지정 합니다.  
  
    폴더 경로 지정 된 경우에 다음 이름으로 파일 **DataMigrationReport&lt;n&gt;합니다. XML** 만들어집니다. (선택 사항 특성)  
  
    보고서를 만드는 두 개의 추가 하위 범주에 있습니다.  
  
    -   `report-errors`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
    -   `verbose`(= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로)  
  
**구문 예제:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
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
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>마이그레이션 준비 명령  
마이그레이션 준비 명령은 원본 및 대상 데이터베이스 간에 스키마 매핑을 시작합니다.  
  
> [!NOTE]  
> 마이그레이션 명령에 대 한 설정 기본 콘솔 출력은 보고 하지 않으려면 자세한 오류 사용 하 여 '전체' 출력 보고서: 소스 개체 트리의 루트 노드에서 요약 합니다.  
  
### <a name="map-schema"></a>스키마 맵  
이 명령은 원본 데이터베이스와 대상 스키마의 스키마 매핑을 제공합니다.  
  
-   `source-schema`마이그레이션할 원본 스키마를 지정 합니다.  
  
-   `sql-server-schema`소스 스키마 마이그레이션할 수 있는 대상 스키마를 지정 합니다.  
  
**구문 예제:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>관리 효율성 명령  
원본 데이터베이스와 대상 데이터베이스 개체를 동기화 하는 데 도움이 관리 효율성 명령.  
  
> [!NOTE]  
> 마이그레이션 명령에 대 한 설정 기본 콘솔 출력은 보고 하지 않으려면 자세한 오류 사용 하 여 '전체' 출력 보고서: 소스 개체 트리의 루트 노드에서 요약 합니다.  
  
### <a name="synchronize-target"></a>동기화 대상  
이 명령은 대상 데이터베이스와 대상 개체를 동기화합니다.  
 
이 명령은 원본 데이터베이스에 대해 실행 될 경우 오류가 발생 합니다.  
  
이 명령을 실행 하기 전에 대상 데이터베이스 연결을 수행 하지 않으면 명령 실행 중에 대상 데이터베이스 서버에 연결할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램 종료 합니다.  
  
-   `object-name:`대상 데이터베이스 (지원 개별 개체 이름 또는 그룹 개체 이름)와 동기화 할 대상으로 고려 대상 개체를 지정 합니다.  
  
-   `object-type:`(개체 유형 "범주"이 됩니다 개체 범주의 지정 된) 경우 개체 이름 특성에 명시 된 개체의 유형을 지정 합니다.  
  
-   `on-error:`동기화 오류 경고 또는 오류로 지정할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
    -   경고로 보고서 합계  
  
    -   보고서-each-으로-경고  
  
    -   스크립트 실패  
  
-   `report-errors-to:`(선택 사항 특성) 동기화 작업에 대 한 오류 보고서의 위치를 지정합니다. 폴더 경로 지정 하는 경우에 다음 이름으로 파일 **TargetSynchronizationReport.XML** 만들어집니다.  
  
**구문 예제:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
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
  
### <a name="refresh-from-database"></a>데이터베이스에서 새로 고침  
이 명령은 데이터베이스에서 원본 개체를 새로 고칩니다.  
  
이 명령은 대상 데이터베이스에 대해 실행 될 경우 오류가 생성 됩니다.  
  
이 명령은 명령줄 매개 변수로 메타 베이스 노드 하나 또는 여러 개 필요합니다.  
  
-   `object-name:`(지원 개별 개체 이름 또는 그룹 개체 이름)에 원본 데이터베이스에서 새로 고침에 대 한 것으로 간주 원본 개체를 지정 합니다.  
  
-   `object-type:`지정 하는 경우 개체 범주는 개체 유형 "범주"이 됩니다 개체 이름 특성에 지정 된 개체의 유형을 지정 합니다.  
  
-   `on-error:`경고 또는 오류를 새로 고침 오류 호출할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
    -   경고로 보고서 합계  
  
    -   보고서-each-으로-경고  
  
    -   스크립트 실패  
  
-   `report-errors-to:`(선택 사항 특성)의 새로 고침 작업에 대 한 오류 보고서의 위치를 지정 합니다. 폴더 경로 지정 하는 경우에 다음 이름으로 파일 **SourceDBRefreshReport.XML** 만들어집니다.  
  
**구문 예제:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
또는  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
또는  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>스크립트 생성 명령  
이중 작업을 수행 하는 스크립트 생성 명령을: 콘솔 스크립트 파일에 출력을 절약할 및 T-SQL 출력은 콘솔 이나 지정한 매개 변수를 기준으로 파일을 기록 합니다.  
  
### <a name="save-as-script"></a>스크립트로 저장  
이 명령은 저장 하는 데 사용 됩니다 파일에 개체의 스크립트를 언급 된 경우 메타 베이스 대상 = 합니다. 이것이 스크립트 하 고 대상 데이터베이스에서 실행 하는 동일한 한다는 점에서 동기화 명령에 대 한 대안입니다.  
  
이 명령은 명령줄 매개 변수로 메타 베이스 노드 하나 또는 여러 개 필요합니다.  
  
-   `object-name:`(지원 개별 개체 이름 또는 그룹 개체 이름)에 저장 되도록 해당 스크립트는 개체를 지정 합니다.  
  
-   `object-type:`(개체 유형 "범주"이 됩니다 개체 범주의 지정 된) 경우 개체 이름 특성에 명시 된 개체의 유형을 지정 합니다.  
  
-   `metabase:`원본 인지를 지정 하거나 메타 베이스를 대상 지정 합니다.  
  
-   `destination:`경로 또는 스크립트를 저장 해야 하는 폴더를 지정 합니다. 파일 이름이 제공 되지 않습니다 (object_name 특성 값) 형식.out에 파일 이름을 제공 됩니다.
  
-   `overwrite:`True 인 경우, 다음 것 같은 파일 이름을 있으면 덮어씁니다. (True/false) 값을 가질 수 있습니다.  
  
**구문 예제:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert sql 문
이 명령은 SQL 문을 변환합니다.  
  
-   `context`스키마 이름을 지정합니다.  
  
-   `destination`출력 파일에 저장할지 여부를 지정 합니다.  
  
    이 특성을 지정 하지 않으면 변환된 된 T-SQL 문이 콘솔에 표시 됩니다. (선택 사항 특성)  
  
-   `conversion-report-folder`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택 사항 특성)  
  
-   `conversion-report-overwrite`이미 있는 경우 평가 보고서 폴더를 덮어쓸 것인지 지정 합니다.  
  
    **기본값:** false입니다. (선택 사항 특성)  
  
-   `write-converted-sql-to`변환 된 T-SQL 해야 저장 파일 (또는) 폴더 경로 지정 합니다. 폴더 경로와 함께 지정 된 경우는 `sql-files` 특성을 각 소스 파일에는 해당 대상 T-SQL 파일 지정된 된 폴더 아래에 생성 합니다. 폴더 경로와 함께 지정 된 경우는 `sql` 특성을 변환 된 T-SQL은 지정된 된 폴더 아래 Result.out 라는 파일에 기록 됩니다.  
  
-   `sql`변환 될 Sybase sql 문을 지정 하나 이상의 문을 사용 하 여 구분할 수 있습니다는 ";"  
  
-   `sql-files`T-SQL 코드를 변환할 수 있는 sql 파일의 경로 지정 합니다.  
  
-   `write-summary-report-to`요약 보고서가 생성 하는 위치 경로 지정 합니다. 폴더 경로 지정 된 경우에 다음 이름으로 파일 **ConvertSQLReport.XML** 만들어집니다. (선택 사항 특성)  
  
    요약 보고서 작성에 두 개의 추가 하위 즉에 있습니다.  
  
    -   -오류를 보고 (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로).  
  
    -   자세한 정보 (= "true/false" 이며 기본값은 "false" (선택 사항 특성)으로).  
  
이 명령은 명령줄 매개 변수로 메타 베이스 노드 하나 또는 여러 개 필요합니다.  
  
**구문 예제:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
또는  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
또는  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>다음 단계  
명령줄 옵션에 대 한 자세한 내용은 참조 하십시오. [SSMA 콘솔 (AccessToSQL)의 명령줄 옵션](../access/command-line-options-in-ssma-console-accesstosql.md)합니다.  
  
샘플 콘솔 스크립트 파일에 대 한 자세한 내용은 참조 [샘플 콘솔 스크립트 파일 &#40; 사용 SybaseToSQL &#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
다음 단계에서는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   암호 또는 내보내기 지정 하기 위한 암호 가져오기 /를 참조 하십시오 [암호 관리 &#40; SybaseToSQL &#41; ](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   보고서를 생성 하는 것에 대 한 참조 [보고서 생성 &#40; SybaseToSQL &#41; ](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   콘솔에서 문제를 해결 하는 것에 대 한 참조 [문제 해결 &#40; SybaseToSQL &#41; ](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  

