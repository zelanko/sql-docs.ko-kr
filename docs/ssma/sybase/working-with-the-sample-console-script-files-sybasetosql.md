---
title: 샘플 콘솔 스크립트 파일 (SybaseToSQL) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Sample Console Script Files
ms.assetid: ef221118-b442-4ca6-9409-6ee1d9f8d948
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4a87b213731ac0b8cb1b76eb87b1997f86157c6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902675"
---
# <a name="working-with-the-sample-console-script-files-sybasetosql"></a>샘플 콘솔 스크립트 파일 작업(SybaseToSQL)
사용자 참조 및 사용에 대 한 몇 가지 샘플 파일 제품와 함께 제공 되었습니다. 이 섹션에서는 최종 사용자 요구에 맞게 이러한 스크립트를 쉽게 사용자 지정 하는 방법은 설명 합니다.  
  
## <a name="sample-console-script-files"></a>샘플 콘솔 스크립트 파일  
사용자 참조에 대 한 다양 한 시나리오를 다루는 다음 샘플 콘솔 스크립트 파일 제공 되었습니다.  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   이 샘플 원본 및 대상 데이터베이스에 연결을 사용할 수 있는 다양 한 모드를 제공 하 고 사용자의 요구 사항에 따라 모드를 선택할 수 있습니다. 이 샘플 서버 정의 포함합니다.  
  
    -   사용자는 단순히 필요한 원본 및 대상 서버 정의에 값을 변경 하 여 필요한 데이터베이스에 연결할 수 있습니다. 제공 된 예제에서 모든 값이 지정에서 사용할 수 있는 값으로 변수를 **VariableValueFileSample.xml**합니다.  사용자의 작업 서버 연결 파일에서 다른 모든 연결 매개 변수를 제거할 수 있습니다.  
  
    -   원본 및 대상 서버에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)합니다.  
  
-   **VariableValueFileSample.xml:**  
    샘플 콘솔에서 사용 된 모든 변수가 스크립트 파일 및 `ServersConnectionFileSample.xml` 이 파일에서 데이터 정렬 되어 있어야 합니다. 사용자가 단순히 샘플 변수를 대체 하는 샘플 콘솔 스크립트를 실행 하려면 사용자를 사용 하 여 값 항목 정의 하 고 스크립트 파일과 함께 추가 명령줄 인수로이 파일을 전달 합니다.  
  
    변수 값 파일에 대 한 자세한 내용은 참조 하세요. [변수 값 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)합니다.  
  
-   **AssessmentReportGenerationSample.xml:**  
    이 샘플에는 사용할 수 있는 사용자가 분석을 위해 데이터를 마이그레이션하고 변환 하기 전에 그 xml 평가 보고서를 생성 하려면 사용자 수 있습니다.  
  
    에 `generate-assessment-report` mandatorily 변수 값을 변경 하려면 사용자가 명령을 (참조 **VariableValueFileSample.xml**)에 `object-name` 특성을 사용자가 사용에서 하는 데이터베이스 이름입니다. 지정 된 개체의 종류에 따라는 `object-type` 값을 변경 해야 합니다.  
  
    사용자가 여러 개체를 평가 / 그 데이터베이스 여러 개 지정할 수 있습니다 `metabase-object` 에 설명 된 대로 노드는 `generate-assessment-report` 샘플 콘솔 스크립트 파일의 예제 4 명령입니다.  
  
    보고서 생성에 대 한 자세한 내용은 참조 하세요. [보고서 생성 &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)합니다.  
  
    > [!NOTE]  
    > -   변수 값 파일 명령줄 인수를 콘솔 응용 프로그램에 전달 되 고 VariableValueFileSample.xml 지정 된 사용자를 사용 하 여 업데이트 되는 확인 값입니다.  
    > -   콘솔 응용 프로그램에 전달 되는 서버 연결 파일 명령줄 인수를 ServersConnectionFileSample.xml 올바른 서버 매개 변수 값으로 업데이트 됩니다 확인 하십시오.  
  
