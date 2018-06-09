---
title: 샘플 콘솔 스크립트 파일 (SybaseToSQL) 작업 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Sample Console Script Files
ms.assetid: ef221118-b442-4ca6-9409-6ee1d9f8d948
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 31de0d04238c414b5380bbaa939fe664c7d1c025
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779629"
---
# <a name="working-with-the-sample-console-script-files-sybasetosql"></a>샘플 콘솔 스크립트 파일 (SybaseToSQL) 작업
사용자 참조 및 사용에 대 한 몇 가지 샘플 파일 제품 함께 제공 되었습니다. 이 여기서 쉽게 이러한 스크립트는 최종 사용자의 요구에 맞게 사용자 지정 하는 방법을 설명 합니다.  
  
## <a name="sample-console-script-files"></a>샘플 콘솔 스크립트 파일  
사용자 참조에 대 한 다양 한 시나리오를 다루는 다음 예제 콘솔 스크립트 파일 제공 되었습니다.  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   이 샘플 원본 및 대상 데이터베이스에 사용할 수 있는 연결의 다양 한 모드를 제공 및 사용자 요구 사항에 따라 모드를 선택할 수 있습니다. 이 샘플의 서버 정의 포함합니다.  
  
    -   사용자는 단순히 필요한 원본 및 대상 서버 정의에 값을 변경 하 여 필요한 데이터베이스에 연결할 수 있습니다. 제공 된 예제에서 모든 값이 지정에서 사용할 수 있는 같이 변수 값은 **VariableValueFileSample.xml**합니다.  사용자의 작업 서버 연결 파일에서 다른 모든 연결 매개 변수를 제거할 수 있습니다.  
  
    -   원본 및 대상 서버에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오. [서버 연결 파일을 만드는 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)합니다.  
  
-   **VariableValueFileSample.xml:**  
    샘플 콘솔에서 사용 된 모든 변수가 스크립트 파일 및 `ServersConnectionFileSample.xml` 이 파일의 데이터 정렬 된 되었습니다. 사용자는 단순히 샘플 변수를 교체 해야 하는 샘플 콘솔 스크립트를 실행 합니다. 사용자를 사용 하 여 값은 스토리를 정의 고 스크립트 파일과 함께 추가 명령줄 인수로 서이 파일을 전달 합니다.  
  
    변수 값 파일에 대 한 자세한 내용은 참조 하십시오. [변수 값 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)합니다.  
  
-   **AssessmentReportGenerationSample.xml:**  
    이 샘플에 사용할 수 있는 사용자가 분석을 위해 데이터를 변환 및 마이그레이션해야 그를 시작 하기 전에 xml 평가 보고서를 생성 하는 사용자 수 있습니다.  
  
    에 `generate-assessment-report` 사용자 mandatorily 변수 값을 변경 해야 하는 명령 (참조 **VariableValueFileSample.xml**)에 `object-name` 특성을 사용자가 사용에서 되 고 데이터베이스 이름입니다. 를 지정 하는 개체의 종류에 따라는 `object-type` 값을 변경 해야 합니다.  
  
    사용자가 여러 개체를 평가 하기 위해 / 그 데이터베이스 여러 개 지정할 수 `metabase-object` 에 설명 된 대로 노드는 `generate-assessment-report` 샘플 콘솔 스크립트 파일의 명령의 예제 4입니다.  
  
    보고서 생성에 대 한 자세한 내용은 참조 하십시오. [보고서 생성 &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)합니다.  
  
    > [!NOTE]  
    > -   변수 값 파일 명령줄 인수는 콘솔 응용 프로그램에 전달 VariableValueFileSample.xml 지정 된 사용자로 업데이트 됩니다 확인할 값입니다.  
    > -   확인 하는 콘솔 응용 프로그램에 전달 되는 서버 연결 파일 명령줄 인수는 ServersConnectionFileSample.xml 올바른 서버 매개 변수 값으로 업데이트 됩니다.  
  
