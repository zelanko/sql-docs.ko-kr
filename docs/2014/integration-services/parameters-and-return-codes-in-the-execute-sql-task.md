---
title: SQL 실행 태스크의 매개 변수 및 반환 코드 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e9009bfb7b44f6690d123697059e105d76688ce0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964773"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>SQL 실행 태스크의 매개 변수 및 반환 코드
  SQL 문과 저장 프로시저에서는 일반적으로 `input` 매개 변수, `output` 매개 변수 및 반환 코드를 사용합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 SQL 실행 태스크는 `Input`, `Output` 및 `ReturnValue` 매개 변수 유형을 지원합니다. 입력 매개 변수에는 `Input` 유형, 출력 매개 변수에는 `Output` 유형, 반환 코드에는 `ReturnValue` 유형을 사용합니다.  
  
> [!NOTE]  
>  데이터 공급자가 지원하는 경우에만 SQL 실행 태스크에 매개 변수를 사용할 수 있습니다.  
  
 쿼리와 저장 프로시저를 포함하여 SQL 명령의 매개 변수는 SQL 실행 태스크의 범위, 부모 컨테이너 또는 패키지 범위 내에서 생성된 사용자 정의 변수에 매핑됩니다. 변수 값은 디자인 타임에 설정하거나 런타임에 동적으로 채울 수 있습니다. 매개 변수를 시스템 변수에 매핑할 수도 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md) 및 [시스템 변수](system-variables.md)를 참조하세요.  
  
 그러나 SQL 실행 태스크에서 매개 변수 및 반환 코드를 사용하려면 태스크에서 지원되는 매개 변수 유형 및 이러한 매개 변수가 매핑되는 방식을 이해하는 것만으로는 충분하지 않습니다. SQL 실행 태스크에서 매개 변수 및 반환 코드를 제대로 사용하려면 추가적인 사용 요구 사항과 지침을 따라야 합니다. 이 항목의 나머지 부분에서는 이러한 사용 요구 사항과 지침을 설명합니다.  
  
