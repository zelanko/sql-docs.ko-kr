---
title: SQL 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6be23e1a45f2b2ed0cc055c5032a72ffe2387399
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62831771"
---
# <a name="execute-sql-task"></a>SQL 실행 태스크
  SQL 실행 태스크는 패키지에서 SQL 문이나 저장 프로시저를 실행합니다. 이 태스크는 단일 SQL 문 또는 순서대로 실행되는 여러 SQL 문을 포함할 수 있습니다. SQL 실행 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   데이터를 삽입하기 위해 테이블 또는 뷰를 자릅니다.  
  
-   테이블 및 뷰와 같은 데이터베이스 개체를 만들고 변경 및 삭제합니다.  
  
-   팩트 및 차원 테이블에 데이터를 로드하기 전에 해당 테이블을 다시 만듭니다.  
  
-   저장 프로시저를 실행합니다. SQL 문이 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
-   쿼리에서 반환된 행 집합을 변수에 저장합니다.  
  
 SQL 실행 태스크를 Foreach 루프 및 For 루프 컨테이너와 함께 사용하여 여러 개의 SQL 문을 실행할 수 있습니다. 두 컨테이너는 패키지의 반복 제어 흐름을 구현하며 SQL 실행 태스크를 반복해서 실행할 수 있습니다. 예를 들어 Foreach 루프 컨테이너를 사용하면 패키지가 폴더에 있는 파일을 열거하고 SQL 실행 태스크를 반복 실행하여 각 파일에 저장된 SQL 문을 실행할 수 있습니다.  
  
## <a name="connecting-to-a-data-source"></a>데이터 원본에 연결  
 SQL 실행 태스크는 여러 유형의 연결 관리자를 사용하여 SQL 문이나 저장 프로시저가 실행될 데이터 원본에 연결할 수 있습니다. 다음 표에 나열된 연결 형식을 사용할 수 있습니다.  
  
