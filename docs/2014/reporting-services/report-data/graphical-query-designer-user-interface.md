---
title: 그래픽 쿼리 디자이너 사용자 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 27b487c787a82f67fc861153939eb5838373fca1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108003"
---
# <a name="graphical-query-designer-user-interface"></a>그래픽 쿼리 디자이너 사용자 인터페이스
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서 디자이너의 보고서 데이터 집합에 대한 관계형 데이터베이스에서 데이터를 검색하기 위해 쿼리를 만들 수 있도록 그래픽 쿼리 디자이너와 텍스트 기반 쿼리 디자이너를 모두 제공합니다. 그래픽 쿼리 디자이너를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Oracle, OLE DB 및 ODBC와 같은 데이터 원본 유형에 대한 쿼리를 대화형으로 작성하고 결과를 볼 수 있습니다. 텍스트 기반 쿼리 디자이너를 사용하면 여러 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문, 복잡한 쿼리 또는 명령 구문 및 식 기반 쿼리를 지정할 수 있습니다. 자세한 내용은 [텍스트 기반 쿼리 디자이너 사용자 인터페이스](../text-based-query-designer-user-interface.md)를 참조하세요. 특정 데이터 원본 유형 작업에 대 한 자세한 내용은 참조 하세요. [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-datasets-ssrs.md)합니다.  
  
 .  
  
## <a name="graphical-query-designer"></a>그래픽 쿼리 디자이너  
 이 그래픽 쿼리 디자이너에서 지원하는 쿼리 명령에는 **Text**, **StoredProcedure**또는 **TableDirect**의 세 가지 유형이 있습니다. 데이터 집합에 대한 쿼리를 만들기 전에 [데이터 집합 속성](../dataset-properties-dialog-box-query.md) 대화 상자의 쿼리 페이지에서 명령 유형 옵션을 선택해야 합니다.  
  
 쿼리 유형에 사용할 수 있는 옵션은 다음과 같습니다.  
  
-   **Text**에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 Oracle용 데이터 처리 확장 프로그램을 비롯한 관계형 데이터베이스 데이터 원본의 표준 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리 텍스트를 지원합니다.  
  
-   **TableDirect** 지정한 테이블에서 모든 열을 선택합니다. 예를 들어 Customers라는 테이블에 대해 이는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 `SELECT * FROM Customers`와 같습니다.  
  
-   **StoredProcedure** 데이터 원본에 대한 저장 프로시저 호출을 지원합니다. 이 옵션을 사용하려면 데이터 원본에 대한 데이터베이스 관리자에게서 저장 프로시저에 대한 실행 권한을 받아야 합니다.  
  
 기본 명령 유형은 **Text**입니다.  
  
> [!NOTE]  
>  모든 데이터 처리 확장 프로그램이 모든 유형을 지원하는 것은 아닙니다. 옵션을 사용할 수 있으려면 기본 데이터 공급자가 명령 유형을 지원해야 합니다.  
  
### <a name="command-type-text"></a>Text 명령 유형  
 **Text** 유형에서는 그래픽 쿼리 디자이너에 4개의 영역 또는 창이 제공됩니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리에 대한 열, 별칭, 정렬 값 및 필터 값을 지정할 수 있으며 선택 항목에서 생성된 쿼리 텍스트를 확인하고 쿼리를 실행하여 결과 집합을 볼 수 있습니다. 다음 그림에서는 4개의 창을 보여 줍니다.  
  
 ![SQL 쿼리를 위한 그래픽 쿼리 디자이너](../media/rsqd-dsaw-sql.gif "SQL 쿼리를 위한 그래픽 쿼리 디자이너")  
  
 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|기능|  
|----------|--------------|  
|다이어그램|쿼리에서 테이블을 그래픽으로 표시합니다. 이 창을 사용하여 필드를 선택하고 테이블 간의 관계를 정의합니다.|  
|표 형태|쿼리에서 반환하는 필드 목록을 표시합니다. 이 창을 사용하여 별칭, 정렬 순서, 필터, 그룹 및 매개 변수를 정의합니다.|  
|SQL|다이어그램 및 표 형태 창에서 나타내는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 표시합니다. 이 창을 통해 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 쿼리를 작성하거나 업데이트합니다.|  
|결과|쿼리 결과를 표시합니다. 쿼리를 실행하려면 아무 창이나 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭하거나 도구 모음에서 **실행** 단추를 클릭합니다.|  
  
 먼저 3개 창 중 하나에서 정보를 변경할 경우 이러한 변경 내용이 다른 창에 표시됩니다. 예를 들어 다이어그램 창에 테이블을 추가하면 SQL 창에서도 자동으로 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리에 테이블이 추가됩니다. SQL 창에서 쿼리에 필드를 추가하면 자동으로 표 형태 창의 목록에 필드가 추가되고 다이어그램 창에서는 테이블이 업데이트됩니다.  
  
 자세한 내용은 [쿼리 및 뷰 디자이너 도구&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)를 참조하세요.  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>그래픽 쿼리 디자이너 도구 모음  
 그래픽 쿼리 디자이너 도구 모음은 그래픽 인터페이스를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 디자인하는 데 도움이 되는 단추를 제공합니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다.|  