-   [매개 변수 이름 및 표식 사용](#Parameter_names_and_markers)  
  
-   [날짜 및 시간 데이터 형식의 매개 변수 사용](#Date_and_time_data_types)  
  
-   [WHERE 절에 매개 변수 사용](#WHERE_clauses)  
  
-   [저장 프로시저에 매개 변수 사용](#Stored_procedures)  
  
-   [반환 코드 값 가져오기](#Return_codes)  
  
-   [SQL 실행 태스크 편집기에서 매개 변수 및 반환 코드 구성](#Configure_parameters_and_return_codes)  
  
##  <a name="using-parameter-names-and-markers"></a><a name="Parameter_names_and_markers"></a>매개 변수 이름 및 표식 사용  
 SQL 실행 태스크가 사용하는 연결 형식에 따라 SQL 명령 구문이 사용하는 매개 변수 표식이 달라집니다. 예를 들어 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자 유형을 사용 하려면 SQL 명령에 형식 ** \@ varparameter**의 매개 변수 표식을 사용 해야 하지만 OLE DB 연결 형식에는 물음표 (?) 매개 변수 표식을 사용 해야 합니다.  
  
 변수와 매개 변수 간 매핑에 매개 변수 이름으로 사용할 수 있는 이름도 연결 관리자 유형에 따라 달라집니다. 예를 들어 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자 유형에는 \@ 접두사가 있는 사용자 정의 이름을 사용하지만 OLE DB 연결 관리자 유형에는 0부터 시작하는 서수의 숫자 값을 매개 변수 이름으로 사용해야 합니다.  
  
 다음 표에서는 SQL 실행 태스크가 사용할 수 있는 연결 관리자 유형에 대한 SQL 명령 요구 사항을 요약합니다.  
  
|연결 형식|매개 변수 표식|매개 변수 이름|SQL 명령 예|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<parameter name>|\@\<parameter name>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 및 OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 및 ADO 연결 관리자의 매개 변수 사용  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 및 ADO 연결 관리자에는 매개 변수를 사용하는 SQL 명령에 대한 특별한 요구 사항이 있습니다.  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자를 사용하려면 SQL 명령에 매개 변수 이름을 매개 변수 표식으로 사용해야 합니다. 즉, 변수를 매개 변수에 직접 매핑할 수 있습니다. 예를 들어 `@varName` 변수는 `@parName` 이라는 매개 변수에 매핑되고 `@parName`매개 변수에 값을 제공합니다.  
  
-   ADO 연결 관리자를 사용하려면 SQL 명령에 물음표(?)를 매개 변수 표식으로 사용해야 합니다. 그러나 정수 값을 제외한 모든 사용자 정의 이름을 매개 변수 이름으로 사용할 수 있습니다.  
  
 매개 변수에 값을 제공하기 위해 변수는 매개 변수 이름에 매핑됩니다. 그런 다음 SQL 실행 태스크에서 매개 변수 목록에 있는 매개 변수 이름의 서수 값을 사용하여 변수의 값을 매개 변수에 로드합니다.  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>EXCEL, ODBC 및 OLE DB 연결 관리자의 매개 변수 사용  
 EXCEL, ODBC 및 OLE DB 연결 관리자를 사용하려면 SQL 명령에 물음표(?)를 매개 변수 표식으로 사용하고 0 또는 1부터 시작하는 숫자 값을 매개 변수 이름으로 사용해야 합니다. SQL 실행 태스크에서 ODBC 연결 관리자를 사용하면 쿼리의 첫 번째 매개 변수에 매핑되는 매개 변수 이름이 1이고, 그렇지 않으면 이 매개 변수 이름이 0입니다. 후속 매개 변수의 경우에도 매개 변수 이름의 숫자 값이 SQL 명령에서 매개 변수 이름이 매핑되는 매개 변수를 나타냅니다. 예를 들어 이름이 3인 매개 변수는 세 번째 매개 변수에 매핑되며 SQL 명령에서 세 번째 물음표(?)로 표현됩니다.  
  
 매개 변수에 값을 제공하기 위해 변수가 매개 변수 이름에 매핑되고 SQL 실행 태스크에서 매개 변수 이름의 서수 값을 사용하여 변수 값을 매개 변수에 로드합니다.  
  
 연결 관리자에서 사용하는 공급자에 따라 일부 OLE DB 데이터 형식이 지원되지 않을 수 있습니다. 예를 들어 Excel 드라이버는 제한된 데이터 형식 집합만 인식합니다. Excel 드라이버를 사용하는 Jet 공급자의 동작에 대한 자세한 내용은 [Excel Source](data-flow/excel-source.md)을 참조하십시오.  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>OLE DB 연결 관리자의 매개 변수 사용  
 SQL 실행 태스크에서 OLE DB 연결 관리자를 사용할 때는 태스크의 BypassPrepare 속성을 사용할 수 있습니다. SQL 실행 태스크에서 매개 변수가 있는 SQL 문을 사용하는 경우 이 속성을 `true`로 설정해야 합니다.  
  
 OLE DB 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 OLE DB Provider를 통해 매개 변수 정보를 파생할 수 없으므로 매개 변수가 있는 하위 쿼리를 사용할 수 없습니다. 그러나 식을 사용하여 매개 변수 값을 쿼리 문자열로 연결하고 태스크의 SqlStatementSource 속성을 설정할 수 있습니다.  
  
##  <a name="using-parameters-with-date-and-time-data-types"></a><a name="Date_and_time_data_types"></a>날짜 및 시간 데이터 형식에 매개 변수 사용  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 및 ADO 연결 관리자의 날짜 및 시간 매개 변수 사용  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 형식인 `time` 및 `datetimeoffset` 데이터를 읽을 때는 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 또는 ADO 연결 관리자를 사용하는 SQL 실행 태스크에 다음과 같은 요구 사항이 추가로 적용됩니다.  
  
-   데이터의 경우 `time` [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자를 사용 하려면 매개 변수 유형이 `Input` 또는이 `Output` 고 데이터 형식이 인 매개 변수에이 데이터를 저장 해야 합니다 `string` .  
  
-   `datetimeoffset` 데이터의 경우 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자를 사용하려면 다음과 같은 매개 변수 중 하나에 이 데이터가 저장되어야 합니다.  
  
    -   매개 변수 유형이 `Input`이고 데이터 형식이 `string`인 매개 변수  
  
    -   매개 변수 유형이 `Output` 또는 `ReturnValue`이고 데이터 형식이 `datetimeoffset`, `string` 또는 `datetime2`인 매개 변수. 데이터 형식이 `string` 또는 `datetime2`인 매개 변수를 선택하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 데이터를 string 또는 datetime2로 변환합니다.  
  
-   ADO 연결 관리자를 사용하려면 매개 변수 유형이 `time` 또는 `datetimeoffset`이고 데이터 형식이 `Input`인 매개 변수에 `Output` 또는 `adVarWchar` 데이터를 저장해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 및 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조하세요.  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>OLE DB 연결 관리자의 날짜 및 시간 매개 변수 사용  
 OLE DB 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 형식인 `date`, `time`, `datetime`, `datetime2` 및 `datetimeoffset` 데이터를 스토리지할 때 특수한 요구 사항이 적용됩니다. 이러한 데이터를 다음과 같은 매개 변수 유형 중 하나에 저장해야 합니다.  
  
-   NVARCHAR 데이터 형식의 입력 매개 변수  
  
-   다음 표에 나열된 적절한 데이터 형식의 출력 매개 변수  
  
    |`Output` 매개 변수 유형|날짜 데이터 형식|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 적절한 입력 또는 출력 매개 변수에 데이터가 저장되지 않으면 패키지가 실패합니다.  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>ODBC 연결 관리자의 날짜 및 시간 매개 변수 사용  
 ODBC 연결 관리자를 사용하는 경우 SQL 실행 태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 형식인 `date`, `time`, `datetime`, `datetime2` 또는 `datetimeoffset` 데이터를 스토리지할 때 특수한 요구 사항이 적용됩니다. 이러한 데이터를 다음과 같은 매개 변수 유형 중 하나에 저장해야 합니다.  
  
-   SQL_WVARCHAR 데이터 형식의 `input` 매개 변수  
  
-   다음 표에 나와 있는 적절한 데이터 형식의 `output` 매개 변수  
  
    |`Output` 매개 변수 유형|날짜 데이터 형식|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> 또는<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 적절한 입력 또는 출력 매개 변수에 데이터가 저장되지 않으면 패키지가 실패합니다.  
  
##  <a name="using-parameters-in-where-clauses"></a><a name="WHERE_clauses"></a>WHERE 절에 매개 변수 사용  
 원본 테이블의 각 행이 SQL 명령에 적합하도록 만들기 위해 만족시켜야 할 조건을 정의하는 필터를 지정하기 위해 SELECT, INSERT, UPDATE 및 DELETE 명령에 WHERE 절을 포함하는 경우가 많습니다. 매개 변수는 WHERE 절에 필터 값을 제공합니다.  
  
 매개 변수 표식을 사용하여 매개 변수 값을 동적으로 제공할 수 있습니다. SQL 문에 사용할 수 있는 매개 변수 표식 및 매개 변수 이름에 대한 규칙은 SQL 실행이 사용하는 연결 관리자 유형에 따라 달라집니다.  
  
 다음 표에서는 연결 관리자 유형별 SELECT 명령의 예를 나열합니다. INSERT, UPDATE 및 DELETE 문도 이와 비슷합니다. 이 예에서는 SELECT를 사용하여 **의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 **ProductID** 가 두 매개 변수로 지정된 값보다 크고 작은 제품을 반환합니다.  
  
|연결 형식|SELECT 구문|  
|---------------------|-------------------|  
|EXCEL, ODBC 및 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 이 예에서는 다음과 같은 이름의 매개 변수가 필요합니다.  
  
-   EXCEL 및 OLED DB 연결 관리자는 매개 변수 이름으로 0과 1을 사용하고 ODBC 연결 형식은 1과 2를 사용합니다.  
  
-   ADO 연결 형식에서는 Param1 및 Param2와 같은 임의의 두 매개 변수 이름을 사용할 수 있지만 이러한 매개 변수는 매개 변수 목록에서의 서수 위치에 따라 매핑되어야 합니다.  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 형식에서는 매개 변수 이름 \@parmMinProductID 및 \@parmMaxProductID를 사용합니다.  
  
##  <a name="using-parameters-with-stored-procedures"></a><a name="Stored_procedures"></a>저장 프로시저에 매개 변수 사용  
 저장 프로시저를 실행하는 SQL 명령도 매개 변수 매핑을 사용할 수 있습니다. 매개 변수 표식 및 매개 변수 이름 사용 방법에 대한 규칙은 매개 변수가 있는 쿼리에 대한 규칙에서와 마찬가지로 SQL 실행이 사용하는 연결 관리자 유형에 따라 달라집니다.  
  
 다음 표에서는 연결 관리자 유형별 EXEC 명령의 예를 나열합니다. 이 예에서는 **의** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]저장 프로시저를 실행합니다. 저장 프로시저는 `@StartProductID` 및 `@CheckDate` `input` 매개 변수를 사용 합니다.  
  
|연결 형식|EXEC 구문|  
|---------------------|-----------------|  
|EXCEL 및 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> ODBC 호출 구문에 대한 자세한 내용은 MSDN Library의 ODBC 프로그래머 참조에서 [프로시저 매개 변수](https://go.microsoft.com/fwlink/?LinkId=89462)항목을 참조하십시오.|  
|ADO|IsQueryStoredProcedure `False` 가로 설정 된 경우`EXEC uspGetBillOfMaterials ?, ?`<br /><br /> IsQueryStoredProcedure `True` 가로 설정 된 경우`uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|IsQueryStoredProcedure `False` 가로 설정 된 경우`EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> IsQueryStoredProcedure `True` 가로 설정 된 경우`uspGetBillOfMaterials`|  
  
 출력 매개 변수를 사용하려면 구문에서 각 매개 변수 표식 다음에 OUTPUT 키워드가 와야 합니다. 올바른 출력 매개 변수 구문의 예로 `EXEC myStoredProcedure ? OUTPUT`을 들 수 있습니다.  
  
 Transact-SQL 저장 프로시저에서 입력 및 출력 매개 변수 사용에 대한 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)를 참조하세요.  
  
##  <a name="getting-values-of-return-codes"></a><a name="Return_codes"></a>반환 코드 값 가져오기  
 저장 프로시저는 반환 코드라고 하는 정수 값을 반환하여 프로시저의 실행 상태를 나타낼 수 있습니다. SQL 실행 태스크에 반환 코드를 구현하려면 `ReturnValue` 유형의 매개 변수를 사용합니다.  
  
 다음 표에서는 반환 코드를 구현하는 EXEC 명령의 몇 가지 예를 연결 형식별로 나열합니다. 모든 예에서는 `input` 매개 변수를 사용합니다. 매개 변수 표식 및 매개 변수 이름을 사용 하는 방법에 대 한 규칙은 모든 매개 변수 형식, 및에 대해 동일 합니다 `Input` `Output` `ReturnValue` .  
  
 일부 구문은 매개 변수 리터럴을 지원하지 않습니다. 이러한 경우 변수를 사용하여 매개 변수 값을 제공해야 합니다.  
  
|연결 형식|EXEC 구문|  
|---------------------|-----------------|  
|EXCEL 및 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> ODBC 호출 구문에 대한 자세한 내용은 MSDN Library의 ODBC 프로그래머 참조에서 [프로시저 매개 변수](https://go.microsoft.com/fwlink/?LinkId=89462)항목을 참조하십시오.|  
|ADO|IsQueryStoreProcedure `False` 가로 설정 된 경우`EXEC ? = myStoredProcedure 1`<br /><br /> IsQueryStoreProcedure `True` 가로 설정 된 경우`myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Set IsQueryStoreProcedure는로 설정 됩니다 `True` .<br /><br /> `myStoredProcedure`|  
  
 위의 표에 나와 있는 구문에서 SQL 실행 태스크는 **직접 입력** 원본 유형을 사용하여 저장 프로시저를 실행합니다. 이 SQL 실행 태스크는 **파일 연결** 원본 유형을 사용하여 저장 프로시저를 실행할 수도 있습니다. SQL 실행 태스크에서 **직접 입력** 또는 **파일 연결** 원본 유형을 사용 하는지 여부에 관계 없이 형식의 매개 변수를 사용 `ReturnValue` 하 여 반환 코드를 구현 합니다. SQL 실행 태스크에서 실행하는 SQL 문의 원본 유형 구성 방법에 대한 자세한 내용은 [SQL 실행 태스크 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)를 참조하세요.  
  
 Transact-SQL 저장 프로시저에서 반환 코드 사용에 대한 자세한 내용은 [RETURN&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql)을 참조하세요.  
  
##  <a name="configuring-parameters-and-return-codes-in-the-execute-sql-task"></a><a name="Configure_parameters_and_return_codes"></a>SQL 실행 태스크에서 매개 변수 및 반환 코드 구성  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 매개 변수 및 반환 코드 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [SQL 실행 태스크 편집기 &#40;매개 변수 매핑 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [태스크 또는 컨테이너의 속성 설정](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   blogs.msdn.com의 블로그 항목 - [출력 매개 변수를 포함하는 저장 프로시저(Stored procedures with output parameters)](https://go.microsoft.com/fwlink/?LinkId=157786)  
  
-   msftisprodsamples.codeplex.com의 CodePlex 예제 - [SQL 실행 매개 변수 및 결과 집합(Execute SQL Parameters and Result Sets)](https://go.microsoft.com/fwlink/?LinkId=157863)  
  
## <a name="see-also"></a>참고 항목  
 [SQL 실행 태스크](control-flow/execute-sql-task.md)   
 [SQL 실행 태스크의 결과 집합](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