-   **SqlStatementConversionSample.xml:**  
    이 샘플에 사용자가 해당 생성할 수 있도록 `t-sql` 원본 데이터베이스에 대 한 스크립트 `sql` 명령 입력으로 제공 합니다.  
  
    에 `convert-sql-statement` mandatorily 변수 값을 변경 하려면 사용자가 명령을 (참조 **VariableValueFileSample.xml**)에 `context` 특성을 사용자가 사용에서 되는 데이터베이스 이름입니다. 사용자도 변경 해야 합니다 `sql` 특성 값을 원본 데이터베이스에 `sql` 명령 변환 하는 데 필요한 권한입니다.  
  
    사용자는 변환할 수 있는 sql 파일을 제공할 수도 있습니다. 설명한 것에이 `convert-sql-statement` 샘플 콘솔 스크립트 파일의 예제 4 명령입니다.  
  
    > [!NOTE]  
    > 변수 값 파일 명령줄 인수를 콘솔 응용 프로그램에 전달 되 고 VariableValueFileSample.xml 지정 된 사용자를 사용 하 여 업데이트 되는 확인 값입니다.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     이 샘플 사용 하면 데이터 마이그레이션 변환할은 종단 간 마이그레이션을 수행할 수 있습니다. 변경 해야 하는 필수 특성 값의 목록 아래에 나열 됩니다.  
  
    **명령 이름**  
  
    `map-schema`  
  
    대상 스키마에 원본 데이터베이스의 스키마 매핑.  
  
    **특성**  
  
    -   `source-schema:` 변환 하는 데 필요한 원본 데이터베이스를 지정 합니다.  
  
    -   `sql-server-schema`: 로 마이그레이션해야 하는 대상 데이터베이스를 지정 합니다.  
  
    **명령 이름**  
  
    `convert-schema`  
  
    -   대상 스키마에 원본에서 스키마 변환을 수행합니다.  
  
    -   사용자가 여러 개체를 평가 / 그 데이터베이스 여러 개 지정할 수 있습니다 `metabase-object` 에 설명 된 대로 노드는 `convert-schema` 샘플 콘솔 스크립트 파일의 예제 4 명령입니다.  
  
    **특성**  
  
    `object-name`: 원본 데이터베이스 지정/이름 변환 하는 데 필요한 개체입니다. 해당 되도록 `object-type` 에 지정 된 개체의 형식에 따라 변경 되는 `object-name`  
  
    **명령 이름**  
  
    `synchronize-target`  
  
    -   대상 데이터베이스를 사용 하 여 대상 개체를 동기화합니다.  
  
    -   사용자가 여러 개체를 평가 / 그 데이터베이스 여러 개 지정할 수 있습니다 `metabase-object` 에 설명 된 대로 노드는 `synchronize-target` 샘플 콘솔 스크립트 파일의 명령의 예제 3입니다.  
  
    **특성**  
  
    `object-name:` Sql server 데이터베이스 지정/개체 만들어야 하는 데 필요한 이름. 해당 되도록 `object-type` 에 지정 된 개체의 형식에 따라 변경 되는 `object-name`  
  
    **명령 이름**  
  
    `migrate-data`  
  
    -   대상에 원본 데이터를 마이그레이션합니다.  
  
    -   사용자가 여러 개체를 평가 / 그 데이터베이스 여러 개 지정할 수 있습니다 `metabase-object` 에 설명 된 대로 노드는 `migrate-data` 샘플 콘솔 스크립트 파일의 명령의 예 2.  
  
    **특성**  
  
    `object-name:` 원본 데이터베이스 지정/마이그레이션해야 하는 데 필요한 이름 테이블입니다. 해당 되도록 `object-type` 에 지정 된 개체의 형식에 따라 변경 되는 `object-name`  
  
## <a name="see-also"></a>관련 항목  
[변수 값 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
[서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
[보고서 생성 &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)  
  
