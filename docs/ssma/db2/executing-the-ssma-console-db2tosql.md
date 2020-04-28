---
title: SSMA 콘솔 실행 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 64348e33502e8407e567b8901890246344765f4f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67989685"
---
# <a name="executing-the-ssma-console-db2tosql"></a>SSMA 콘솔 실행 (DB2ToSQL)
Microsoft는 SSMA 활동을 실행 하 고 제어할 수 있는 강력한 스크립트 파일 명령 집합을 제공 합니다. 결과 섹션에서 자세히 설명 합니다. 콘솔 응용 프로그램은이 섹션에 열거 된 특정 표준 스크립트 파일 명령을 사용 합니다.  
  
## <a name="project-script-file-commands"></a>프로젝트 스크립트 파일 명령  
프로젝트 명령은 프로젝트 만들기, 열기, 저장 및 종료 프로젝트를 처리 합니다.  
  
**명령**  
  
create-new-project  
  
새 SSMA 프로젝트를 만듭니다.  
  
**스크립트**  
  
-   `project-folder`생성 되는 프로젝트의 폴더를 나타냅니다.  
  
-   `project-name`프로젝트의 이름을 나타냅니다. {string}  
  
-   `overwrite-if-exists`기존 프로젝트를 덮어쓸지 여부를 나타내는 선택적 특성입니다. 부울  
  
-   `project-type:`선택적 특성입니다. 프로젝트 형식 (예: "2005 2014 2012 2008") 또는 "sql-dmo" 프로젝트 또는 "sql-dmo" 프로젝트 또는 "sql-dmo" 프로젝트 또는 "sql-azure"를 나타냅니다. 기본값은 "2014"입니다.  
  
**예제:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
' Overwrite-exists ' 특성은 기본적으로 **false** 입니다.  
  
' 프로젝트-형식 ' 특성은 기본적으로 **sql server-2008** 입니다.  
  
**명령**  
  
열기-프로젝트  
  
기존 프로젝트를 엽니다.  
  
**스크립트**  
  
-   `project-folder`생성 되는 프로젝트의 폴더를 나타냅니다. 지정 된 폴더가 존재 하지 않으면 명령이 실패 합니다.  {string}  
  
-   `project-name`프로젝트의 이름을 나타냅니다. 지정 된 프로젝트가 없는 경우 명령이 실패 합니다.  {string}  
  
**구문 예제:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
D b 2 용 SSMA 콘솔 응용 프로그램은 이전 버전과의 호환성을 지원 합니다. 이전 버전의 SSMA에서 만든 프로젝트를 열 수 있습니다.  
  
**명령**  
  
save-project  
  
