---
title: (DB2ToSQL) 보고서를 생성 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 69ef5fd9-190d-4c58-8199-b3f77d5e1883
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8938e54e18b5f9d4eef4cf657d53d447ff39b24c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="generating-reports-db2tosql"></a>보고서 생성 (DB2ToSQL)
명령을 사용 하 여 수행 된 특정 작업 보고서는 개체 트리 수준 SSMA 콘솔에 생성 됩니다.  
  
다음 절차를 사용 하 여 보고서를 생성 하려면:  
  
1.  지정 된 **쓰기 요약-보고서-대상** 매개 변수입니다. 관련 된 보고서는 지정 하는 경우 파일 이름으로 저장 되며 또는 폴더에서 지정 합니다. 파일 이름이 시스템 정의 where, 아래 표에서 설명 했 듯이 **&lt;n&gt;** 숫자로 동일한 명령이 실행 될 때마다 증가 하는 고유한 파일 수입니다.  
  
    보고서 vis-...-vis 명령은 다음과 같습니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. 아니요.**|**Command**|**보고서 제목**|  
    |1.|-평가-보고서 생성|AssessmentReport&lt;n&gt;합니다. XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|데이터 마이그레이션|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|동기화 대상|TargetSynchronizationReport&lt;n&gt;합니다. XML|  
    |6|데이터베이스에서 새로 고침|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > 형식의 출력 보고서는 평가 보고서와에서 다릅니다. 전자는 동안 실행 된 명령의 성능에 대 한 보고서, 후자는 프로그래밍 방식 소비에 대 한 XML 보고서입니다.  
  
    (Sl에서에서 출력 보고서에 대 한 명령 옵션에 대 한. 아니요. 위의 2-4), 참조는 [SSMA 콘솔 실행 &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) 섹션.  
  
2.  보고서의 자세한 정도 설정을 사용 하 여 출력 보고서에서 사용자가 원하는 세부의 범위를 나타냅니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. 아니요.**|**명령 및 매개 변수**|**출력 설명**|  
    |1.|자세한 정보 = "false"|활동의 요약 된 보고서를 생성합니다.|  
    |2|verbose=”true”|각 작업에 대 한 요약 및 세부 상태 보고서를 생성합니다.|  
  
    > [!NOTE]  
    > 위에 지정 된 보고서의 자세한 정도 설정이 생성-평가-보고서, convert 스키마, 데이터 마이그레이션, convert sql 문 명령에 대 한 적용 됩니다.  
  
3.  오류 보고 설정을 사용 하 여 오류 보고서에서 사용자가 원하는 세부의 범위를 나타냅니다.  
  
    ||||  
    |-|-|-|  
    |**Sl 합니다. 아니요.**|**명령 및 매개 변수**|**출력 설명**|  
    |1.|report-errors=”false”|오류에 세부 정보 없음 / 경고 / 정보 메시지입니다.|  
    |2|report-errors=”true”|자세한 오류 / 경고 / 정보 메시지입니다.|  
  
    > [!NOTE]  
    > 오류 보고 설정 위에서 지정한 생성-평가-보고서, convert 스키마, 데이터 마이그레이션, convert sql 문 명령에 대 한 적용 됩니다.  
  
**예:**  
  
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
명령 **동기화 대상** 가 **보고 오류-대상** 매개 변수는 동기화 작업에 대 한 오류 보고서의 위치를 지정 합니다. 그런 다음 이름의 파일이 **TargetSynchronizationReport&lt;n&gt;합니다. XML** 지정된 된 위치에 만든 여기서 **&lt;n&gt;** 숫자로 동일한 명령이 실행 될 때마다 증가 하는 고유한 파일 수입니다.  
  
**참고:** 폴더 경로 지정 하는 경우 다음 ' 보고 오류-대상 ' 매개 변수는 명령 ' 동기화 대상 '에 대 한 선택적 특성이 됩니다.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**개체 이름:** 동기화 (가질 수도 있습니다 indivdual 개체 이름이 나 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
**-오류:** 동기화 오류 경고 또는 오류로 지정할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   스크립트 실패  
  
### <a name="refresh-from-database"></a>새로 고침--데이터베이스에서:  
명령 **데이터베이스에서 새로 고침** 가 **보고 오류-대상** 매개 변수는 새로 고침 작업에 대 한 오류 보고서의 위치를 지정 합니다. 그런 다음 이름의 파일이 **SourceDBRefreshReport&lt;n&gt;합니다. XML** 지정된 된 위치에 만든 여기서 **&lt;n&gt;** 숫자로 동일한 명령이 실행 될 때마다 증가 하는 고유한 파일 수입니다.  
  
**참고:** 폴더 경로 지정 하는 경우 다음 ' 보고 오류-대상 ' 매개 변수는 명령 ' 동기화 대상 '에 대 한 선택적 특성이 됩니다.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**개체 이름:** 새로 고침 (가질 수도 있습니다 indivdual 개체 이름이 나 그룹 개체 이름)에 대 한 것으로 간주 하는 개체를 지정 합니다.  
  
**-오류:** 경고 또는 오류도 새로 고침 오류를 지정할 것인지 지정 합니다. 오류에 대 한 사용 가능한 옵션:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   스크립트 실패  
  
## <a name="see-also"></a>관련 항목:  
[SSMA 콘솔 실행](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