|**가져오기**|파일 또는 보고서에서 기존 쿼리를 가져옵니다. 파일 유형 .sql 및 .rdl만 지원됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.|  
|![다이어그램 창 표시/숨기기 토글 단추](../media/rsqdicon-showhidediagram.gif "다이어그램 창 표시/숨기기 토글 단추")|다이어그램 창을 표시하거나 숨깁니다.|  
|![표 형태 창 표시/숨기기 토글](../media/rsqdicon-showhidegrid.gif "표 형태 창 표시/숨기기 토글")|표 형태 창을 표시하거나 숨깁니다.|  
|![SQL 창 표시/숨기기 토글](../media/rsqdicon-showhidesql.gif "SQL 창 표시/숨기기 토글")|SQL 창을 표시하거나 숨깁니다.|  
|![결과 창 표시/숨기기 토글](../media/rsqdicon-showhideresult.gif "결과 창 표시/숨기기 토글")|결과 창을 표시하거나 숨깁니다.|  
|![쿼리 실행](../../analysis-services/media/rsqdicon-run.gif "쿼리 실행")|쿼리를 실행합니다.|  
|![SQL 창의 SQL 검증 단추](../media/rsqdicon-verifysql.gif "SQL 창의 SQL 검증 단추")|쿼리 텍스트의 구문이 올바른지 확인합니다.|  
|![선택한 필드에 대해 오름차순 정렬 설정](../media/rsqdicon-sortascending.gif "선택한 필드에 대해 오름차순 정렬 설정")|다이어그램 창의 선택한 열에 대해 정렬 순서를 **오름차순 정렬** 로 설정합니다.|  
|![선택한 필드에 대해 내림차순 정렬 설정](../media/rsqdicon-sortdescending.gif "선택한 필드에 대해 내림차순 정렬 설정")|다이어그램 창의 선택한 열에 대해 정렬 순서를 **내림차순 정렬** 로 설정합니다.|  
|![선택한 필드에 대한 필터 제거](../media/rsqdicon-removefilter.gif "선택한 필드에 대한 필터 제거")|필터가 있는 것으로 표시된 다이어그램 창에서 선택한 열의 필터를 제거(![선택한 필터 열 옆에 있는 필터 그래픽](../media/rsqdicon-filter.gif "선택한 필터 열 옆에 있는 필터 그래픽"))합니다.|  
|![선택한 필드에 대해 Group By 사용](../media/rsqdicon-usegroupby.gif "선택한 필드에 대해 Group By 사용")|표 형태 창에서 **그룹화 방법** 열을 표시하거나 숨깁니다. **Group By** 토글 단추가 설정된 경우 표 형태 창에 **그룹화 방법** 이라는 추가 열이 나타나며 쿼리에서 선택한 열의 각 값이 기본적으로 **Group By**로 설정되기 때문에 선택한 열이 SQL 텍스트의 Group By 절에 포함됩니다. Group By 사용 단추를 사용하여 SELECT 절의 모든 열을 포함하는 GROUP BY 절을 자동으로 추가할 수 있습니다. SELECT 절에 집계 함수 호출(예: SUM(ColumnName))이 포함된 경우 비집계 열을 결과 집합에 표시하려면 각 열을 GROUP BY 절에 포함합니다.<br /><br /> 결과 창에 표시하려면 쿼리의 각 열에 결과 창에 표시할 값을 계산하는 데 사용할 집계 함수가 정의되어 있거나 SQL 쿼리의 GROUP BY 절에 쿼리의 열이 지정되어야 합니다.|  
|![다이어그램 창에 새 테이블 추가](../media/rsqdicon-addtable.gif "다이어그램 창에 새 테이블 추가")|데이터 원본의 새 테이블을 다이어그램 창에 추가합니다.<br /><br /> **참고** 새 테이블을 추가할 경우 쿼리 디자이너는 데이터 원본의 외래 키 관계와 일치시키려고 시도합니다. 테이블을 추가한 후 테이블 간의 링크로 표시되는 외래 키 관계가 올바른지 확인하십시오.|  
  
