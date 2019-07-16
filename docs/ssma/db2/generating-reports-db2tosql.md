---
title: 보고서 (DB2ToSQL) 생성 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 69ef5fd9-190d-4c58-8199-b3f77d5e1883
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2d96b82e3ce883bcf9e704ea001024228be81761
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989652"
---
# <a name="generating-reports-db2tosql"></a>보고서 생성 (DB2ToSQL)
개체 트리 수준 SSMA 콘솔의 명령을 사용 하 여 수행 되는 특정 활동의 보고서를 생성 됩니다.  
  
보고서를 생성 하려면 다음 절차를 따르십시오.  
  
1.  지정 된 **쓰기-요약-보고 대상** 매개 변수입니다. 지정 하는 경우 관련 된 보고서 파일 이름으로 저장 됩니다 또는 폴더를 지정 합니다. 파일 이름은 시스템 정의 where, 아래 표에서 설명 했 듯이 **&lt;n&gt;** 동일한 명령 실행할 때마다를 사용 하 여 숫자를 사용 하 여 증가 하는 고유한 파일입니다.  
  
    보고서 vis-...-vis 명령은 다음과 같습니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. No.**|**Command**|**보고서 제목**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|데이터 마이그레이션|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|동기화 대상|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|데이터베이스에서 새로 고침|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > 형식의 출력 보고서는 평가 보고서와 다릅니다. 전자는 하는 동안 실행 된 명령의 성능에 대 한 보고서, 후자는 XML 보고서를 프로그래밍 방식으로 사용 합니다.  
  
    (Sl에서에서 출력 보고서에 대 한 명령 옵션. 아니요. 위의 2-4)를 참조 합니다 [SSMA 콘솔 실행 &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) 섹션.  
  
2.  세부 정보 보고서 세부 정보 표시 설정을 사용 하 여 출력 보고서에서 원하는 범위를 나타냅니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. No.**|**명령 및 매개 변수**|**출력 설명**|  
    |1|verbose="false"|활동의 요약 된 보고서를 생성합니다.|  
    |2|verbose="true"|각 작업에 대 한 요약 및 자세한 상태 보고서를 생성합니다.|  
  
    > [!NOTE]  
    > 위에 지정 된 보고서의 자세한 정도 설정이-평가-보고서 생성, 스키마 변환, 데이터 마이그레이션, 문-변환-sql 명령에 적용 됩니다.  
  
3.  오류 보고 설정을 사용 하는 오류 보고서에 원하는 세부 범위를 나타냅니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. No.**|**명령 및 매개 변수**|**출력 설명**|  
    |1|report-errors="false"|오류 세부 정보 없음 / 경고 / 정보 메시지입니다.|  
    |2|report-errors="true"|자세한 오류 / 경고 / 정보 메시지입니다.|  
  
    > [!NOTE]  
    > 위에 지정 된 오류 보고 설정-평가-보고서 생성, 스키마 변환, 데이터 마이그레이션, 문-변환-sql 명령에 적용 됩니다.  
  
**예제:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>동기화 대상:  
명령을 **동기화 대상** 했습니다 **보고서 오류-간** 동기화 작업에 대 한 오류 보고서의 위치를 지정 하는 매개 변수. 그런 다음 이름의 파일이 **TargetSynchronizationReport&lt;n&gt;합니다. XML** 지정된 된 위치에 만들어진 위치 **&lt;n&gt;** 동일한 명령 실행할 때마다를 사용 하 여 숫자를 사용 하 여 증가 하는 고유한 파일입니다.  
  
**참고:** 폴더 경로 지정 하는 경우 ' 보고서-오류-를 ' 매개 변수는 명령 ' 동기화 대상 '의 선택적 특성이 됩니다.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** 동기화 (가질 수도 있습니다 개별 개체 이름 또는 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
**오류 발생 시:** 동기화 오류 경고 또는 오류도 지정할지 여부를 지정 합니다. 오류 발생 시에 대 한 사용 가능한 옵션:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   스크립트 실패  
  
### <a name="refresh-from-database"></a>새로 고침--데이터베이스:  
명령을 **데이터베이스에서 새로 고침** 했습니다 **보고서 오류-간** 새로 고침 작업에 대 한 오류 보고서의 위치를 지정 하는 매개 변수. 그런 다음 이름의 파일이 **SourceDBRefreshReport&lt;n&gt;합니다. XML** 지정된 된 위치에 만들어진 위치 **&lt;n&gt;** 동일한 명령 실행할 때마다를 사용 하 여 숫자를 사용 하 여 증가 하는 고유한 파일입니다.  
  
**참고:** 폴더 경로 지정 하는 경우 ' 보고서-오류-를 ' 매개 변수는 명령 ' 동기화 대상 '의 선택적 특성이 됩니다.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** 새로 고침 (가질 수도 있습니다 개별 개체 이름 또는 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
**오류 발생 시:** 경고 또는 오류 새로 고침 오류를 지정할지 여부를 지정 합니다. 오류 발생 시에 대 한 사용 가능한 옵션:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   스크립트 실패  
  
## <a name="see-also"></a>관련 항목  
[SSMA 콘솔 실행](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