|연결 형식|ODBC 대상 편집기|  
|---------------------|------------------------|  
|EXCEL|[Excel 연결 관리자](../connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 연결 관리자](../connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 연결 관리자](../connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 연결 관리자](../connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 연결 관리자](../connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 연결 관리자](../connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="creating-sql-statements"></a>SQL 문 만들기  
 이 태스크에 사용되는 SQL 문의 원본은 문이 포함된 작업 속성, 하나 이상의 문이 포함된 파일에 대한 연결 또는 문이 포함된 변수 이름일 수 있습니다. SQL 문은 원본 DBMS(데이터베이스 관리 시스템) 언어로 기록되어야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 쿼리](../integration-services-ssis-queries.md)를 참조하세요.  
  
 SQL 문이 파일에 저장되어 있을 경우 SQL 실행 태스크는 파일 연결 관리자를 사용하여 해당 파일에 연결합니다. 자세한 내용은 [File Connection Manager](../connection-manager/file-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서는 **SQL 실행 태스크 편집기** 대화 상자를 사용하여 SQL 문을 입력하거나 SQL 쿼리 작성용 그래픽 사용자 인터페이스인 **쿼리 작성기**를 사용할 수 있습니다. 자세한 내용은 [SQL 실행 태스크 편집기&#40;일반 페이지&#41;](../execute-sql-task-editor-general-page.md) 및 [쿼리 작성기](../query-builder.md)를 참조하세요.  
  
> [!NOTE]  
>  SQL 실행 태스크 외부에서 작성된 SQL 문은 유효하더라도 SQL 실행 태스크에서 성공적으로 구문 분석되지 않을 수도 있습니다.  
  
> [!NOTE]  
>  SQL 실행 태스크는 `RecognizeAll` ParseMode 열거형 값을 사용합니다. 자세한 내용은 [ManagedBatchParser 네임스페이스](https://go.microsoft.com/fwlink/?LinkId=223617)를 참조하십시오.  
  
## <a name="sending-multiple-statements-in-a-batch"></a>여러 개의 문을 일괄 처리로 전송  
 SQL 실행 태스크에 여러 개의 문이 포함된 경우 문을 그룹화하여 일괄 처리로 실행할 수 있습니다. 일괄 처리의 마지막을 알리려면 GO 명령을 사용합니다. 두 GO 명령 사이의 모든 SQL 문은 일괄 처리로 실행되도록 OLE DB Provider에 전송됩니다. SQL 명령은 GO 명령으로 구분된 여러 개의 일괄 처리를 포함할 수 있습니다.  
  
 일괄 처리로 그룹화할 수 있는 SQL 문의 종류에는 제한이 있습니다. 자세한 내용은 [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)을 참조하세요.  
  
 SQL 실행 태스크에서 SQL 문의 일괄 처리를 실행하는 경우 해당 일괄 처리에 다음 규칙이 적용됩니다.  
  
-   일괄 처리의 첫 번째 문 하나만 결과 집합을 반환할 수 있습니다.  
  
-   결과 집합에 결과 바인딩을 사용하는 경우 쿼리에서 동일한 수의 열이 반환되어야 합니다. 쿼리에서 반환된 열 수가 서로 다르면 태스크가 실패합니다. 그러나 태스크 실패해도 해당 태스크에서 실행하는 DELETE 또는 INSERT와 같은 쿼리는 성공할 수 있습니다.  
  
-   결과 바인딩에 열 이름을 사용하는 경우 태스크에 사용된 결과 집합 이름과 동일한 이름이 포함된 열이 쿼리에서 반환되어야 합니다. 해당 열이 없으면 태스크가 실패합니다.  
  
-   태스크에 매개 변수 바인딩이 사용되는 경우 일괄 처리의 모든 쿼리에 동일한 수와 유형의 매개 변수를 사용해야 합니다.  
  
## <a name="running-parameterized-sql-commands"></a>매개 변수가 있는 SQL 명령 실행  
 SQL 문과 저장 프로시저는 일반적으로 입력 매개 변수, 출력 매개 변수 및 반환 코드를 사용합니다. SQL 실행 태스크는 `Input`, `Output` 및 `ReturnValue` 매개 변수 유형을 지원합니다. 입력 매개 변수에는 `Input` 유형, 출력 매개 변수에는 `Output` 유형, 반환 코드에는 `ReturnValue` 유형을 사용합니다.  
  
> [!NOTE]  
>  데이터 공급자가 지원하는 경우에만 SQL 실행 태스크에 매개 변수를 사용할 수 있습니다.  
  
 SQL 실행 태스크에서 매개 변수 및 반환 코드를 사용하는 방법은 [SQL 실행 태스크의 매개 변수 및 반환 코드](execute-sql-task.md)를 참조하세요.  
  
## <a name="specifying-a-result-set-type"></a>결과 집합 유형 지정  
 SQL 명령 유형에 따라 SQL 실행 태스크에서 결과 집합이 반환될 수도 있고 반환되지 않을 수도 있습니다. 예를 들어 SELECT 문은 일반적으로 결과 집합을 반환하지만 INSERT 문은 결과 집합을 반환하지 않습니다. SELECT 문의 결과 집합은 행을 포함하지 않을 수도 있고, 하나 이상의 행을 포함할 수 있습니다. 저장 프로시저도 반환 코드라고 하는 정수 값을 반환하여 프로시저의 실행 상태를 표시할 수 있습니다. 이 경우에는 결과 집합이 단일 행으로 구성됩니다.  
  
 SQL 실행 태스크의 SQL 명령에서 결과 집합을 검색하는 방법은 [SQL 실행 태스크의 결과 집합](../result-sets-in-the-execute-sql-task.md)을 참조하세요.  
  
## <a name="troubleshooting-the-execute-sql-task"></a>SQL 실행 태스크 문제 해결  
 SQL 실행 태스크가 외부 데이터 공급자에 대해 수행하는 호출을 기록할 수 있습니다. 이 로깅 기능을 사용하여 SQL 실행 태스크가 실행하는 SQL 명령의 문제를 해결할 수 있습니다. SQL 실행 태스크가 외부 데이터 공급자에 대해 수행하는 호출을 기록하려면 패키지 로깅을 사용하도록 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
 경우에 따라 SQL 명령 또는 저장 프로시저는 여러 결과 집합을 반환합니다. 이러한 결과 집합에는 `SELECT` 쿼리의 결과인 행 집합뿐만 아니라 `RAISERROR` 또는 `PRINT` 문에 대한 오류 결과인 단일 값도 포함됩니다. 이 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합의 오류를 무시할지 여부는 사용되는 연결 관리자의 유형에 따라 달라집니다.  
  
-   OLE DB 및 ADO 연결 관리자를 사용하는 경우 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합을 무시합니다. 따라서 이러한 연결 관리자를 사용하는 경우에는 오류가 첫 번째 결과 집합의 일부가 아니면 태스크에서 SQL 명령 또는 저장 프로시저가 반환하는 오류를 무시합니다.  
  
-   ODBC 및 ADO.NET 연결 관리자를 사용하는 경우 태스크에서 첫 번째 결과 집합 후에 발생하는 결과 집합을 무시하지 않습니다. 이러한 연결 관리자를 사용하는 경우 첫 번째 결과 집합이 아닌 다른 결과 집합에 오류가 포함되어 있으면 오류가 발생하여 태스크에 실패하게 됩니다.  
  
### <a name="custom-log-entries"></a>사용자 지정 로그 항목  
 다음 표에서는 SQL 실행 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|설명|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|SQL 문의 실행 단계에 대한 정보를 제공합니다. 로그 항목은 태스크에서 데이터베이스에 대한 연결을 설정할 때, 태스크에서 SQL 문 준비를 시작할 때 또는 SQL 문 실행이 완료된 후에 기록됩니다. 준비 단계에 대한 로그 항목은 태스크에서 사용하는 SQL 문을 포함합니다.|  
  
## <a name="configuring-the-execute-sql-task"></a>SQL 실행 태스크 구성  
 다음과 같은 방법으로 SQL 실행 태스크를 구성할 수 있습니다.  
  
-   데이터베이스에 연결할 때 사용할 연결 관리자 유형을 지정합니다.  
  
-   SQL 문에서 반환되는 결과 집합 유형을 지정합니다.  
  
-   SQL 문의 제한 시간을 지정합니다.  
  
-   SQL 문의 원본을 지정합니다.  
  
-   태스크에서 SQL 문의 준비 단계를 건너뛸지를 나타냅니다.  
  
-   ADO 연결 형식을 사용하는 경우 SQL 문이 저장 프로시저인지 여부를 나타내야 합니다. 다른 연결 유형에서 이 속성은 읽기 전용이며 항상 `false` 값을 갖습니다.  
  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SQL 실행 태스크 편집기 &#40;일반 페이지&#41;](../execute-sql-task-editor-general-page.md)  
  
-   [SQL 실행 태스크 편집기 &#40;매개 변수 매핑 페이지&#41;](../execute-sql-task-editor-parameter-mapping-page.md)  
  
-   [SQL 실행 태스크 편집기 &#40;결과 집합 페이지&#41;](../execute-sql-task-editor-result-set-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="configuring-the-execute-sql-task-programmatically"></a>프로그래밍 방식으로 SQL 실행 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [쿼리 매개 변수를 SQL 실행 태스크의 변수에 매핑](../map-query-parameters-to-variables-in-an-execute-sql-task.md)  
  
-   [결과 집합을 SQL 실행 태스크의 변수에 매핑](../map-result-sets-to-variables-in-an-execute-sql-task.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   [SQL 실행 태스크의 매개 변수 및 반환 코드](execute-sql-task.md)  
  
-   [SQL 실행 태스크의 결과 집합](../result-sets-in-the-execute-sql-task.md)  
  
-   [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)  
  
-   mssqltips.com의 블로그 항목 - [SQL Server 2012에서의 새로운 날짜 및 시간 함수](https://go.microsoft.com/fwlink/?LinkId=239783)  
  
  
