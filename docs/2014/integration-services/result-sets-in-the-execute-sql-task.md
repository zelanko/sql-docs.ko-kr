---
title: SQL 실행 태스크의 결과 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8efb049292caecf21f38ef5bc5a7392138bdcf5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056426"
---
# <a name="result-sets-in-the-execute-sql-task"></a>SQL 실행 태스크의 결과 집합
  
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 결과 집합이 SQL 실행 태스크에 반환되는지 여부는 태스크에 사용되는 SQL 명령의 유형에 따라 다릅니다. 예를 들어 SELECT 문은 일반적으로 결과 집합을 반환하지만 INSERT 문은 결과 집합을 반환하지 않습니다.  
  
 결과 집합의 내용도 SQL 명령에 따라 다릅니다. 예를 들어 SELECT 문의 결과 집합은 행을 포함하지 않을 수도 있고, 하나 이상의 행을 포함할 수 있습니다. 그러나 개수 또는 합계를 반환하는 SELECT 문의 결과 집합에는 행 하나만 포함되어 있습니다.  
  
 SQL 실행 태스크에서 결과 집합을 사용하려면 SQL 명령에서 결과 집합을 반환하는지 여부와 결과 집합의 내용을 아는 것만으로는 충분하지 않습니다. SQL 실행 태스크에서 결과 집합을 제대로 사용하려면 추가적인 사용 요구 사항과 지침을 따라야 합니다. 이 항목의 나머지 부분에서는 이러한 사용 요구 사항과 지침을 설명합니다.  
  
