---
title: SQL 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f334633fa164a22f8e23175fd3ba6b25c4f6423
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917931"
---
# <a name="execute-sql-task"></a>SQL 실행 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SQL 실행 태스크는 패키지에서 SQL 문이나 저장 프로시저를 실행합니다. 이 태스크는 단일 SQL 문 또는 순서대로 실행되는 여러 SQL 문을 포함할 수 있습니다. SQL 실행 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   데이터를 삽입하기 위해 테이블 또는 뷰를 자릅니다.  
  
-   테이블 및 뷰와 같은 데이터베이스 개체를 만들고 변경 및 삭제합니다.  
  
-   팩트 및 차원 테이블에 데이터를 로드하기 전에 해당 테이블을 다시 만듭니다.  
  
-   저장 프로시저를 실행합니다. SQL 문이 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
-   쿼리에서 반환된 행 집합을 변수에 저장합니다.  
  
 SQL 실행 태스크를 Foreach 루프 및 For 루프 컨테이너와 함께 사용하여 여러 개의 SQL 문을 실행할 수 있습니다. 두 컨테이너는 패키지의 반복 제어 흐름을 구현하며 SQL 실행 태스크를 반복해서 실행할 수 있습니다. 예를 들어 Foreach 루프 컨테이너를 사용하면 패키지가 폴더에 있는 파일을 열거하고 SQL 실행 태스크를 반복 실행하여 각 파일에 저장된 SQL 문을 실행할 수 있습니다.  
  
## <a name="connect-to-a-data-source"></a>데이터 원본에 연결  
 SQL 실행 태스크는 여러 유형의 연결 관리자를 사용하여 SQL 문이나 저장 프로시저가 실행될 데이터 원본에 연결할 수 있습니다. 다음 표에 나열된 연결 형식을 사용할 수 있습니다.  
  
|연결 형식|ODBC 대상 편집기|  
|---------------------|------------------------|  
|EXCEL|[Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>SQL 문 만들기  
 이 태스크에 사용되는 SQL 문의 원본은 문이 포함된 작업 속성, 하나 이상의 문이 포함된 파일에 대한 연결 또는 문이 포함된 변수 이름일 수 있습니다. SQL 문은 원본 DBMS(데이터베이스 관리 시스템) 언어로 기록되어야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 쿼리](../../integration-services/integration-services-ssis-queries.md)를 참조하세요.  
  
 SQL 문이 파일에 저장되어 있을 경우 SQL 실행 태스크는 파일 연결 관리자를 사용하여 해당 파일에 연결합니다. 자세한 내용은 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서는 **SQL 실행 태스크 편집기** 대화 상자를 사용하여 SQL 문을 입력하거나 SQL 쿼리 작성용 그래픽 사용자 인터페이스인 **쿼리 작성기**를 사용할 수 있습니다. 
  
> [!NOTE]  
>  SQL 실행 태스크 외부에서 작성된 SQL 문은 유효하더라도 SQL 실행 태스크에서 성공적으로 구문 분석되지 않을 수도 있습니다.  
  
> [!NOTE]  
>  SQL 실행 태스크는 **RecognizeAll** ParseMode 열거형 값을 사용합니다. 자세한 내용은 [ManagedBatchParser 네임스페이스](https://go.microsoft.com/fwlink/?LinkId=223617)를 참조하십시오.  
  
## <a name="send-multiple-statements-in-a-batch"></a>여러 개의 문을 일괄 처리로 전송  
 SQL 실행 태스크에 여러 개의 문이 포함된 경우 문을 그룹화하여 일괄 처리로 실행할 수 있습니다. 일괄 처리의 마지막을 알리려면 GO 명령을 사용합니다. 두 GO 명령 사이의 모든 SQL 문은 일괄 처리로 실행되도록 OLE DB Provider에 전송됩니다. SQL 명령은 GO 명령으로 구분된 여러 개의 일괄 처리를 포함할 수 있습니다.  
  
 일괄 처리로 그룹화할 수 있는 SQL 문의 종류에는 제한이 있습니다. 자세한 내용은 [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)을 참조하세요.  
  
 SQL 실행 태스크에서 SQL 문의 일괄 처리를 실행하는 경우 해당 일괄 처리에 다음 규칙이 적용됩니다.  
  
-   일괄 처리의 첫 번째 문 하나만 결과 집합을 반환할 수 있습니다.  
  
-   결과 집합에 결과 바인딩을 사용하는 경우 쿼리에서 동일한 수의 열이 반환되어야 합니다. 쿼리에서 반환된 열 수가 서로 다르면 태스크가 실패합니다. 그러나 태스크 실패해도 해당 태스크에서 실행하는 DELETE 또는 INSERT와 같은 쿼리는 성공할 수 있습니다.  
  
-   결과 바인딩에 열 이름을 사용하는 경우 태스크에 사용된 결과 집합 이름과 동일한 이름이 포함된 열이 쿼리에서 반환되어야 합니다. 해당 열이 없으면 태스크가 실패합니다.  
  
-   태스크에 매개 변수 바인딩이 사용되는 경우 일괄 처리의 모든 쿼리에 동일한 수와 유형의 매개 변수를 사용해야 합니다.  
  
## <a name="run-parameterized-sql-commands"></a>매개 변수가 있는 SQL 명령 실행  
 SQL 문과 저장 프로시저는 일반적으로 입력 매개 변수, 출력 매개 변수 및 반환 코드를 사용합니다. SQL 실행 태스크는 **Input**, **Output**및 **ReturnValue** 매개 변수 유형을 지원합니다. 입력 매개 변수에는 **Input** 유형, 출력 매개 변수에는 **Output** 유형, 반환 코드에는 **ReturnValue** 유형을 사용합니다.  
  
> [!NOTE]  
>  데이터 공급자가 지원하는 경우에만 SQL 실행 태스크에 매개 변수를 사용할 수 있습니다.  
  
## <a name="specify-a-result-set-type"></a>결과 집합 유형 지정  
 SQL 명령 유형에 따라 SQL 실행 태스크에서 결과 집합이 반환될 수도 있고 반환되지 않을 수도 있습니다. 예를 들어 SELECT 문은 일반적으로 결과 집합을 반환하지만 INSERT 문은 결과 집합을 반환하지 않습니다. SELECT 문의 결과 집합은 행을 포함하지 않을 수도 있고, 하나 이상의 행을 포함할 수 있습니다. 저장 프로시저도 반환 코드라고 하는 정수 값을 반환하여 프로시저의 실행 상태를 표시할 수 있습니다. 이 경우에는 결과 집합이 단일 행으로 구성됩니다.  
  
## <a name="configure-the-execute-sql-task"></a>SQL 실행 태스크 구성  
 다음과 같은 방법으로 SQL 실행 태스크를 구성할 수 있습니다.  
  
-   데이터베이스에 연결할 때 사용할 연결 관리자 유형을 지정합니다.  
  
-   SQL 문에서 반환되는 결과 집합 유형을 지정합니다.  
  
-   SQL 문의 제한 시간을 지정합니다.  
  
-   SQL 문의 원본을 지정합니다.  
  
-   태스크에서 SQL 문의 준비 단계를 건너뛸지를 나타냅니다.  
  
-   ADO 연결 형식을 사용하는 경우 SQL 문이 저장 프로시저인지 여부를 나타내야 합니다. 다른 연결 형식에서 이 속성은 읽기 전용이며 항상 **false**값을 갖습니다.  
  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  

## <a name="general-page---execute-sql-task-editor"></a>일반 페이지 - SQL 실행 태스크 편집기
 **SQL 실행 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 SQL 실행 태스크를 구성하고 해당 태스크에서 실행할 SQL 문을 제공할 수 있습니다.  

Transact-SQL 쿼리 언어에 대한 자세한 내용은 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](../../t-sql/transact-sql-reference-database-engine.md)를 참조하세요.  
  