마이그레이션 프로젝트를 저장 합니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<save-project/>  
```  
**명령**  
  
프로젝트 닫기  
  
마이그레이션 프로젝트를 닫습니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>데이터베이스 연결 스크립트 파일 명령  
데이터베이스 연결 명령은 데이터베이스에 연결 하는 데 도움이 됩니다.  
  
-   콘솔에서는 UI의 **찾아보기** 기능이 지원 되지 않습니다.  
  
-   ' 스크립트 파일 만들기 '에 대 한 자세한 내용은 [스크립트 파일 만들기 &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md)를 참조 하세요.  
  
**명령**  
  
연결-원본-데이터베이스  
  
-   원본 데이터베이스에 대 한 연결을 수행 하 고 원본 데이터베이스의 상위 수준 메타 데이터를 로드 하지만 일부 메타 데이터는 로드 하지 않습니다.  
  
-   소스에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 추가 실행이 중지 됩니다.  
  
**스크립트**  
  
서버 정의는 서버 연결 파일이 나 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 name 특성에서 검색 됩니다.  
  
**구문 예제:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**명령**  
  
강제 로드-원본/대상-데이터베이스  
  
-   원본 메타 데이터를 로드 합니다.  
  
-   오프 라인 마이그레이션 프로젝트에서 작업 하는 데 유용 합니다.  
  
-   원본/대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 추가 실행이 중지 됩니다.  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드가 명령줄 매개 변수로 필요 합니다.  
  
**구문 예제:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
또는  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**명령**  
  
다시 연결-원본-데이터베이스  
  
-   원본 데이터베이스에 다시 연결 하지만 연결 원본-데이터베이스 명령과 달리 메타 데이터는 로드 하지 않습니다.  
  
-   원본과의 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 추가 실행이 중지 됩니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**명령**  
  
연결 대상-데이터베이스  
  
-   대상 SQL Server 데이터베이스에 연결 하 고 대상 데이터베이스의 상위 수준 메타 데이터를 로드 하지만 메타 데이터는 완전히 로드 하지 않습니다.  
  
-   대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 추가 실행이 중지 됩니다.  
  
**스크립트**  
  
서버 정의는 서버 연결 파일이 나 스크립트 파일의 서버 섹션에서 각 연결에 대해 정의 된 name 특성에서 검색 됩니다.  
  
**구문 예제:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**명령**  
  
다시 연결-대상-데이터베이스  
  
-   는 대상 데이터베이스에 다시 연결 하지만 연결 대상 데이터베이스 명령과 달리 메타 데이터는 로드 하지 않습니다.  
  
-   대상에 대 한 연결을 설정할 수 없는 경우 오류가 발생 하 고 콘솔 응용 프로그램에서 추가 실행이 중지 됩니다.  
  
**스크립트**  
  
**구문 예제:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>보고서 스크립트 파일 명령  
보고서 명령은 다양 한 SSMA 콘솔 활동의 성능에 대 한 보고서를 생성 합니다.  
  
**명령**  
  
평가 생성-보고서  
  
-   원본 데이터베이스에 대 한 평가 보고서를 생성 합니다.  
  
-   이 명령을 실행 하기 전에 원본 데이터베이스 연결을 수행 하지 않으면 오류가 발생 하 고 콘솔 응용 프로그램이 종료 됩니다.  
  
-   명령을 실행 하는 동안 원본 데이터베이스 서버에 연결 하지 못하면 콘솔 응용 프로그램도 종료 됩니다.  
  
**스크립트**  
  
-   `conversion-report-folder:`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택적 특성)  
  
-   `object-name:`평가 보고서 생성에 고려 되는 개체를 지정 합니다 (개별 개체 이름 또는 그룹 개체 이름이 있을 수 있음).  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `conversion-report-overwrite:`평가 보고서 폴더가 이미 있는 경우 덮어쓸지 여부를 지정 합니다.  
  
    **기본값:** false (선택적 특성)  
  
-   `write-summary-report-to:`요약 보고서가 생성 될 경로를 지정 합니다.  
  
    폴더 경로만 언급 하는 경우 파일 이름 **&lt;AssessmentReport n&gt;. XML** 이 생성 됩니다. (선택적 특성)  
  
    보고서 만들기에는 두 개의 하위 범주가 있습니다.  
  
    -   `report-errors`(= "true/false", 기본값은 "false" (옵션 특성))  
  
    -   `verbose`(= "true/false", 기본값은 "false" (옵션 특성))  
  
**구문 예제:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
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
  
## <a name="migration-script-file-commands"></a>마이그레이션 스크립트 파일 명령  
마이그레이션 명령은 대상 데이터베이스 스키마를 원본 스키마로 변환 하 고 대상 서버로 데이터를 마이그레이션합니다. 마이그레이션 명령의 기본 콘솔 출력 설정은 자세한 오류 보고가 없는 ' 전체 ' 출력 보고서입니다. 원본 개체 트리 루트 노드의 요약만 포함 됩니다.  
  
**명령**  
  
변환-스키마  
  
-   원본에서 대상 스키마로의 스키마 변환을 수행 합니다.  
  
-   이 명령을 실행 하기 전에 원본 또는 대상 데이터베이스 연결을 수행 하지 않거나 명령이 실행 되는 동안 원본 또는 대상 데이터베이스 서버에 대 한 연결이 실패 하면 오류가 발생 하 고 콘솔 응용 프로그램이 종료 됩니다.  
  
**스크립트**  
  
-   `conversion-report-folder:`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택적 특성)  
  
-   `object-name:`스키마를 변환 하는 데 고려 되는 원본 개체를 지정 합니다. 개별 개체 이름 또는 그룹 개체 이름이 있을 수 있습니다.  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `conversion-report-overwrite:`평가 보고서 폴더가 이미 있는 경우 덮어쓸지 여부를 지정 합니다.  
  
    **기본값:** false (선택적 특성)  
  
-   `write-summary-report-to:`요약 보고서가 생성 될 경로를 지정 합니다.  
  
    폴더 경로만 언급 하는 경우 파일 이름 **&lt;SchemaConversionReport n&gt;. XML** 이 생성 됩니다. (선택적 특성)  
  
    보고서 만들기에는 두 개의 하위 범주가 있습니다.  
  
    -   `report-errors`(= "true/false", 기본값은 "false" (옵션 특성))  
  
    -   `verbose`(= "true/false", 기본값은 "false" (옵션 특성))  
  
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
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**명령**  
  
마이그레이션-데이터: 원본 데이터를 대상으로 마이그레이션합니다.  
  
**스크립트**  
  
-   `conversion-report-folder:`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택적 특성)  
  
-   `object-name:`데이터 마이그레이션에 고려 되는 원본 개체를 지정 합니다 (개별 개체 이름 또는 그룹 개체 이름이 있을 수 있음).  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `conversion-report-overwrite:`평가 보고서 폴더가 이미 있는 경우 덮어쓸지 여부를 지정 합니다.  
  
    **기본값:** false (선택적 특성)  
  
-   `write-summary-report-to:`요약 보고서가 생성 될 경로를 지정 합니다.  
  
    폴더 경로만 언급 하는 경우 파일 이름 **&lt;DataMigrationReport n&gt;. XML** 이 생성 됩니다. (선택적 특성)  
  
    보고서 만들기에는 두 개의 하위 범주가 있습니다.  
  
    -   `report-errors`(= "true/false", 기본값은 "false" (옵션 특성))  
  
    -   `verbose`(= "true/false", 기본값은 "false" (옵션 특성))  
  
**구문 예제:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
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
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>마이그레이션 준비 스크립트 파일 명령  
마이그레이션 준비 명령은 원본 데이터베이스와 대상 데이터베이스 간의 스키마 매핑을 시작 합니다.  
  
**명령**  
  
맵-스키마  
  
원본 데이터베이스와 대상 스키마의 스키마 매핑  
  
**스크립트**  
  
-   `source-schema`마이그레이션하려는 원본 스키마를 지정 합니다.  
  
-   `sql-server-schema`마이그레이션할 대상 스키마를 지정 합니다.  
  
**구문 예제:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
**명령**  
  
맵-스키마  
  
원본 데이터베이스와 대상 스키마의 스키마 매핑  
  
**스크립트**  
  
`source-schema`마이그레이션하려는 원본 스키마를 지정 합니다.  
  
`sql-server-schema`마이그레이션할 대상 스키마를 지정 합니다.  
  
**구문 예제:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>관리 효율성 스크립트 파일 명령  
관리 효율성 명령은 대상 데이터베이스 개체를 원본 데이터베이스와 동기화 하는 데 도움이 됩니다.  
  
마이그레이션 명령의 기본 콘솔 출력 설정은 자세한 오류 보고가 없는 ' 전체 ' 출력 보고서입니다. 원본 개체 트리 루트 노드의 요약만 포함 됩니다.  
  
**명령**  
  
동기화-대상  
  
-   대상 개체를 대상 데이터베이스와 동기화 합니다.  
  
-   원본 데이터베이스에 대해이 명령을 실행 하면 오류가 발생 합니다.  
  
-   이 명령을 실행 하기 전에 대상 데이터베이스 연결이 수행 되지 않거나 명령 실행 중에 대상 데이터베이스 서버에 대 한 연결이 실패 하면 오류가 발생 하 고 콘솔 응용 프로그램이 종료 됩니다.  
  
**스크립트**  
  
-   `object-name:`대상 데이터베이스와 동기화 하는 데 사용 되는 대상 개체를 지정 합니다 (개별 개체 이름 또는 그룹 개체 이름이 있을 수 있음).  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `on-error:`동기화 오류를 경고 또는 오류로 지정 하는지 여부를 지정 합니다. 오류 시 사용 가능한 옵션:  
  
    -   보고-전체 경고  
  
    -   report-경고만  
  
    -   fail-스크립트  
  
-   `report-errors-to:`동기화 작업에 대 한 오류 보고서의 위치를 지정 합니다 (옵션 특성). 폴더 경로만 지정 하면 파일 이름 **TargetSynchronizationReport** 이 만들어집니다.  
  
**구문 예제:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
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
**명령**  
  
데이터베이스에서 새로 고침  
  
-   데이터베이스에서 소스 개체를 새로 고칩니다.  
  
-   대상 데이터베이스에 대해이 명령을 실행 하면 오류가 발생 합니다.  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드가 명령줄 매개 변수로 필요 합니다.  
  
-   `object-name:`원본 데이터베이스에서 새로 고치는 것으로 간주 되는 원본 개체를 지정 합니다. 개별 개체 이름 또는 그룹 개체 이름을 가질 수 있습니다.  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `on-error:`새로 고침 오류를 경고 또는 오류로 지정 하는지 여부를 지정 합니다. 오류 시 사용 가능한 옵션:  
  
    -   보고-전체 경고  
  
    -   report-경고만  
  
    -   fail-스크립트  
  
-   `report-errors-to:`폴더 경로만 지정 된 경우 새로 고침 작업 (옵션 특성)에 대 한 오류 보고서의 위치를 지정 합니다. 그러면 파일 이름 **SourceDBRefreshReport** 이 만들어집니다.  
  
**구문 예제:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
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
스크립트 생성 명령은 두 가지 작업을 수행 합니다. 스크립트 파일에 콘솔 출력을 저장 하는 데 도움이 됩니다. 지정한 매개 변수를 기반으로 하 여 콘솔 또는 파일에 T-sql 출력을 기록 합니다.  
  
**명령**  
  
스크립트로 저장  
  
개체의 스크립트를 메타 베이스 = 대상이 될 때 언급 된 파일에 저장 하는 데 사용 됩니다 .이는 스크립트를 가져오고 대상 데이터베이스에서 동일 하 게 실행 하는 동기화 명령의 대안입니다.  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드가 명령줄 매개 변수로 필요 합니다.  
  
-   `object-name:`스크립트를 저장할 개체를 지정 합니다. (개별 개체 이름 또는 그룹 개체 이름이 있을 수 있음)  
  
-   `object-type:`개체 이름 특성에 지정 된 개체의 유형을 지정 합니다. 개체 범주가 지정 된 경우 개체 유형은 "category"가 됩니다.  
  
-   `metabase:`원본 또는 대상 메타 베이스 인지 여부를 지정 합니다.  
  
-   `destination:`파일 이름에 파일 이름을 지정 하지 않은 경우 스크립트를 저장 해야 하는 경로 또는 폴더를 지정 합니다 (object_name 특성 값).  
  
-   `overwrite:`true 이면 동일한 파일 이름이 있는 경우 덮어씁니다. 값 (true/false)이 있을 수 있습니다.  
  
**구문 예제:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
또는  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**명령**  
  
convert-sql 문  
  
-   `context`스키마 이름을 지정 합니다.  
  
-   `destination`출력을 파일에 저장할지 여부를 지정 합니다.  
  
    이 특성을 지정 하지 않으면 변환 된 T-sql 문이 콘솔에 표시 됩니다. (선택적 특성)  
  
-   `conversion-report-folder`평가 보고서를 저장할 수 있는 폴더를 지정 합니다. (선택적 특성)  
  
-   `conversion-report-overwrite`평가 보고서 폴더가 이미 있는 경우 덮어쓸지 여부를 지정 합니다.  
  
    **기본값:** false (선택적 특성)  
  
-   `write-converted-sql-to`변환 된 T-sql을 저장할 파일 (또는) 폴더 경로를 지정 합니다. 폴더 경로를 `sql-files` 특성과 함께 지정 하면 각 원본 파일에 지정 된 폴더에 해당 하는 대상 t-sql 파일이 생성 됩니다. `sql` 특성을 사용 하 여 폴더 경로를 지정 하면 변환 된 t-sql은 지정 된 폴더에 있는 **Result. out** 이라는 파일에 기록 됩니다.  
  
-   `sql`변환할 DB2 sql 문을 지정 합니다. ";"을 사용 하 여 하나 이상의 문을 구분할 수 있습니다.  
  
-   `sql-files`T-sql 코드로 변환 해야 하는 sql 파일의 경로를 지정 합니다.  
  
-   `write-summary-report-to`보고서가 생성 될 경로를 지정 합니다. 폴더 경로만 설명 된 경우 이름이 **Convertsqlreport .xml** 인 파일을 만듭니다. (선택적 특성)  
  
    보고서를 만들 때 두 개의 하위 범주인 시각화.  
  
    -   report-errors (= "true/false" 이며 기본값은 "false" (옵션 특성))입니다.  
  
    -   verbose (= "true/false" 이며 기본값은 "false" (옵션 특성))입니다.  
  
**스크립트**  
  
하나 또는 여러 메타 베이스 노드가 명령줄 매개 변수로 필요 합니다.  
  
**구문 예제:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
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
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
또는  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>다음 단계  
명령줄 옵션에 대 한 자세한 내용은 [SSMA 콘솔의 명령줄 옵션 &#40;DB2ToSQL&#41;](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) 을 참조 하세요.  
  
샘플 콘솔 스크립트 파일에 대 한 자세한 내용은 [샘플 콘솔 스크립트 파일 작업 &#40;DB2ToSQL](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md) 를 참조 하세요&#41;  
  
다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   암호 또는 내보내기/가져오기 암호를 지정 하려면 [DB2ToSQL&#41;&#40;암호 관리 ](../../ssma/db2/managing-passwords-db2tosql.md)를 참조 하세요.  
  
-   보고서를 생성 하려면 [DB2ToSQL&#41;&#40;보고서 생성 ](../../ssma/db2/generating-reports-db2tosql.md)을 참조 하세요.  
  
-   콘솔의 문제 해결에 대해서는 [문제 해결 &#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md)을 참조 하세요.  
  