-   **SqlStatementConversionSample.xml:**  
    이 샘플은 해당 생성을 사용 하면 `t-sql` 원본 데이터베이스에 대 한 스크립트 `sql` 명령 입력으로 제공 합니다.  
  
    에 `convert-sql-statement` 사용자 mandatorily 변수 값을 변경 해야 하는 명령 (참조 **VariableValueFileSample.xml**)에 `context` 특성을 사용자가 사용에서 되는 데이터베이스 이름입니다. 사용자를 변경 해야 할 됩니다는 `sql` 특성 값을 원본 데이터베이스 `sql` 변환 하는 데 필요한 합리적인 명령입니다.  
  
    사용자는 변환할 sql 파일을 제공할 수도 있습니다. 설명한 것에이 `convert-sql-statement` 샘플 콘솔 스크립트 파일의 명령의 예제 4입니다.  
  
    > [!NOTE]  
    > 변수 값 파일 명령줄 인수는 콘솔 응용 프로그램에 전달 VariableValueFileSample.xml 지정 된 사용자로 업데이트 됩니다 확인할 값입니다.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     이 샘플 마이그레이션을 수행 하기 위해 종단 간 데이터 마이그레이션으로 변환할에서 수 있습니다. 그러면 변경 해야 하는 필수 속성 값 목록은 다음과 같습니다.  
  
    **명령 이름**  
  
    `map-schema`  
  
    원본 데이터베이스와 대상 스키마의 스키마 매핑.  
  
    **Attribute**  
  
    -   `source-schema:` 변환 하는 데 필요한 원본 데이터베이스를 지정 합니다.  
  
    -   `sql-server-schema`: 마이그레이션해야 하는 대상 데이터베이스를 지정 합니다.  
  
    **명령 이름**  
  
    `convert-schema`  
  
    -   소스에서 대상 스키마로 스키마 변환을 수행합니다.  
  
    -   사용자가 여러 개체를 평가 하기 위해 / 그 데이터베이스 여러 개 지정할 수 `metabase-object` 에 설명 된 대로 노드는 `convert-schema` 샘플 콘솔 스크립트 파일의 명령의 예제 4입니다.  
  
    **Attribute**  
  
    `object-name`: 원본 데이터베이스를 지정 합니다. / 개체 변환 하는 데 필요한 이름. 해당 확인 `object-type` 에 지정 된 개체의 유형에 따라 변경 되는 `object-name`  
  
    **명령 이름**  
  
    `synchronize-target`  
  
    -   대상 데이터베이스와 대상 개체를 동기화합니다.  
  
    -   사용자가 여러 개체를 평가 하기 위해 / 그 데이터베이스 여러 개 지정할 수 `metabase-object` 에 설명 된 대로 노드는 `synchronize-target` 샘플 콘솔 스크립트 파일의 명령의 예제 3입니다.  
  
    **Attribute**  
  
    `object-name:` 개체를 만들 수 필요로 하는 이름/sql server 데이터베이스를 지정 합니다. 해당 확인 `object-type` 에 지정 된 개체의 유형에 따라 변경 되는 `object-name`  
  
    **명령 이름**  
  
    `migrate-data`  
  
    -   대상에는 원본 데이터를 마이그레이션합니다.  
  
    -   사용자가 여러 개체를 평가 하기 위해 / 그 데이터베이스 여러 개 지정할 수 `metabase-object` 에 설명 된 대로 노드는 `migrate-data` 예제 콘솔 스크립트 파일의 예 2 명령입니다.  
  
    **Attribute**  
  
    `object-name:` 원본 데이터베이스 지정/마이그레이션에 필요한 이름이 테이블. 해당 확인 `object-type` 에 지정 된 개체의 유형에 따라 변경 되는 `object-name`  
  
## <a name="see-also"></a>관련 항목  
[변수 값 파일을 만드는 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
[서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
[보고서 생성 &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)  
  