### <a name="static-options"></a>정적 옵션  
 **이름**  
 워크플로의 SQL 실행 태스크에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 SQL 실행 태스크를 설명합니다. 해당 태스크의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **TimeOut**  
 태스크 제한 시간이 초과될 때까지 걸리는 최대 시간(초)을 지정합니다. 값 0은 제한 시간이 없음을 의미합니다. 기본값은 0입니다.  
  
> [!NOTE]  
>  저장 프로시저에서 연결 설정 및 트랜잭션 완료 시간으로 **TimeOut**에서 지정한 시간(초)보다 큰 수를 지정하여 대기 기능을 에뮬레이트할 경우 저장 프로시저의 제한 시간이 없습니다. 그러나 쿼리를 실행하는 저장 프로시저는 항상 **TimeOut**에서 지정한 시간의 제한을 받습니다.  
  
 **CodePage**  
 변수의 유니코드 값을 변환할 때 사용할 코드 페이지를 지정합니다. 기본값은 로컬 컴퓨터의 코드 페이지입니다.  
  
> [!NOTE]  
>  SQL 실행 태스크에서 ADO 또는 ODBC 연결 관리자를 사용할 때는 **CodePage** 속성을 사용할 수 없습니다. 솔루션에 코드 페이지의 사용이 필요한 경우에는 SQL 실행 태스크에서 OLE DB 또는 ADO.NET 연결 관리자를 사용하십시오.  
  
 **TypeConversionMode**  
 이 속성을 **Allowed**로 설정하면 SQL 실행 태스크는 출력 매개 변수와 쿼리 결과를 결과가 할당되는 변수의 데이터 형식으로 변환합니다. 이는 **단일 행** 결과 집합 유형에 적용됩니다.  
  
 **ResultSet**  
 실행 중인 SQL 문에서 예상하는 결과 유형을 지정합니다. **단일 행**, **전체 결과 집합**, **XML**또는 **없음**중에서 선택합니다.  
  
 **ConnectionType**  
 데이터 원본에 연결할 때 사용할 연결 관리자 유형을 선택합니다. 사용 가능한 연결 형식에는 **OLE DB**, **ODBC**, **ADO**, **ADO.NET** 및 **SQLMOBILE**이 있습니다.  
  
 **관련 항목:** [OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md), [ODBC 연결 관리자](../../integration-services/connection-manager/odbc-connection-manager.md), [ADO 연결 관리자](../../integration-services/connection-manager/ado-connection-manager.md), [ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md), [SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **연결**  
 정의된 연결 관리자 목록에서 연결을 선택합니다. 새 연결을 설정하려면 \<**New connection...**>을 선택합니다.  
  
 **SQLSourceType**  
 태스크에서 실행하는 SQL 문의 원본 유형을 선택합니다.  
  
 SQL 실행 태스크에서 사용하는 연결 관리자 유형에 따라 매개 변수가 있는 SQL 문에서 특정 매개 변수 표식을 사용해야 합니다.    
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 Transact-SQL 문으로 설정합니다. 이 값을 선택하면 동적 옵션 **SQLStatement**가 표시됩니다.|  
|**파일 연결**|Transact-SQL 문이 포함된 파일을 선택합니다. 이 옵션을 설정하면 동적 옵션 **FileConnection**이 표시됩니다.|  
|**변수**|원본을 Transact-SQL 문을 정의하는 변수로 설정합니다. 이 값을 선택하면 동적 옵션 **SourceVariable**이 표시됩니다.|  
  
 **QueryIsStoredProcedure**  
 실행하도록 지정한 SQL 문이 저장 프로시저인지 여부를 표시합니다. 이 속성은 태스크에서 ADO 연결 관리자를 사용하는 경우에만 읽기/쓰기가 가능합니다. 그렇지 않은 경우 읽기 전용이고 값은 **false**입니다.  
  
 **BypassPrepare**  
 SQL 문의 준비 여부를 나타냅니다.  **true** 이면 준비를 건너뛰고 **false** 이면 SQL 문을 실행하기 전에 SQL 문을 준비합니다. 이 옵션은 준비를 지원하는 OLE DB 연결에만 사용할 수 있습니다.  
  
 **관련 항목:**  [준비된 실행](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 문이 포함된 파일을 찾습니다. 해당 내용을 **SQLStatement** 속성에 SQL 문으로 복사할 파일을 선택합니다.  
  
 **쿼리 작성**  
 쿼리를 만들 때 사용하는 그래픽 도구인 **쿼리 작성기** 대화 상자를 사용하여 SQL 문을 만듭니다. 이 옵션은 **SQLSourceType** 옵션을 **직접 입력**으로 설정한 경우에만 사용할 수 있습니다.  
  
 **쿼리 구문 분석**  
 SQL 문의 구문 유효성을 검사합니다.  
  
### <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 동적 옵션  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 직접 입력  
 **SQLStatement**  
 실행할 SQL 문을 옵션 상자에 입력하거나, 찾아보기 단추(...)를 클릭하여 **SQL 쿼리 입력** 대화 상자에 SQL 문을 입력하거나, **쿼리 작성**을 클릭하고 **쿼리 작성기** 대화 상자를 사용하여 SQL 문을 작성합니다.  
  
 **관련 항목:** [쿼리 작성기](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 파일 연결  
 **FileConnection**  
 기존 파일 연결 관리자를 선택하거나 \<**New connection...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = 변수  
 **SourceVariable**  
 기존 변수를 선택하거나 \<**New variable...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>매개 변수 매핑 페이지 - SQL 실행 태스크 편집기
**SQL 실행 태스크 편집기** 대화 상자의 **매개 변수 매핑** 페이지를 사용하여 변수를 SQL 문의 매개 변수에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **변수 이름**  
 **추가**를 클릭하여 매개 변수 매핑을 추가했으면 **변수 추가** 대화 상자를 사용하여 목록에서 시스템 또는 사용자 정의 변수를 선택하거나 \<**New variable...**>를 클릭하여 새 변수를 추가합니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)  
  
 **Direction**  
 매개 변수의 방향을 선택합니다. 각 변수를 입력 매개 변수, 출력 매개 변수 또는 반환 코드에 매핑합니다.  
  
 **데이터 형식**  
 매개 변수의 데이터 형식을 선택합니다. 사용 가능한 데이터 형식의 목록은 태스크에서 사용하는 연결 관리자에서 선택한 공급자에만 적용됩니다.  
  
 **매개 변수 이름**  
 매개 변수 이름을 입력합니다.  
  
 태스크에서 사용하는 연결 관리자 유형에 따라 숫자 또는 매개 변수 이름을 사용해야 합니다. 일부 연결 관리자 유형의 경우 매개 변수 이름의 첫 문자가 \@ 기호여야 하거나, 이름이 \@Param1과 같은 특정 이름이어야 하거나, 열 이름을 매개 변수 이름으로 지정해야 합니다.  
  
 **매개 변수 크기**  
 문자열 및 이진 필드와 같은 가변 길이를 가지는 매개 변수의 크기를 제공합니다.  
  
 이 설정을 사용하면 공급자에서 가변 길이 매개 변수 값에 대해 충분한 공간을 할당합니다.  
  
 **추가**  
 매개 변수 매핑을 추가하려면 클릭합니다.  
  
 **제거**  
 목록에서 매개 변수 매핑을 선택한 다음 **제거**를 클릭합니다.  
 
## <a name="result-set-page---execute-sql-task-editor"></a>결과 집합 페이지 - SQL 실행 태스크 편집기
**SQL 실행 태스크 편집기** 대화 상자의 **결과 집합** 페이지를 사용하여 SQL 문의 결과를 새 변수 또는 기존 변수로 매핑할 수 있습니다. 일반 페이지의 **ResultSet** 을 **없음**으로 설정한 경우에는 이 대화 상자의 옵션을 사용할 수 없습니다.  
  
### <a name="options"></a>옵션  
 **결과 이름**  
 **추가**를 클릭하여 결과 집합 매핑 집합을 추가한 다음 결과를 설명하는 이름을 제공합니다. 결과 집합 유형에 따라 특정 결과 이름을 사용해야 합니다.  
  
 결과 집합 유형이 **단일 행**이면 쿼리에서 반환한 열 이름이나 쿼리에서 반환한 열의 열 목록에서 열 위치를 나타내는 숫자 중 하나를 사용할 수 있습니다.  
  
 결과 집합 유형이 **전체 결과 집합** 이나 **XML**이면 결과 집합 이름으로 0을 사용해야 합니다.  
 
  
 **변수 이름**  
 변수를 선택하여 결과 집합을 변수로 매핑하거나 \<**New variable...**>를 클릭하여 **변수 추가** 대화 상자를 사용하여 새 변수를 추가합니다.  
  
 **추가**  
 결과 집합 매핑을 추가하려면 클릭합니다.  
  
 **제거**  
 목록에서 결과 집합 매핑을 선택한 다음 **제거**를 클릭합니다.  
 
## <a name="parameters-in-the-execute-sql-task"></a>SQL 실행 태스크의 매개 변수
SQL 문과 저장 프로시저에서는 일반적으로 **input** 매개 변수, **output** 매개 변수 및 반환 코드를 사용합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 SQL 실행 태스크는 **Input**, **Output**및 **ReturnValue** 매개 변수 유형을 지원합니다. 입력 매개 변수에는 **Input** 유형, 출력 매개 변수에는 **Output** 유형, 반환 코드에는 **ReturnValue** 유형을 사용합니다.  
  
> [!NOTE]  
>  데이터 공급자가 지원하는 경우에만 SQL 실행 태스크에 매개 변수를 사용할 수 있습니다.  
  
 쿼리와 저장 프로시저를 포함하여 SQL 명령의 매개 변수는 SQL 실행 태스크의 범위, 부모 컨테이너 또는 패키지 범위 내에서 생성된 사용자 정의 변수에 매핑됩니다. 변수 값은 디자인 타임에 설정하거나 런타임에 동적으로 채울 수 있습니다. 매개 변수를 시스템 변수에 매핑할 수도 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [시스템 변수](../../integration-services/system-variables.md)를 참조하세요.  
  
 그러나 SQL 실행 태스크에서 매개 변수 및 반환 코드를 사용하려면 태스크에서 지원되는 매개 변수 유형 및 이러한 매개 변수가 매핑되는 방식을 이해하는 것만으로는 충분하지 않습니다. SQL 실행 태스크에서 매개 변수 및 반환 코드를 제대로 사용하려면 추가적인 사용 요구 사항과 지침을 따라야 합니다. 이 항목의 나머지 부분에서는 이러한 사용 요구 사항과 지침을 설명합니다.  
  
-   [매개 변수 이름 및 표식 사용](#Parameter_names_and_markers)  
  
-   [날짜 및 시간 데이터 형식의 매개 변수 사용](#Date_and_time_data_types)  
  
-   [WHERE 절에 매개 변수 사용](#WHERE_clauses)  
  
-   [저장 프로시저에 매개 변수 사용](#Stored_procedures)  
  
-   [반환 코드 값 가져오기](#Return_codes)    
  
###  <a name="parameter-names-and-markers"></a><a name="Parameter_names_and_markers"></a> 매개 변수 이름 및 표식  
 SQL 실행 태스크가 사용하는 연결 형식에 따라 SQL 명령 구문이 사용하는 매개 변수 표식이 달라집니다. 예를 들어 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자 유형을 사용하려면 SQL 명령에서 **\@varParameter** 형식의 매개 변수 표식을 사용해야 하지만 OLE DB 연결 형식에는 물음표(?) 매개 변수 표식을 사용해야 합니다.  
  
 변수와 매개 변수 간 매핑에 매개 변수 이름으로 사용할 수 있는 이름도 연결 관리자 유형에 따라 달라집니다. 예를 들어 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자 유형에는 \@ 접두사가 있는 사용자 정의 이름을 사용하지만 OLE DB 연결 관리자 유형에는 0부터 시작하는 서수의 숫자 값을 매개 변수 이름으로 사용해야 합니다.  
  
 다음 표에서는 SQL 실행 태스크가 사용할 수 있는 연결 관리자 유형에 대한 SQL 명령 요구 사항을 요약합니다.  
  
|연결 형식|매개 변수 표식|매개 변수 이름|SQL 명령 예|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|\@\<parameter name>|\@\<parameter name>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 및 OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 및 ADO 연결 관리자의 매개 변수 사용  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 및 ADO 연결 관리자에는 매개 변수를 사용하는 SQL 명령에 대한 특별한 요구 사항이 있습니다.  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하려면 SQL 명령에 매개 변수 이름을 매개 변수 표식으로 사용해야 합니다. 즉, 변수를 매개 변수에 직접 매핑할 수 있습니다. 예를 들어 `@varName` 변수는 `@parName` 이라는 매개 변수에 매핑되고 `@parName`매개 변수에 값을 제공합니다.  
  
-   ADO 연결 관리자를 사용하려면 SQL 명령에 물음표(?)를 매개 변수 표식으로 사용해야 합니다. 그러나 정수 값을 제외한 모든 사용자 정의 이름을 매개 변수 이름으로 사용할 수 있습니다.  
  
 매개 변수에 값을 제공하기 위해 변수는 매개 변수 이름에 매핑됩니다. 그런 다음 SQL 실행 태스크에서 매개 변수 목록에 있는 매개 변수 이름의 서수 값을 사용하여 변수의 값을 매개 변수에 로드합니다.  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>EXCEL, ODBC 및 OLE DB 연결 관리자의 매개 변수 사용  
 EXCEL, ODBC 및 OLE DB 연결 관리자를 사용하려면 SQL 명령에 물음표(?)를 매개 변수 표식으로 사용하고 0 또는 1부터 시작하는 숫자 값을 매개 변수 이름으로 사용해야 합니다. SQL 실행 태스크에서 ODBC 연결 관리자를 사용하면 쿼리의 첫 번째 매개 변수에 매핑되는 매개 변수 이름이 1이고, 그렇지 않으면 이 매개 변수 이름이 0입니다. 후속 매개 변수의 경우에도 매개 변수 이름의 숫자 값이 SQL 명령에서 매개 변수 이름이 매핑되는 매개 변수를 나타냅니다. 예를 들어 이름이 3인 매개 변수는 세 번째 매개 변수에 매핑되며 SQL 명령에서 세 번째 물음표(?)로 표현됩니다.  
  
 매개 변수에 값을 제공하기 위해 변수가 매개 변수 이름에 매핑되고 SQL 실행 태스크에서 매개 변수 이름의 서수 값을 사용하여 변수 값을 매개 변수에 로드합니다.  
  
 연결 관리자에서 사용하는 공급자에 따라 일부 OLE DB 데이터 형식이 지원되지 않을 수 있습니다. 예를 들어 Excel 드라이버는 제한된 데이터 형식 집합만 인식합니다. Excel 드라이버를 사용하는 Jet 공급자의 동작에 대한 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md)을 참조하십시오.  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>OLE DB 연결 관리자의 매개 변수 사용  
 SQL 실행 태스크에서 OLE DB 연결 관리자를 사용할 때는 태스크의 BypassPrepare 속성을 사용할 수 있습니다. SQL 실행 태스크에서 매개 변수가 있는 SQL 문을 사용하는 경우 이 속성을 **true** 로 설정해야 합니다.  
  
 OLE DB 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 OLE DB Provider를 통해 매개 변수 정보를 파생할 수 없으므로 매개 변수가 있는 하위 쿼리를 사용할 수 없습니다. 그러나 식을 사용하여 매개 변수 값을 쿼리 문자열로 연결하고 태스크의 SqlStatementSource 속성을 설정할 수 있습니다.  
  
###  <a name="use-parameters-with-date-and-time-data-types"></a><a name="Date_and_time_data_types"></a> 날짜 및 시간 데이터 형식의 매개 변수 사용  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 및 ADO 연결 관리자의 날짜 및 시간 매개 변수 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식인 **time** 및 **datetimeoffset**데이터를 읽을 때는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 또는 ADO 연결 관리자를 사용하는 SQL 실행 태스크에 다음과 같은 요구 사항이 추가로 적용됩니다.  
  
-   **time** 데이터의 경우 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하려면 매개 변수 유형이 **Input** 또는 **Output**이고 데이터 형식이 **string**인 매개 변수에 이 데이터를 저장해야 합니다.  
  
-   **datetimeoffset** 데이터의 경우 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하려면 다음 매개 변수 중 하나에 이 데이터를 저장해야 합니다.  
  
    -   매개 변수 유형이 **Input** 이고 데이터 형식이 **string**인 매개 변수  
  
    -   매개 변수 유형이 **Output** 또는 **ReturnValue**이고 데이터 형식이 **datetimeoffset**, **string**또는 **datetime2**인 매개 변수. 데이터 형식이 **string** 또는 **datetime2**인 매개 변수를 선택하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 데이터를 string이나 datetime2로 변환합니다.  
  
-   ADO 연결 관리자를 사용하려면 매개 변수 유형이 **time** 또는 **datetimeoffset** 이고 데이터 형식이 **Input** 인 매개 변수에 **Output**또는 **adVarWchar**데이터를 저장해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 및 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>OLE DB 연결 관리자의 날짜 및 시간 매개 변수 사용  
 OLE DB 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime**, **datetime2** 및 **datetimeoffset** 형식의 데이터를 스토리지할 때 특수한 요구 사항이 적용됩니다. 이러한 데이터를 다음과 같은 매개 변수 유형 중 하나에 저장해야 합니다.  
  
-   NVARCHAR 데이터 형식의 입력 매개 변수  
  
-   다음 표에 나열된 적절한 데이터 형식의 출력 매개 변수  
  
    |**Output** 매개 변수 유형|날짜 데이터 형식|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 적절한 입력 또는 출력 매개 변수에 데이터가 저장되지 않으면 패키지가 실패합니다.  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>ODBC 연결 관리자의 날짜 및 시간 매개 변수 사용  
 ODBC 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime**, **datetime2** 또는 **datetimeoffset** 중 한 형식의 데이터를 스토리지할 때 특수한 요구 사항이 적용됩니다. 이러한 데이터를 다음과 같은 매개 변수 유형 중 하나에 저장해야 합니다.  
  
-   SQL_WVARCHAR 데이터 형식의 **input** 매개 변수  
  
-   다음 표에 나와 있는 적절한 데이터 형식의 **output** 매개 변수  
  
    |**Output** 매개 변수 유형|날짜 데이터 형식|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> 또는<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 적절한 입력 또는 출력 매개 변수에 데이터가 저장되지 않으면 패키지가 실패합니다.  
  
###  <a name="use-parameters-in-where-clauses"></a><a name="WHERE_clauses"></a> WHERE 절에 매개 변수 사용  
 원본 테이블의 각 행이 SQL 명령에 적합하도록 만들기 위해 만족시켜야 할 조건을 정의하는 필터를 지정하기 위해 SELECT, INSERT, UPDATE 및 DELETE 명령에 WHERE 절을 포함하는 경우가 많습니다. 매개 변수는 WHERE 절에 필터 값을 제공합니다.  
  
 매개 변수 표식을 사용하여 매개 변수 값을 동적으로 제공할 수 있습니다. SQL 문에 사용할 수 있는 매개 변수 표식 및 매개 변수 이름에 대한 규칙은 SQL 실행이 사용하는 연결 관리자 유형에 따라 달라집니다.  
  
 다음 표에서는 연결 관리자 유형별 SELECT 명령의 예를 나열합니다. INSERT, UPDATE 및 DELETE 문도 이와 비슷합니다. 이 예에서는 SELECT를 사용하여 **의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 **ProductID** 가 두 매개 변수로 지정된 값보다 크고 작은 제품을 반환합니다.  
  
|연결 형식|SELECT 구문|  
|---------------------|-------------------|  
|EXCEL, ODBC 및 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 이 예에서는 다음과 같은 이름의 매개 변수가 필요합니다.  
  
-   EXCEL 및 OLED DB 연결 관리자는 매개 변수 이름으로 0과 1을 사용하고 ODBC 연결 형식은 1과 2를 사용합니다.  
  
-   ADO 연결 형식에서는 Param1 및 Param2와 같은 임의의 두 매개 변수 이름을 사용할 수 있지만 이러한 매개 변수는 매개 변수 목록에서의 서수 위치에 따라 매핑되어야 합니다.  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 형식에서는 매개 변수 이름 \@parmMinProductID 및 \@parmMaxProductID를 사용합니다.  
  
###  <a name="use-parameters-with-stored-procedures"></a><a name="Stored_procedures"></a> 저장 프로시저에 매개 변수 사용  
 저장 프로시저를 실행하는 SQL 명령도 매개 변수 매핑을 사용할 수 있습니다. 매개 변수 표식 및 매개 변수 이름 사용 방법에 대한 규칙은 매개 변수가 있는 쿼리에 대한 규칙에서와 마찬가지로 SQL 실행이 사용하는 연결 관리자 유형에 따라 달라집니다.  
  
 다음 표에서는 연결 관리자 유형별 EXEC 명령의 예를 나열합니다. 이 예에서는 **의** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]저장 프로시저를 실행합니다. 이 저장 프로시저는 `@StartProductID` 및 `@CheckDate` **input** 매개 변수를 사용합니다.  
  
|연결 형식|EXEC 구문|  
|---------------------|-----------------|  
|EXCEL 및 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> ODBC 호출 구문에 대한 자세한 내용은 MSDN Library의 ODBC 프로그래머 참조에서 [프로시저 매개 변수](https://go.microsoft.com/fwlink/?LinkId=89462)항목을 참조하십시오.|  
|ADO|IsQueryStoredProcedure가 **False**로 설정된 경우 `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> IsQueryStoredProcedure가 **True**로 설정된 경우 `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|IsQueryStoredProcedure가 **False**로 설정된 경우 `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> IsQueryStoredProcedure가 **True**로 설정된 경우 `uspGetBillOfMaterials`|  
  
 출력 매개 변수를 사용하려면 구문에서 각 매개 변수 표식 다음에 OUTPUT 키워드가 와야 합니다. 올바른 출력 매개 변수 구문의 예로 `EXEC myStoredProcedure ? OUTPUT`을 들 수 있습니다.  
  
 Transact-SQL 저장 프로시저에서 입력 및 출력 매개 변수 사용에 대한 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)를 참조하세요.  
 
### <a name="map-query-parameters-to-variables"></a>변수에 매개 변수 매핑
이 섹션에서는 SQL 실행 태스크에서 매개 변수가 있는 SQL 문을 사용하는 방법과 SQL 문의 변수와 매개 변수 간 매핑을 만드는 방법에 대해 설명합니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 작업하려는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  패키지에 아직 SQL 실행 태스크가 포함되어 있지 않으면 패키지의 제어 흐름에 해당 작업을 추가합니다. 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)를 참조하세요.  
  
5.  SQL 실행 태스크를 두 번 클릭합니다.  
  
6.  다음 방법 중 하나로 매개 변수가 있는 SQL 명령을 제공합니다.  
  
    -   직접 입력을 사용하여 SQLStatement 속성에 SQL 명령을 입력합니다.  
  
    -   직접 입력을 사용하여 **쿼리 작성**을 클릭한 후 쿼리 작성기에서 제공하는 그래픽 도구를 사용하여 SQL 명령을 만듭니다.  
  
    -   파일 연결을 사용한 후 SQL 명령이 포함된 파일을 참조합니다.  
  
    -   변수를 사용한 후 SQL 명령이 포함된 변수를 참조합니다.  
  
     매개 변수가 있는 SQL 문에서 사용하는 매개 변수 표식은 SQL 실행 태스크에서 사용하는 연결 형식에 따라 다릅니다.  
  
    |연결 형식|매개 변수 표식|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 및 SQLMOBILE|\@\<parameter name>|  
    |ODBC|?|  
    |EXCEL 및 OLE DB|?|  
  
     다음 표에서는 연결 관리자 유형별 SELECT 명령의 예를 나열합니다. 매개 변수는 WHERE 절에 필터 값을 제공합니다. 이 예에서는 SELECT를 사용하여 **의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 **ProductID** 가 두 매개 변수로 지정된 값보다 크고 작은 제품을 반환합니다.  
  
    |연결 형식|SELECT 구문|  
    |---------------------|-------------------|  
    |EXCEL, ODBC 및 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  **매개 변수 매핑**을 클릭합니다.  
  
8.  매개 변수 매핑을 추가하려면 **추가**를 클릭합니다.  
  
9. **매개 변수 이름** 상자에 이름을 제공합니다.  
  
     사용하는 매개 변수 이름은 SQL 실행 태스크에 사용하는 연결 형식에 따라 다릅니다.  
  
    |연결 형식|매개 변수 이름|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET 및 SQLMOBILE|\@\<parameter name>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL 및 OLE DB|0, 1, 2, 3, ...|  
  
10. **변수 이름** 목록에서 변수를 선택합니다. 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)을 참조하세요.  
  
11. **방향** 목록에서 매개 변수가 입력, 출력 또는 반환 값인지 여부를 지정합니다.  
  
12. **데이터 형식** 목록에서 매개 변수의 데이터 형식을 설정합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수의 데이터 형식은 변수의 데이터 형식과 호환되어야 합니다.  
  
13. SQL 문의 각 매개 변수에 대해 8에서 11단계를 반복합니다.  
  
    > [!IMPORTANT]  
    >  매개 변수 매핑의 순서는 SQL 문에 표시된 매개 변수의 순서와 동일해야 합니다.  
  
14. **확인**을 클릭합니다.  

##  <a name="get-the-values-of-return-codes"></a><a name="Return_codes"></a> 반환 코드 값 가져오기  
 저장 프로시저는 반환 코드라고 하는 정수 값을 반환하여 프로시저의 실행 상태를 나타낼 수 있습니다. SQL 실행 태스크에 반환 코드를 구현하려면 **ReturnValue** 유형의 매개 변수를 사용합니다.  
  
 다음 표에서는 반환 코드를 구현하는 EXEC 명령의 몇 가지 예를 연결 형식별로 나열합니다. 모든 예에서는 **input** 매개 변수를 사용합니다. 매개 변수 표식과 매개 변수 이름을 사용하는 방법에 대한 규칙은**Input**, **Output**, **ReturnValue** 등의 모든 매개 변수 유형에 대해 동일합니다.  
  
 일부 구문은 매개 변수 리터럴을 지원하지 않습니다. 이러한 경우 변수를 사용하여 매개 변수 값을 제공해야 합니다.  
  
|연결 형식|EXEC 구문|  
|---------------------|-----------------|  
|EXCEL 및 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> ODBC 호출 구문에 대한 자세한 내용은 MSDN Library의 ODBC 프로그래머 참조에서 [프로시저 매개 변수](https://go.microsoft.com/fwlink/?LinkId=89462)항목을 참조하십시오.|  
|ADO|IsQueryStoreProcedure가 **False**로 설정된 경우 `EXEC ? = myStoredProcedure 1`<br /><br /> IsQueryStoreProcedure가 **True**로 설정된 경우 `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Set IsQueryStoreProcedure가 **True**로 설정됩니다.<br /><br /> `myStoredProcedure`|  
  
 위의 표에 나와 있는 구문에서 SQL 실행 태스크는 **직접 입력** 원본 유형을 사용하여 저장 프로시저를 실행합니다. 이 SQL 실행 태스크는 **파일 연결** 원본 유형을 사용하여 저장 프로시저를 실행할 수도 있습니다. SQL 실행 태스크에서 **직접 입력** 또는 **파일 연결** 원본 유형 중 어느 것을 사용하든 간에 **ReturnValue** 유형의 매개 변수를 사용하여 반환 코드를 구현합니다.
  
 Transact-SQL 저장 프로시저에서 반환 코드 사용에 대한 자세한 내용은 [RETURN&#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)을 참조하세요.  
  
## <a name="result-sets-in-the-execute-sql-task"></a>SQL 실행 태스크의 결과 집합
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 결과 집합이 SQL 실행 태스크에 반환되는지 여부는 태스크에 사용되는 SQL 명령의 유형에 따라 다릅니다. 예를 들어 SELECT 문은 일반적으로 결과 집합을 반환하지만 INSERT 문은 결과 집합을 반환하지 않습니다.  
  
 결과 집합의 내용도 SQL 명령에 따라 다릅니다. 예를 들어 SELECT 문의 결과 집합은 행을 포함하지 않을 수도 있고, 하나 이상의 행을 포함할 수 있습니다. 그러나 개수 또는 합계를 반환하는 SELECT 문의 결과 집합에는 행 하나만 포함되어 있습니다.  
  
 SQL 실행 태스크에서 결과 집합을 사용하려면 SQL 명령에서 결과 집합을 반환하는지 여부와 결과 집합의 내용을 아는 것만으로는 충분하지 않습니다. SQL 실행 태스크에서 결과 집합을 제대로 사용하려면 추가적인 사용 요구 사항과 지침을 따라야 합니다. 이 항목의 나머지 부분에서는 이러한 사용 요구 사항과 지침을 설명합니다.  
  
-   [결과 집합 유형 지정](#Result_set_type)  
  
-   [결과 집합으로 변수 채우기](#Populate_variable_with_result_set)  
  
###  <a name="specify-a-result-set-type"></a><a name="Result_set_type"></a> 결과 집합 유형 지정  
 SQL 실행 태스크는 다음 유형의 결과 집합을 지원합니다.  
  
-   **없음** 결과 집합은 쿼리에서 결과가 반환되지 않을 때 사용합니다. 예를 들어 이 결과 집합은 테이블에서 레코드를 추가, 변경 및 삭제하는 쿼리에 사용됩니다.  
  
-   **단일 행** 결과 집합은 쿼리에서 하나의 행만 반환될 때 사용합니다. 예를 들어 이 결과 집합은 개수 또는 합계를 반환하는 SELECT 문에 사용됩니다.  
  
-   **전체 결과 집합** 결과 집합은 쿼리에서 여러 개의 행이 반환될 때 사용합니다. 예를 들어 이 결과 집합은 테이블의 모든 행을 검색하는 SELECT 문에 사용됩니다.  
  
-   **XML** 결과 집합은 쿼리에서 XML 형식의 결과 집합이 반환될 때 사용합니다. 예를 들어 이 결과 집합은 FOR XML 절을 포함한 SELECT 문에 사용됩니다.  
  
 SQL 실행 태스크가 **전체 결과 집합** 결과 집합을 사용하고 쿼리가 여러 행 집합을 반환하는 경우 작업은 첫 번째 행 집합만 반환합니다. 이 행 집합에서 오류가 발생하는 경우 태스크에서 오류를 보고합니다. 다른 행 집합에서 오류가 발생하는 경우 태스크에서 오류를 보고하지 않습니다.  
  
###  <a name="populate-a-variable-with-a-result-set"></a><a name="Populate_variable_with_result_set"></a> 결과 집합으로 변수 채우기  
 결과 집합 유형이 단일 행, 행 집합 또는 XML일 경우 쿼리에서 반환된 결과 집합을 사용자 정의 변수에 바인딩할 수 있습니다.  
  
 결과 집합 유형이 **단일 행**인 경우 열 이름을 결과 집합 이름으로 사용하여 반환 결과의 열을 변수에 바인딩하거나 열 목록의 열의 서수 위치를 결과 집합 이름으로 사용할 수 있습니다. 예를 들어 `SELECT Color FROM Production.Product WHERE ProductID = ?` 쿼리에 대한 결과 집합 이름은 **Color** 또는 **0**일 수 있습니다. 쿼리에서 여러 열을 반환하고 모든 열의 값에 액세스하려는 경우 각 열을 다른 변수에 바인딩해야 합니다. 번호를 결과 집합 이름으로 사용하여 열을 변수에 매핑하면 열이 쿼리의 열 목록에 표시되는 순서가 번호로 적용됩니다. 예를 들어 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`쿼리에서 **Color** 열에 대해 0을 사용하고 **ListPrice** 열에 대해 1을 사용할 수 있습니다. 열 이름을 결과 집합 이름으로 사용하는 기능은 태스크에서 사용하도록 구성된 공급자에 따라 달라집니다. 일부 공급자만 열 이름을 사용할 수 있습니다.  
  
 단일 값을 반환하는 일부 쿼리에는 열 이름이 포함되지 않을 수 있습니다. 예를 들어 `SELECT COUNT (*) FROM Production.Product` 문은 열 이름을 반환하지 않습니다. 서수 위치인 0을 결과 이름으로 사용하여 반환 결과에 액세스할 수 있습니다. 열 이름별로 반환 결과에 액세스하려면 쿼리에 AS \<alias name> 절을 포함하여 열 이름을 제공해야 합니다. `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`문은 **CountOfProduct** 열을 제공합니다. **CountOfProduct** 열 이름 또는 서수 위치 0을 사용하여 반환 결과 열에 액세스할 수 있습니다.  
  
 결과 집합 유형이 **전체 결과 집합** 이나 **XML**이면 결과 집합 이름으로 0을 사용해야 합니다.  
  
 변수를 **단일 행** 결과 집합 유형이 있는 결과 집합에 매핑하면 변수에는 결과 집합이 포함하는 열의 데이터 형식과 호환되는 데이터 형식이 있어야 합니다. 예를 들어 **String** 데이터 형식이 있는 열을 포함하는 결과 집합은 숫자 데이터 형식의 변수에 매핑할 수 없습니다. **TypeConversionMode** 속성을 **Allowed**로 설정하면 SQL 실행 태스크는 출력 매개 변수와 쿼리 결과를 결과가 할당되는 변수의 데이터 형식으로 변환합니다.  
  
 XML 결과 집합은 **String** 또는 **Object** 데이터 형식의 변수에만 매핑할 수 있습니다. 변수에 **String** 데이터 형식이 있는 경우 SQL 실행 태스크는 문자열을 반환하고 XML 원본은 XML 데이터를 사용할 수 있습니다. 변수가 **개체** 데이터 형식인 경우 SQL 실행 태스크는 DOM(문서 개체 모델) 개체를 반환합니다.  
  
 **전체 결과 집합** 은 **Object** 데이터 형식의 변수에 매핑되어야 합니다. 반환 결과는 행 집합 개체입니다. Foreach 루프 컨테이너를 사용하여 개체 변수에 저장된 테이블 행 값을 패키지 변수로 추출한 다음 스크립트 태스크를 사용하여 패키지 변수에 저장된 데이터를 파일에 쓸 수 있습니다. Foreach 루프 컨테이너 및 스크립트 태스크를 사용하여 이러한 작업을 수행하는 방법에 대한 데모는 msftisprodsamples.codeplex.com에서 CodePlex 샘플인 [SQL 매개 변수 및 결과 집합 실행](https://go.microsoft.com/fwlink/?LinkId=157863)(영문)을 참조하세요.  
  
 다음 표에는 결과 집합에 매핑될 수 있는 변수의 데이터 형식이 요약되어 있습니다.  
  
|결과 집합 유형|변수의 데이터 형식|개체 유형|  
|---------------------|---------------------------|--------------------|  
|단일 행|결과 집합의 유형 열과 호환되는 모든 형식|해당 없음|  
|전체 결과 집합|**Object**|태스크에서 ADO, OLE DB, Excel 및 ODBC 연결 관리자를 비롯한 네이티브 연결 관리자를 사용하는 경우 반환되는 개체는 ADO **Recordset**입니다.<br /><br /> 태스크에서 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자와 같이 관리되는 연결 관리자를 사용하는 경우 반환되는 개체는 **System.Data.DataSet**입니다.<br /><br /> 다음 예제에서처럼 스크립트 태스크를 사용하여 **System.Data.DataSet** 개체에 액세스할 수 있습니다.<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**Object**|태스크에서 ADO, OLE DB, Excel 및 ODBC 연결 관리자 등의 네이티브 연결 관리자를 사용하는 경우 반환되는 개체는 **MSXML6.IXMLDOMDocument**입니다.<br /><br /> 태스크에서 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자와 같이 관리되는 연결 관리자를 사용하는 경우 반환되는 개체는 **System.Xml.XmlDocument**입니다.|  
  
 변수는 SQL 실행 태스크나 패키지 범위에서 정의할 수 있습니다. 변수 범위가 패키지이면 해당 패키지 내의 다른 태스크와 컨테이너는 물론 패키지 실행 또는 DTS 2000 패키지 실행 태스크가 실행한 모든 패키지에서 결과 집합을 사용할 수 있습니다.  
  
 변수를 **단일 행** 결과 집합에 매핑할 때 SQL 문에서 반환하는 문자열이 아닌 값은 다음 조건을 충족하는 경우 문자열로 변환됩니다.  
  
-   **TypeConversionMode** 속성이 True로 설정된 경우. 속성 창 또는 **SQL 실행 태스크 편집기**를 사용하여 속성 값을 설정합니다.  
  
-   변환에서 데이터 잘림이 발생하지 않은 경우  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>결과 집합을 SQL 실행 태스크의 변수에 매핑
이 섹션에서는 결과 집합과 SQL 실행 태스크의 변수 간 매핑을 만드는 방법에 대해 설명합니다. 결과 집합을 변수에 매핑하면 결과 집합을 패키지의 다른 요소에서 사용할 수 있습니다. 예를 들어 스크립트 태스크의 스크립트는 변수를 읽은 다음 결과 집합의 값을 사용할 수 있으며 XML 원본은 변수에 저장된 결과 집합을 사용할 수 있습니다. 부모 패키지에서 결과 집합을 생성하는 경우 결과 집합을 부모 패키지의 변수에 매핑한 다음 부모 변수 값을 저장할 자식 패키지의 부모 패키지 변수 구성을 만들어 패키지 실행 태스크로 호출하는 자식 패키지에서 결과 집합을 사용할 수 있습니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  패키지에 아직 SQL 실행 태스크가 포함되어 있지 않으면 패키지의 제어 흐름에 해당 작업을 추가합니다. 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)를 참조하세요.  
  
5.  SQL 실행 태스크를 두 번 클릭합니다.  
  
6.  **SQL 실행 태스크 편집기** 대화 상자의 **일반** 페이지에서 **단일 행**, **전체 결과 집합**또는 **XML** 결과 집합 형식을 선택합니다.  

7.  **결과 집합**을 클릭합니다.  
  
8.  결과 집합 매핑을 추가하려면 **추가**를 클릭합니다.  
  
9. **변수 이름** 목록에서 변수를 선택하거나 새 변수를 만듭니다. 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)을 참조하세요.  
  
10. 필요에 따라 **결과 이름** 목록에서 결과 집합의 이름을 수정합니다.  
  
     일반적으로 열 이름을 결과 집합 이름으로 사용하거나 열 목록의 열 서수 위치를 결과 집합으로 사용할 수 있습니다. 열 이름을 결과 집합 이름으로 사용하는 기능은 태스크에서 사용하도록 구성된 공급자에 따라 달라집니다. 일부 공급자만 열 이름을 사용할 수 있습니다.  
  
11. **확인**을 클릭합니다.  

## <a name="troubleshoot-the-execute-sql-task"></a>SQL 실행 태스크 문제 해결  
 SQL 실행 태스크가 외부 데이터 공급자에 대해 수행하는 호출을 기록할 수 있습니다. 이 로깅 기능을 사용하여 SQL 실행 태스크가 실행하는 SQL 명령의 문제를 해결할 수 있습니다. SQL 실행 태스크가 외부 데이터 공급자에 대해 수행하는 호출을 기록하려면 패키지 로깅을 사용하도록 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
 경우에 따라 SQL 명령 또는 저장 프로시저는 여러 결과 집합을 반환합니다. 이러한 결과 집합에는 **SELECT** 쿼리의 결과인 행 집합뿐만 아니라 **RAISERROR** 또는 **PRINT** 문에 대한 오류 결과인 단일 값도 포함됩니다. 이 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합의 오류를 무시할지 여부는 사용되는 연결 관리자의 유형에 따라 달라집니다.  
  
-   OLE DB 및 ADO 연결 관리자를 사용하는 경우 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합을 무시합니다. 따라서 이러한 연결 관리자를 사용하는 경우에는 오류가 첫 번째 결과 집합의 일부가 아니면 태스크에서 SQL 명령 또는 저장 프로시저가 반환하는 오류를 무시합니다.  
  
-   ODBC 및 ADO.NET 연결 관리자를 사용하는 경우 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합을 무시하지 않습니다. 이러한 연결 관리자를 사용하는 경우 첫 번째 결과 집합이 아닌 다른 결과 집합에 오류가 포함되어 있으면 오류가 발생하여 태스크에 실패하게 됩니다.  
  
### <a name="custom-log-entries"></a>사용자 지정 로그 항목  
 다음 표에서는 SQL 실행 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|SQL 문의 실행 단계에 대한 정보를 제공합니다. 로그 항목은 태스크에서 데이터베이스에 대한 연결을 설정할 때, 태스크에서 SQL 문 준비를 시작할 때 또는 SQL 문 실행이 완료된 후에 기록됩니다. 준비 단계에 대한 로그 항목은 태스크에서 사용하는 SQL 문을 포함합니다.|  