#### <a name="example"></a>예제  
 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 데이터베이스 **Person** 테이블에서 성 목록을 반환합니다.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 또한 SQL 창에서 저장 프로시저를 실행할 수 있습니다. 다음 쿼리는 **데이터베이스의** uspGetEmployeeManagers [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 저장 프로시저를 실행합니다.  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>TableDirect 명령 유형  
 **TableDirect** 유형에서 그래픽 쿼리 디자이너는 데이터 원본의 사용 가능한 테이블에 대한 드롭다운 목록과 결과 창을 표시합니다. 테이블을 선택하고 **실행** 단추를 클릭할 경우 해당 테이블의 모든 열이 반환됩니다.  
  
> [!NOTE]  
>  TableDirect 기능은 **OLE DB** 및 **ODBC** 데이터 원본 유형에서만 지원됩니다.  
  
 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|기능|  
|----------|--------------|  
|테이블 드롭다운 목록|데이터 원본의 사용 가능한 모든 테이블을 나열합니다. 저장 프로시저를 활성화하려면 목록에서 선택합니다.|  
|결과|선택한 테이블의 모든 열을 표시합니다. 테이블 쿼리를 실행하려면 도구 모음에서 **실행** 단추를 클릭합니다.|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>TableDirect 명령 유형의 도구 모음 단추  
 그래픽 쿼리 디자이너 도구 모음은 데이터 원본의 테이블에 대한 드롭다운 목록을 제공합니다. 다음 표에서는 각 단추와 해당 기능을 나열합니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다.|  
|**가져오기**|파일 또는 보고서에서 기존 쿼리를 가져옵니다. 파일 유형 .sql 및 .rdl만 지원됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.|  
|![일반 쿼리 디자이너 단추 아이콘](../media/icongenericquerydesigner.gif "일반 쿼리 디자이너 단추 아이콘")|쿼리 텍스트 또는 저장 프로시저 보기를 유지하면서 일반 쿼리 디자이너 및 그래픽 쿼리 디자이너 사이를 전환합니다.|  
|![쿼리 실행](../../analysis-services/media/rsqdicon-run.gif "쿼리 실행")|선택한 테이블의 모든 열을 선택합니다.|  
  
### <a name="command-type-storedprocedure"></a>StoredProcedure 명령 유형  
 **StoredProcedure** 유형에서 그래픽 쿼리 디자이너는 데이터 원본의 사용 가능한 저장 프로시저에 대한 드롭다운 목록과 결과 창을 표시합니다. 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|기능|  
|----------|--------------|  
|저장 프로시저 드롭다운 목록|데이터 원본의 사용 가능한 모든 저장 프로시저를 나열합니다. 저장 프로시저를 활성화하려면 목록에서 선택합니다.|  
|결과|저장 프로시저의 실행 결과를 표시합니다. 선택한 저장 프로시저를 실행하려면 도구 모음에서 **실행** 단추를 클릭합니다.|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>StoredProcedure 명령 유형의 도구 모음 단추  
 그래픽 쿼리 디자이너 도구 모음은 데이터 원본의 저장 프로시저에 대한 드롭다운 목록을 제공합니다. 다음 표에서는 각 단추와 해당 기능을 나열합니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다.|  
|**가져오기**|파일 또는 보고서에서 기존 쿼리를 가져옵니다. 파일 유형 .sql 및 .rdl만 지원됩니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)이라는 데이터 집합이 들어 있습니다.|  
|![쿼리 실행](../../analysis-services/media/rsqdicon-run.gif "쿼리 실행")|선택한 저장 프로시저를 실행합니다.|  
|저장 프로시저 드롭다운 목록|아래쪽 화살표를 클릭하면 데이터 원본의 사용 가능한 저장 프로시저 목록이 표시됩니다. 저장 프로시저를 선택하려면 목록에서 클릭합니다.|  
  
#### <a name="example"></a>예제  
 다음 저장 프로시저는 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 데이터베이스에서 관리자의 명령 체인 목록을 호출합니다. 이 저장 프로시저는 *BusinessEntityID* 를 매개 변수로 허용합니다. 작은 정수를 입력할 수 있습니다.  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>관련 항목  
 [쿼리, 보고서 디자이너 SQL Server Data Tools의 디자인 도구 &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-datasets-ssrs.md)   
 [SQL Server 연결 형식&#40;SSRS&#41;](sql-server-connection-type-ssrs.md)   
 [OLE DB 연결 형식&#40;SSRS&#41;](ole-db-connection-type-ssrs.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-datasets-ssrs.md)   
 [Oracle 연결 형식&#40;SSRS&#41;](oracle-connection-type-ssrs.md)   
 [RSReportDesigner 구성 파일](../report-server/rsreportdesigner-configuration-file.md)   
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
