---
title: 텍스트 기반 쿼리 디자이너 사용자 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36805b803d52652d0b072f6124eb2f90cf9617c9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085743"
---
# <a name="text-based-query-designer-user-interface"></a>텍스트 기반 쿼리 디자이너 사용자 인터페이스
  텍스트 기반 쿼리 디자이너에서 데이터 원본에서 지원하는 쿼리 언어를 사용하여 쿼리를 지정하고, 쿼리를 실행하고, 디자인 타임에 결과를 볼 수 있습니다. 여러 개의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 사용자 지정 데이터 처리 확장 프로그램에 대한 쿼리 또는 명령 구문, 식으로 지정된 쿼리를 지정할 수 있습니다. 텍스트 기반 쿼리 디자이너는 쿼리를 전처리하지 않고 모든 종류의 쿼리 구문을 포함할 수 있으므로 많은 데이터 원본 유형에 대한 기본 쿼리 디자이너 도구입니다.  
  
 텍스트 기반 쿼리 디자이너에서는 도구 모음과 다음과 같은 두 개의 창이 표시됩니다.  
  
-   **쿼리** 쿼리 텍스트, 테이블 이름 또는 저장된 프로시저 이름을 표시 합니다.  
  
-   **결과** 디자인 타임에 쿼리 실행 결과를 표시합니다.  
  
## <a name="text-based-query-designer-toolbar"></a>텍스트 기반 쿼리 디자이너 도구 모음  
 텍스트 쿼리 디자이너는 모든 명령 유형을 위한 단일 도구 모음을 제공합니다. 다음 표에서는 도구 모음에 있는 각 단추와 해당 기능을 나열합니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다. 모든 데이터 원본 유형에서 그래픽 쿼리 디자이너를 지원하는 것은 아닙니다.|  
|**가져오기**|파일 또는 보고서에서 기존 쿼리를 가져옵니다. 파일 유형 sql 및 rdl만 지원됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.|  
|![쿼리 실행](../analysis-services/media/rsqdicon-run.gif "쿼리 실행")|쿼리를 실행하고 결과 창에 결과 집합을 표시합니다.|  
|**명령 유형**|**Text**, **StoredProcedure**또는 **TableDirect**를 선택합니다. 저장 프로시저에 매개 변수가 있을 경우 도구 모음에서 **실행** 을 클릭하면 **쿼리 매개 변수 정의** 대화 상자가 표시되며 필요에 따라 값을 입력할 수 있습니다. 저장된 프로시저에서 둘 이상의 결과 집합을 반환 하는 경우 첫 번째 결과 집합만 데이터 집합을 채우는 데 사용 된다는 note 합니다.<br /><br /> 명령 유형에 대한 지원은 데이터 원본 유형에 따라 달라집니다. 예를 들어 OLE DB 및 ODBC의 경우에만 **TableDirect**를 지원합니다.|  
  
### <a name="command-type-text"></a>Text 명령 유형  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 집합을 만들 때 기본적으로 보고서 디자이너에는 그래픽 쿼리 디자이너가 표시됩니다. 텍스트 기반 쿼리 디자이너로 전환하려면 도구 모음에서 **텍스트로 편집** 토글 단추를 클릭합니다. 텍스트 기반 쿼리 디자이너에는 쿼리 창 및 결과 창이 제공됩니다. 다음 그림에서는 레이블과 함께 각 창을 보여 줍니다.  
  
 ![관계형 데이터 쿼리를 위한 일반 쿼리 디자이너](../analysis-services/media/rsqd-dsaw-sql-generic.gif "관계형 데이터 쿼리를 위한 일반 쿼리 디자이너")  
  
 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|기능|  
|----------|--------------|  
|쿼리|[!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리 텍스트를 표시합니다. 이 창을 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리를 작성하거나 편집할 수 있습니다.|  
|결과|쿼리 결과를 표시합니다. 쿼리를 실행하려면 아무 창이나 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭하거나 도구 모음에서 **실행** 단추를 클릭합니다.|  
  
#### <a name="example"></a>예제  
 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스 `Contact` 테이블에서 성 목록을 반환합니다.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 `EXEC` 문을 비롯하여 Text 명령 유형에 대한 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용할 수 있습니다. 다음 호출을 쿼리 합니다 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 저장 프로시저 `uspGetEmployeeManagers` id 번호가 1 인 직원에 대 한 명령 체인을 반환 합니다.  
  
```  
EXEC uspGetEmployeeManagers 1;  
```  
  
 도구 모음에서 **실행** 을 클릭할 경우 **쿼리** 창의 명령이 실행되고 **결과** 창에 결과가 표시됩니다.  
  
### <a name="command-type-storedprocedure"></a>StoredProcedure 명령 유형  
 **명령 typeStoredProcedure**를 선택하면 텍스트 기반 쿼리 디자이너에 쿼리 창 및 결과 창이 제공됩니다. 쿼리 창에 저장 프로시저 이름을 입력하고 도구 모음에서 **실행** 을 클릭합니다. 쿼리 매개 변수 정의 대화 상자가 열립니다. 저장 프로시저에 대한 매개 변수 값을 입력합니다. 모든 저장 프로시저 매개 변수에 대해 보고서 매개 변수가 생성됩니다.  
  
#### <a name="example"></a>예제  
 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 저장 프로시저 `uspGetEmployeeManagers`를 호출합니다. 쿼리를 실행할 때 직원 ID 번호 매개 변수에 대한 값을 입력해야 합니다.  
  
```  
uspGetEmployeeManagers;  
```  
  
### <a name="command-type-tabledirect"></a>TableDirect 명령 유형  
 **명령 typeTableDirect**를 선택하면 텍스트 기반 쿼리 디자이너에 쿼리 창 및 결과 창이 제공됩니다. 테이블을 입력하고 **실행** 단추를 클릭할 경우 해당 테이블의 모든 열이 반환됩니다.  
  
#### <a name="example"></a>예제  
 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 모든 고객에 대한 결과 집합을 반환합니다.  
  
 `Sales.Customer`  
  
 테이블 이름 Sales.Customer를 입력 하면 경우에 생성 합니다 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 `SELECT * FROM Sales.Customer;`합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리, 보고서 디자이너 SQL Server Data Tools의 디자인 도구 &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [SQL Server 연결 형식&#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [OLE DB 연결 형식&#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md)   
 [ODBC 연결 형식 &#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md)   
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [RSReportDesigner 구성 파일](report-server/rsreportdesigner-configuration-file.md)  
  
  
