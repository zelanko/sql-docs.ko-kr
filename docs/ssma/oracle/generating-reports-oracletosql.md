---
title: 보고서 생성 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ca9490b53cd55c9d8fdae5d24a045ceaf5a2e83e
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396232"
---
# <a name="generating-reports-oracletosql"></a>보고서 생성(OracleToSQL)
명령을 사용 하 여 수행 되는 특정 활동의 보고서는 SSMA 콘솔에서 개체 트리 수준에 생성 됩니다.  
  
다음 절차를 사용 하 여 보고서를 생성 합니다.  
  
1.  **쓰기 요약-보고서-대상** 매개 변수를 지정 합니다. 관련 보고서는 파일 이름 (지정 된 경우) 또는 지정한 폴더에 저장 됩니다. 파일 이름은 아래 표에 설명 된 대로 시스템에서 미리 정의 되어 있습니다. ** &lt; n &gt; ** 은 동일한 명령을 실행할 때마다 숫자로 증가 하는 고유 파일 번호입니다.  
  
    Reports vis-à-vis 명령은 다음과 같습니다.  
  
    |Sl. 아니요.|명령|보고서 제목|  
    |-|-|-|  
    |1|평가 생성-보고서|AssessmentReport &lt; n &gt; . XML|  
    |2|변환-스키마|SchemaConversionReport &lt; n &gt; . XML|  
    |3|마이그레이션-데이터|DataMigrationReport &lt; n &gt; . XML|  
    |4|convert-sql 문|ConvertSQLReport &lt; n &gt; . XML|  
    |5|동기화-대상|TargetSynchronizationReport &lt; n &gt; . XML|  
    |6|데이터베이스에서 새로 고침|SourceDBRefreshReport &lt; n &gt; . XML|  
  
    > [!IMPORTANT]  
    > 출력 보고서는 평가 보고서와 다릅니다. 전자는 실행 된 명령의 성능에 대 한 보고서 이며 후자는 프로그래밍 방식으로 사용할 수 있는 XML 보고서입니다.  
  
    Sl에서 출력 보고서에 대 한 명령 옵션을 선택 합니다. 아니요. 2-4 위) [OracleToSQL&#41;&#40;SSMA 콘솔 실행](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) 섹션을 참조 하세요.  
  
2.  보고서 세부 정보 표시 설정을 사용 하 여 출력 보고서에서 원하는 세부 정보 범위를 표시 합니다.  
  
    |Sl. 아니요.|명령 및 매개 변수|출력 설명|  
    |-|-|-|  
    |1|verbose = "false"|활동의 요약 된 보고서를 생성 합니다.|  
    |2|verbose = "true"|각 작업에 대 한 요약 및 자세한 상태 보고서를 생성 합니다.|  
  
    > [!NOTE]  
    > 위에서 지정한 보고서의 자세한 정도 설정은 평가 보고서 생성, 변환-스키마, 마이그레이션 데이터, convert-sql 문 명령에 적용 됩니다.  
  
3.  오류 보고 설정을 사용 하 여 오류 보고서에서 원하는 세부 정보 범위를 표시 합니다.  
  
    |Sl. 아니요.|명령 및 매개 변수|출력 설명|  
    |-|-|-|  
    |1|report-errors = "false"|오류/경고/정보 메시지에 대 한 세부 정보가 없습니다.|  
    |2|report-errors = "true"|자세한 오류/경고/정보 메시지입니다.|  
  
    > [!NOTE]  
    > 위에서 지정한 오류 보고 설정은 평가 보고서 생성, 변환-스키마, 마이그레이션 데이터, convert-sql 문 명령에 적용 됩니다.  
  
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
  
### <a name="synchronize-target"></a>동기화-대상:  
**Synchronize-target** 명령에는 동기화 작업에 대 한 오류 보고서의 위치를 지정 하는 **보고서-오류** 매개 변수가 있습니다. 그런 다음 이름이 **TargetSynchronizationReport n 인 파일 &lt; &gt; 입니다. **지정 된 위치에 XML이 생성 됩니다. 여기서 ** &lt; n &gt; ** 은 동일한 명령을 실행할 때마다 숫자로 증가 하는 고유 파일 번호입니다.  
  
**참고:** 폴더 경로를 지정 하면 ' synchronize-target ' 명령에 대 한 선택적 특성이 ' report-errors ' 매개 변수가 됩니다.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**개체 이름:** 동기화에 사용할 개체를 지정 합니다 (개별 개체 이름 또는 그룹 개체 이름이 있을 수도 있음).  
  
**오류가 발생 한 경우:** 동기화 오류를 경고 또는 오류로 지정 하는지 여부를 지정 합니다. 오류 시 사용 가능한 옵션:  
  
-   보고-전체 경고  
  
-   report-경고만  
  
-   fail-스크립트  
  
### <a name="refresh-from-database"></a>새로 고침-데이터베이스에서:  
**데이터베이스에서 새로 고침** 명령에는 새로 고침 작업에 대 한 오류 보고서의 위치를 지정 하는 **보고서-오류** 매개 변수가 있습니다. 그런 다음 이름이 **SourceDBRefreshReport n 인 파일 &lt; &gt; 입니다. **지정 된 위치에 XML이 생성 됩니다. 여기서 ** &lt; n &gt; ** 은 동일한 명령을 실행할 때마다 숫자로 증가 하는 고유 파일 번호입니다.  
  
**참고:** 폴더 경로를 지정 하면 ' synchronize-target ' 명령에 대 한 선택적 특성이 ' report-errors ' 매개 변수가 됩니다.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**개체 이름:** 새로 고침에 사용할 개체를 지정 합니다. 개별 개체 이름이 나 그룹 개체 이름도 지정할 수 있습니다.  
  
**오류가 발생 한 경우:** 새로 고침 오류를 경고 또는 오류로 지정 하는지 여부를 지정 합니다. 오류 시 사용 가능한 옵션:  
  
-   보고-전체 경고  
  
-   report-경고만  
  
-   fail-스크립트  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행 (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
