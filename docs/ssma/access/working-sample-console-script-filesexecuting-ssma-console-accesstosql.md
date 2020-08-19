---
description: SSMA 콘솔 FilesExecuting 샘플 콘솔 스크립트 사용 (AccessToSQL)
title: SSMA 콘솔 FilesExecuting 샘플 콘솔 스크립트 사용 Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ad75b648-d119-4119-98f0-d18f058be68d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 91ccdde50fc0e4f031f376132213881db0a85449
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418529"
---
# <a name="working-with-the-sample-console-script-filesexecuting-the-ssma-console-accesstosql"></a>SSMA 콘솔 FilesExecuting 샘플 콘솔 스크립트 사용 (AccessToSQL)
사용자 참조 및 사용을 위해 제품과 함께 몇 가지 샘플 파일이 제공 되었습니다. 이 섹션에서는 최종 사용자 요구에 맞게 이러한 스크립트를 쉽게 사용자 지정 하는 방법을 설명 합니다.  
  
## <a name="sample-console-script-files"></a>샘플 콘솔 스크립트 파일  
사용자 참조를 위해 다양 한 시나리오를 포함 하는 다음과 같은 샘플 콘솔 스크립트 파일이 제공 됩니다.  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   이 샘플은 원본 및 대상 데이터베이스에 사용할 수 있는 다양 한 연결 모드를 제공 하며, 사용자는 요구 사항에 따라 모드를 선택할 수 있습니다. 이 샘플에는 서버 정의가 포함 되어 있습니다.  
  
    -   사용자는 필요한 원본 및 대상 서버 정의로 값을 변경 하 여 필요한 데이터베이스에 연결할 수 있습니다. 이 예제에서는 모든 값이 **VariableValueFileSample.xml**에서 사용할 수 있는 변수 값으로 제공 되었습니다. 다른 모든 연결 매개 변수는 사용자의 작업 중인 서버 연결 파일에서 제거할 수 있습니다.  
  
    -   원본 및 대상 서버에 연결 하는 방법에 대 한 자세한 내용은 [AccessToSQL&#41;&#40;서버 연결 파일 만들기 ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) 를 참조 하세요.  
  
-   **VariableValueFileSample.xml:** 샘플 콘솔에서 사용 된 모든 변수가 `ServersConnectionFileSample.xml` 이 파일에서 정렬 되었습니다. 샘플 콘솔 스크립트를 실행 하려면 사용자가 샘플 변수 값을 사용자 정의 된 값으로 바꾸고이 파일을 스크립트 파일과 함께 추가 명령줄 인수로 전달 하기만 하면 됩니다.  
  
    변수 값 파일에 대 한 자세한 내용은 [AccessToSQL&#41;&#40;변수 값 파일 만들기 ](../../ssma/access/creating-variable-value-files-accesstosql.md)를 참조 하세요.  
  
-   **AssessmentReportGenerationSample.xml:** 이 샘플을 사용 하면 사용자가 데이터 변환 및 마이그레이션을 시작 하기 전에 분석을 위해 사용자가 사용할 수 있는 xml 평가 보고서를 생성할 수 있습니다.  
  
    명령에서 사용자가 `generate-assessment-report` ** ** `object-name` 사용 중인 데이터베이스 이름에 대 한 변수 값 (VariableValueFileSample.xml참조)을 mandatorily 변경 해야 합니다. 지정 된 개체의 종류에 따라 `object-type` 값도 변경 해야 합니다.  
  
    사용자가 여러 개체/데이터베이스를 평가 해야 하는 경우 `metabase-object` `generate-assessment-report` 샘플 콘솔 스크립트 파일의 명령 예제 4에 나와 있는 것 처럼 여러 노드를 지정할 수 있습니다.  
  
    보고서를 생성 하는 방법에 대 한 자세한 내용은 [보고서 생성 &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)을 참조 하세요.  
  
    > [!NOTE]  
    > -   변수 값 파일 명령줄 인수가 콘솔 응용 프로그램에 전달 되 고 VariableValueFileSample.xml 사용자 지정 값으로 업데이트 되었는지 확인 합니다.  
    > -   서버 연결 파일 명령줄 인수가 콘솔 응용 프로그램에 전달 되 고 ServersConnectionFileSample.xml 올바른 서버 매개 변수 값으로 업데이트 되었는지 확인 합니다.  
  
-   **ConversionAndDataMigrationSample.xml:** 이 샘플은 사용자가 데이터 마이그레이션에 대 한 변환에서 종단 간 마이그레이션을 수행할 수 있도록 합니다. 변경 해야 하는 필수 특성 값 목록은 아래에 나열 되어 있습니다.  
  
    |명령 이름|설명|attribute|  
    |----------------|---------------|-------------|  
    |`map-schema`|원본 데이터베이스와 대상 스키마의 스키마 매핑|`source-schema:` 변환 해야 하는 원본 데이터베이스를 지정 합니다.<br /><br />`sql-server-schema`: 마이그레이션할 대상 데이터베이스를 지정 합니다.|  
    |`convert-schema`|원본에서 대상 스키마로의 스키마 변환을 수행 합니다.<br /><br />사용자가 여러 개체/데이터베이스를 평가 해야 하는 경우 `metabase-object` `convert-schema` 샘플 콘솔 스크립트 파일의 명령 예제 4에 나와 있는 것 처럼 여러 노드를 지정할 수 있습니다.|`object-name`: 변환 해야 하는 원본 데이터베이스/개체 이름을 지정 합니다. 에 `object-type` 지정 된 개체의 형식에 따라 해당이 변경 되었는지 확인 합니다. `object-name`|  
    |`synchronize-target`|대상 개체를 대상 데이터베이스와 동기화 합니다.<br /><br />사용자가 여러 개체/데이터베이스를 평가 해야 하는 경우 `metabase-object` `synchronize-target` 샘플 콘솔 스크립트 파일의 명령 예제 3에 나와 있는 것 처럼 여러 노드를 지정할 수 있습니다.|`object-name:` 만들어야 하는 sql server 데이터베이스/개체 이름을 지정 합니다. 에 `object-type` 지정 된 개체의 형식에 따라 해당이 변경 되었는지 확인 합니다. `object-name`|  
    |`migrate-data`|원본 데이터를 대상으로 마이그레이션합니다.<br /><br />사용자가 여러 개체/데이터베이스를 평가 해야 하는 경우 `metabase-object` `migrate-data` 샘플 콘솔 스크립트 파일의 명령 예제 2에 설명 된 대로 여러 노드를 지정할 수 있습니다.|`object-name:` 마이그레이션해야 하는 원본 데이터베이스/테이블 이름을 지정 합니다. 에 `object-type` 지정 된 개체의 형식에 따라 해당이 변경 되었는지 확인 합니다. `object-name`|  
  
## <a name="see-also"></a>참고 항목  
[AccessToSQL&#41;&#40;변수 값 파일 만들기 ](../../ssma/access/creating-variable-value-files-accesstosql.md)  
[AccessToSQL&#41;&#40;서버 연결 파일 만들기 ](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
[AccessToSQL&#41;&#40;보고서 생성 ](../../ssma/access/generating-reports-accesstosql.md)  
  