-   [결과 집합 유형 지정](#Result_set_type)  
  
-   [결과 집합으로 변수 채우기](#Populate_variable_with_result_set)  
  
-   [SQL 실행 태스크 편집기에서 결과 집합 구성](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a>결과 집합 유형 지정  
 SQL 실행 태스크는 다음 유형의 결과 집합을 지원합니다.  
  
-   
  **없음** 결과 집합은 쿼리에서 결과가 반환되지 않을 때 사용합니다. 예를 들어 이 결과 집합은 테이블에서 레코드를 추가, 변경 및 삭제하는 쿼리에 사용됩니다.  
  
-   
  **단일 행** 결과 집합은 쿼리에서 하나의 행만 반환될 때 사용합니다. 예를 들어 이 결과 집합은 개수 또는 합계를 반환하는 SELECT 문에 사용됩니다.  
  
-   
  **전체 결과 집합** 결과 집합은 쿼리에서 여러 개의 행이 반환될 때 사용합니다. 예를 들어 이 결과 집합은 테이블의 모든 행을 검색하는 SELECT 문에 사용됩니다.  
  
-   
  **XML** 결과 집합은 쿼리에서 XML 형식의 결과 집합이 반환될 때 사용합니다. 예를 들어 이 결과 집합은 FOR XML 절을 포함한 SELECT 문에 사용됩니다.  
  
 SQL 실행 태스크가 **전체 결과 집합** 결과 집합을 사용하고 쿼리가 여러 행 집합을 반환하는 경우 작업은 첫 번째 행 집합만 반환합니다. 이 행 집합에서 오류가 발생하는 경우 태스크에서 오류를 보고합니다. 다른 행 집합에서 오류가 발생하는 경우 태스크에서 오류를 보고하지 않습니다.  
  
##  <a name="Populate_variable_with_result_set"></a>결과 집합으로 변수 채우기  
 결과 집합 유형이 단일 행, 행 집합 또는 XML일 경우 쿼리에서 반환된 결과 집합을 사용자 정의 변수에 바인딩할 수 있습니다.  
  
 결과 집합 유형이 **단일 행**인 경우 열 이름을 결과 집합 이름으로 사용하여 반환 결과의 열을 변수에 바인딩하거나 열 목록의 열의 서수 위치를 결과 집합 이름으로 사용할 수 있습니다. 예를 들어 `SELECT Color FROM Production.Product WHERE ProductID = ?` 쿼리에 대한 결과 집합 이름은 **Color** 또는 **0**일 수 있습니다. 쿼리에서 여러 열을 반환하고 모든 열의 값에 액세스하려는 경우 각 열을 다른 변수에 바인딩해야 합니다. 번호를 결과 집합 이름으로 사용하여 열을 변수에 매핑하면 열이 쿼리의 열 목록에 표시되는 순서가 번호로 적용됩니다. 예를 들어 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`쿼리에서 **Color** 열에 대해 0을 사용하고 **ListPrice** 열에 대해 1을 사용할 수 있습니다. 열 이름을 결과 집합 이름으로 사용하는 기능은 태스크에서 사용하도록 구성된 공급자에 따라 달라집니다. 일부 공급자만 열 이름을 사용할 수 있습니다.  
  
 단일 값을 반환하는 일부 쿼리에는 열 이름이 포함되지 않을 수 있습니다. 예를 들어 `SELECT COUNT (*) FROM Production.Product` 문은 열 이름을 반환하지 않습니다. 서수 위치인 0을 결과 이름으로 사용하여 반환 결과에 액세스할 수 있습니다. 열 이름별로 반환 결과에 액세스하려면 쿼리에 AS \<alias name> 절을 포함하여 열 이름을 제공해야 합니다. 
  `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`문은 **CountOfProduct** 열을 제공합니다. 
  **CountOfProduct** 열 이름 또는 서수 위치 0을 사용하여 반환 결과 열에 액세스할 수 있습니다.  
  
 결과 집합 유형이 **전체 결과 집합** 이나 **XML**이면 결과 집합 이름으로 0을 사용해야 합니다.  
  
 변수를 **단일 행** 결과 집합 유형이 있는 결과 집합에 매핑하면 변수에는 결과 집합이 포함하는 열의 데이터 형식과 호환되는 데이터 형식이 있어야 합니다. 예를 들어 `String` 데이터 형식이 있는 열을 포함하는 결과 집합은 숫자 데이터 형식의 변수에 매핑할 수 없습니다. **TypeConversionMode** 속성을로 `Allowed`설정 하는 경우 SQL 실행 태스크는 출력 매개 변수와 쿼리 결과를 결과가 할당 되는 변수의 데이터 형식으로 변환 하려고 시도 합니다.  
  
 XML 결과 집합은 `String` 또는 `Object` 데이터 형식의 변수에만 매핑할 수 있습니다. 변수에 `String` 데이터 형식이 있는 경우 SQL 실행 태스크는 문자열을 반환하고 XML 원본은 XML 데이터를 사용할 수 있습니다. 변수에 `Object` 데이터 형식이 있는 경우 SQL 실행 태스크는 DOM(문서 개체 모델) 개체를 반환합니다.  
  
 **전체 결과 집합** 은 `Object` 데이터 형식의 변수에 매핑되어야 합니다. 반환 결과는 행 집합 개체입니다. Foreach 루프 컨테이너를 사용하여 개체 변수에 저장된 테이블 행 값을 패키지 변수로 추출한 다음 스크립트 태스크를 사용하여 패키지 변수에 저장된 데이터를 파일에 쓸 수 있습니다. Foreach 루프 컨테이너 및 스크립트 태스크를 사용하여 이러한 작업을 수행하는 방법에 대한 데모는 msftisprodsamples.codeplex.com에서 CodePlex 샘플인 [SQL 매개 변수 및 결과 집합 실행](https://go.microsoft.com/fwlink/?LinkId=157863)(영문)을 참조하세요.  
  
 다음 표에는 결과 집합에 매핑될 수 있는 변수의 데이터 형식이 요약되어 있습니다.  
  
|결과 집합 유형|변수의 데이터 형식|개체 유형|  
|---------------------|---------------------------|--------------------|  
|단일 행|결과 집합의 유형 열과 호환되는 모든 형식|해당 없음|  
|전체 결과 집합|`Object`|태스크에서 ADO, OLE DB, Excel 및 ODBC 연결 관리자를 비롯한 네이티브 연결 관리자를 사용하는 경우 반환되는 개체는 ADO `Recordset`입니다.<br /><br /> 태스크에서 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자와 같이 관리되는 연결 관리자를 사용하는 경우 반환되는 개체는 `System.Data.DataSet`입니다.<br /><br /> 다음 예제에서처럼 스크립트 태스크를 사용하여 `System.Data.DataSet` 개체에 액세스할 수 있습니다.<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|태스크에서 ADO, OLE DB, Excel 및 ODBC 연결 관리자 등의 네이티브 연결 관리자를 사용하는 경우 반환되는 개체는 `MSXML6.IXMLDOMDocument`입니다.<br /><br /> 태스크에서 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 연결 관리자와 같이 관리되는 연결 관리자를 사용하는 경우 반환되는 개체는 `System.Xml.XmlDocument`입니다.|  
  
 변수는 SQL 실행 태스크나 패키지 범위에서 정의할 수 있습니다. 변수 범위가 패키지이면 해당 패키지 내의 다른 태스크와 컨테이너는 물론 패키지 실행 또는 DTS 2000 패키지 실행 태스크가 실행한 모든 패키지에서 결과 집합을 사용할 수 있습니다.  
  
 변수를 **단일 행** 결과 집합에 매핑할 때 SQL 문에서 반환하는 문자열이 아닌 값은 다음 조건을 충족하는 경우 문자열로 변환됩니다.  
  
-   
  **TypeConversionMode** 속성이 True로 설정된 경우. 속성 창 또는 **SQL 실행 태스크 편집기**를 사용하여 속성 값을 설정합니다.  
  
-   변환에서 데이터 잘림이 발생하지 않은 경우  
  
 결과 집합을 변수에 로드하는 방법에 대한 자세한 내용은 [결과 집합을 SQL 실행 태스크의 변수에 매핑](control-flow/execute-sql-task.md)을 참조하세요.  
  
##  <a name="Configure_result_sets"></a>SQL 실행 태스크에서 결과 집합 구성  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 결과 집합 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [SQL 실행 태스크 편집기 &#40;결과 집합 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [결과 집합을 SQL 실행 태스크의 변수에 매핑](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   msftisprodsamples.codeplex.com의 CodePlex 예제 - [SQL 실행 매개 변수 및 결과 집합(Execute SQL Parameters and Result Sets)](https://go.microsoft.com/fwlink/?LinkId=157863)  
  
  
