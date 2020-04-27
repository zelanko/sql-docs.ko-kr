---
title: SQL 실행 태스크 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96d211defa789888a3fd7b513b4dff60fa795cb6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058985"
---
# <a name="execute-sql-task-editor-general-page"></a>SQL 실행 태스크 편집기(일반 페이지)
  **SQL 실행 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 SQL 실행 태스크를 구성하고 해당 태스크에서 실행할 SQL 문을 제공할 수 있습니다.  
  
 이 태스크에 대해 알아보려면 [SQL 실행 태스크](control-flow/execute-sql-task.md), [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) 및 [SQL 실행 태스크의 결과 집합](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)을 참조하세요. Transact-SQL 쿼리 언어에 대한 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)를 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **이름**  
 워크플로의 SQL 실행 태스크에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 SQL 실행 태스크를 설명합니다. 해당 태스크의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **초과가**  
 제한 시간이 초과 되기 전까지 태스크가 실행 되는 최대 시간 (초)을 지정 합니다. 값 0은 시간 제한이 없음을 나타냅니다. 기본값은 0입니다.  
  
> [!NOTE]  
>  저장 프로시저에서 연결 설정 및 트랜잭션 완료 시간으로 **TimeOut**에서 지정한 시간(초)보다 큰 수를 지정하여 대기 기능을 에뮬레이트할 경우 저장 프로시저의 제한 시간이 없습니다. 그러나 쿼리를 실행하는 저장 프로시저는 항상 **TimeOut**에서 지정한 시간의 제한을 받습니다.  
  
 **코드 페이지**  
 변수의 유니코드 값을 변환할 때 사용할 코드 페이지를 지정합니다. 기본값은 로컬 컴퓨터의 코드 페이지입니다.  
  
> [!NOTE]  
>  SQL 실행 태스크에서 ADO 또는 ODBC 연결 관리자를 사용할 때는 **CodePage** 속성을 사용할 수 없습니다. 솔루션에 코드 페이지의 사용이 필요한 경우에는 SQL 실행 태스크에서 OLE DB 또는 ADO.NET 연결 관리자를 사용하십시오.  
  
 **TypeConversionMode**  
 이 속성을 `Allowed`로 설정하면 SQL 실행 태스크는 출력 매개 변수와 쿼리 결과를 결과가 할당되는 변수의 데이터 형식으로 변환합니다. 이는 **단일 행** 결과 집합 유형에 적용됩니다.  
  
 **ResultSet**  
 실행 중인 SQL 문에서 예상하는 결과 유형을 지정합니다. **단일 행**, **전체 결과 집합**, **XML**또는 **없음**중에서 선택합니다.  
  
 **ConnectionType**  
 데이터 원본에 연결할 때 사용할 연결 관리자 유형을 선택합니다. 사용 가능한 연결 형식에는 **OLE DB**, **ODBC**, **ADO**, **ADO.NET** 및 **SQLMOBILE**이 있습니다.  
  
 **관련 항목:** [OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md), [ODBC 연결 관리자](connection-manager/odbc-connection-manager.md), [ADO 연결 관리자](connection-manager/ado-connection-manager.md), [ADO.NET 연결 관리자](connection-manager/ado-net-connection-manager.md), [SQL Server Compact Edition 연결 관리자](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **연결**  
 정의된 연결 관리자 목록에서 연결을 선택합니다. 새 연결을 만들려면 \< **새 연결** ...>을 선택 합니다.  
  
 **SQLSourceType**  
 태스크에서 실행하는 SQL 문의 원본 유형을 선택합니다.  
  
 SQL 실행 태스크에서 사용하는 연결 관리자 유형에 따라 매개 변수가 있는 SQL 문에서 특정 매개 변수 표식을 사용해야 합니다.  
  
 **관련 항목:**[SQL 실행 태스크](control-flow/execute-sql-task.md)  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**직접 입력**|원본을 Transact-SQL 문으로 설정합니다. 이 값을 선택하면 동적 옵션 **SQLStatement**가 표시됩니다.|  
|**파일 연결**|Transact-SQL 문이 포함된 파일을 선택합니다. 이 옵션을 설정하면 동적 옵션 **FileConnection**이 표시됩니다.|  
|**변수**|원본을 Transact-SQL 문을 정의하는 변수로 설정합니다. 이 값을 선택하면 동적 옵션 **SourceVariable**이 표시됩니다.|  
  
 **QueryIsStoredProcedure**  
 실행하도록 지정한 SQL 문이 저장 프로시저인지 여부를 표시합니다. 이 속성은 태스크에서 ADO 연결 관리자를 사용하는 경우에만 읽기/쓰기가 가능합니다. 그렇지 않은 경우 읽기 전용이고 값은 `false`입니다.  
  
 **BypassPrepare**  
 SQL 문의 준비 여부를 나타냅니다.  `true`이면 준비를 건너뛰고 `false`이면 SQL 문을 실행하기 전에 SQL 문을 준비합니다. 이 옵션은 준비를 지원하는 OLE DB 연결에만 사용할 수 있습니다.  
  
 **관련 항목:**  [준비된 실행](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 문이 포함된 파일을 찾습니다. 해당 내용을 **SQLStatement** 속성에 SQL 문으로 복사할 파일을 선택합니다.  
  
 **쿼리 작성**  
 쿼리를 만들 때 사용하는 그래픽 도구인 **쿼리 작성기** 대화 상자를 사용하여 SQL 문을 만듭니다. 이 옵션은 **SQLSourceType** 옵션을 **직접 입력**으로 설정한 경우에만 사용할 수 있습니다.  
  
 **쿼리 구문 분석**  
 SQL 문의 구문 유효성을 검사합니다.  
  
## <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 동적 옵션  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 직접 입력  
 **SQLStatement**  
 실행할 SQL 문을 옵션 상자에 입력 하거나, 찾아보기 단추 (...)를 클릭 하 여 **Sql 쿼리 입력** 대화 상자에 sql 문을 입력 하거나, **쿼리 작성** 을 클릭 하 여 **쿼리 작성기** 대화 상자를 사용 하 여 문을 작성 합니다.  
  
 **관련 항목:** [쿼리 작성기](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 파일 연결  
 **FileConnection**  
 기존 파일 연결 관리자를 선택 하거나 \< **새 연결** ...>을 클릭 하 여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = 변수  
 **SourceVariable**  
 기존 변수를 선택 하거나 \< **새 변수** ...>를 클릭 하 여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 실행 태스크 편집기 &#40;매개 변수 매핑 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [SQL 실행 태스크 편집기 &#40;결과 집합 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
