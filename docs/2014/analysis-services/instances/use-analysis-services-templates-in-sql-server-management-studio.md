---
title: SQL Server Management Studio에서 Analysis Services 템플릿 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 54ad1954-22e2-4628-b334-8fad8e9433b8
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 387d1752c2e2e2a8f6bdc6e48b2d9b9e7952419f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153374"
---
# <a name="use-analysis-services-templates-in-sql-server-management-studio"></a>SQL Server Management Studio에서 Analysis Services 템플릿 사용
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 XMLA 스크립트, DMX 또는 MDX 쿼리를 빠르게 만들고, 큐브 또는 테이블 형식 모델에 KPI를 만들고, 백업 및 복원 작업을 스크립팅하고, 기타 여러 태스크를 수행하는 데 사용할 수 있는 다양한 템플릿을 제공합니다. 템플릿은 **의** 템플릿 탐색기 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 있습니다.  
  
 이 항목에서는 다차원 모델 및 테이블 형식 모델에 사용할 수 있는 템플릿에 대해 설명하고 메타데이터 탐색기와 템플릿 탐색기를 사용하여 MDX 쿼리와 XMLA 문을 작성하는 방법을 보여 주는 예를 제공합니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [Analysis Services 템플릿 열기](#bkmk_usingTE)  
  
 [템플릿을 사용하여 테이블 형식 모델에 MDX 쿼리 작성 및 실행](#BKMK_Building_Queries)  
  
 [템플릿에서 XMLA 스크립트 만들기](#bkmk_backup)  
  
 [XMLA 템플릿을 사용하여 스키마 행 집합 쿼리 생성](#bkmk_schemarowset)  
  
 [Analysis Services 템플릿 참조](#bkmk_Ref)  
  
 이 항목에서 DMX 템플릿은 다루지 않습니다. 템플릿을 사용하여 데이터 마이닝 쿼리를 만드는 방법의 예는 [SQL Server Management Studio에서 DMX 쿼리 만들기](../data-mining/create-a-dmx-query-in-sql-server-management-studio.md) 또는 [템플릿에서 단일 예측 쿼리 만들기](../data-mining/create-a-singleton-prediction-query-from-a-template.md)를 참조하세요.  
  
##  <a name="bkmk_usingTE"></a> Analysis Services 템플릿 열기  
 데이터베이스 엔진 쿼리 및 Analysis Services 쿼리와 명령에 대한 모든 템플릿은 템플릿 탐색기에 있습니다.  
  
 **템플릿 탐색기**를 열려면 **보기** 메뉴에서 템플릿 탐색기를 선택합니다. 그런 다음 큐브 아이콘을 클릭하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 사용할 수 있는 템플릿 목록을 표시합니다.  
  
 ![템플릿 탐색기, Analysis Services에 대 한 필터링](../media/ssas-templateexplorer.gif "템플릿 탐색기, Analysis Services에 대 한 필터링")  
  
 템플릿을 열려면 템플릿 이름을 마우스 오른쪽 단추로 클릭하고 **열기**를 선택하거나 열어 둔 쿼리 창으로 템플릿을 끌어옵니다. 쿼리 창을 연 후 도구 모음이나 쿼리 메뉴에 있는 명령을 사용하여 문을 손쉽게 작성할 수 있습니다.  
  
-   쿼리 구문을 검사하려면 **구문 분석**을 클릭합니다.  
  
-   쿼리를 실행하려면 **실행**을 클릭합니다.  
  
     실행 중인 쿼리를 중지하려면 **쿼리 실행 취소**를 클릭합니다.  
  
-   화면 아래에 있는 **결과** 탭에서 쿼리 결과를 확인합니다.  
  
     반환된 레코드 수, 오류, 쿼리 문 및 쿼리 실행과 관련된 기타 메시지를 보려면 **메시지** 탭으로 전환합니다. 예를 들어 직접 쿼리 모드에서 실행 중인 모델에 대해 DAX 식을 실행하면 xVelocity 메모리 내 분석 엔진(VertiPaq)에서 생성한 Transact-SQL 문이 표시됩니다.  
  
##  <a name="BKMK_Building_Queries"></a> 템플릿을 사용하여 테이블 형식 모델에 MDX 쿼리 작성 및 실행  
 이 예에서는 SQL Server Management Studio에서 테이블 형식 model 데이터베이스를 데이터 원본으로 사용하여 MDX 쿼리를 만드는 방법을 보여 줍니다. 사용 중인 컴퓨터에서 이 예를 재현하려면 [Adventureworks 테이블 형식 모델 샘플 프로젝트를 다운로드](http://go.microsoft.com/fwlink/?LinkId=231183)하십시오.  
  
> [!WARNING]  
>  직접 쿼리 모드에서 배포된 테이블 형식 모델에 대해서는 MDX 쿼리를 사용할 수 없습니다. 그러나 EVALUATE 명령이 포함된 DAX 테이블 쿼리를 사용하여 동일한 쿼리를 보낼 수 있습니다. 자세한 내용은 [DAX 쿼리 매개 변수](https://msdn.microsoft.com/library/gg492200(v=sql.120).aspx)합니다.  
  
#### <a name="create-an-mdx-query-from-a-template"></a>템플릿에서 MDX쿼리 만들기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 쿼리할 테이블 형식 모델이 들어 있는 인스턴스를 엽니다. 데이터베이스 아이콘을 마우스 오른쪽 단추로 클릭하여 **새 쿼리**를 선택한 다음 **MDX**를 선택합니다.  
  
2.  템플릿 탐색기의 Analysis Services 템플릿에서 **MDX**를 연 다음 **쿼리**를 엽니다. **기본 쿼리** 를 쿼리 창으로 끌어옵니다.  
  
3.  **메타데이터 탐색기**에서 다음 필드 및 측정값을 쿼리 템플릿으로 끌어옵니다.  
  
    1.  바꿉니다 \<mdx_set r o w s >와 **[Product Category]. [ Product Category Name]** 합니다.  
  
    2.  바꿉니다 \<column_axis, mdx_set >와 **[Date]. [ Calendar Year]입니다. [Calendar Year]** .  
  
    3.  바꿉니다 \<from_clause, mdx_name > 사용 하 여 **[Internet Sales]** 합니다.  
  
    4.  바꿉니다 \<where_clause, mdx_set >와 **[Measures]. [ Internet Total Sales]** 합니다.  
  
4.  쿼리를 있는 그대로 실행해도 되지만 특정 멤버를 반환하기 위해 함수를 추가하는 등 일부를 변경할 수도 있습니다. 예를 들어 입력 `.members` 후 **[Product Category]. [ Product Category Name]** 합니다. 자세한 내용은 [Using Member Expressions](/sql/mdx/using-member-expressions)을(를) 참조하세요.  
  
##  <a name="bkmk_backup"></a> 템플릿에서 XMLA 스크립트 만들기  
 템플릿 탐색기에 있는 XMLA 명령 템플릿을 사용하면 인스턴스가 다차원 및 데이터 마이닝 모드에 있는지 아니면 테이블 형식 모드에 있는지 관계없이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 모니터링 및 업데이트하는 데 사용할 스크립트를 만들 수 있습니다. **XMLA** 템플릿에는 다음 스크립트 유형에 대한 예제가 포함되어 있습니다.  
  
-   작업 백업, 복원 및 동기화  
  
-   지정된 프로세스 또는 명령 취소  
  
-   개체 처리  
  
-   스키마 행 집합 검색  
  
-   작업, 연결, 트랜잭션, 메모리 및 성능 카운터 등의 서버 상태 모니터링  
  
#### <a name="create-a-backup-command-script-from-a-template"></a>템플릿에서 백업 명령 스크립트 만들기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 쿼리할 데이터베이스가 들어 있는 인스턴스를 엽니다. 데이터베이스 아이콘을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택한 다음 **XMLA**를 선택합니다.  
  
    > [!WARNING]  
    >  제한 목록을 변경하거나 연결 대화 상자에서 데이터베이스를 지정하는 방법으로는 XMLA 쿼리의 컨텍스트를 설정할 수 없습니다. 쿼리할 데이터베이스에서 XMLA 쿼리 창을 열어야 합니다.  
  
2.  끌어서는 `Backup` 빈 쿼리 창에는 템플릿.  
  
3.  내의 텍스트를 두 번 클릭 합니다 \<DatabaseID > 요소입니다.  
  
4.  개체 탐색기에서 백업할 데이터베이스를 선택한 후 DatabaseID 요소를 묶고 있는 대괄호 사이에 끌어다 놓습니다.  
  
5.  내의 텍스트를 두 번 클릭 합니다 \<파일 > 요소입니다. .abf 파일 확장명을 포함하여 백업 파일의 이름을 입력합니다. 기본 백업 위치를 사용하지 않는 경우 전체 파일 경로를 지정합니다. 자세한 내용은 [데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)를 참조하세요.  
  
##  <a name="bkmk_schemarowset"></a> XMLA 템플릿을 사용하여 스키마 행 집합 쿼리 생성  
 **템플릿 탐색기** 에는 스키마 행 집합 쿼리용 템플릿이 하나만 있습니다. 이 템플릿을 사용하려면 필수 요소, 제한으로 사용할 수 있는 열 등 사용하고자 하는 개별 스키마 행 집합의 요구 사항에 대해 잘 알고 있어야 합니다. 자세한 내용은 [Analysis Services 스키마 행 집합](../schema-rowsets/analysis-services-schema-rowsets.md)을 참조하세요.  
  
 대부분의 스키마 행 집합은 간단한 표현을 위해 DMV(동적 관리 뷰)로도 표시된다는 점에 유의하십시오. 해당 DMV를 사용하면 Transact-SQL 구문과 비슷한 구문을 사용하여 스키마 행 집합을 쿼리할 수 있습니다. 예를 들어 다음 쿼리는 동일한 결과를 하나는 XML 형식으로, 다른 하나는 테이블 형식으로 반환합니다. DMV에 대한 자세한 내용은 [DMV&#40;동적 관리 뷰&#41;를 사용하여 Analysis Services 모니터링](use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)을 참조하세요.  
  
 DMV로 사용할 수 있는 모든 스키마 행 집합 목록을 반환하는 DMV  
  
```  
SELECT * FROM $system.DISCOVER_SCHEMA_ROWSETS  
```  
  
 사용할 수 있는 스키마 행 집합 목록을 반환하는 XMLA 명령  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>  
    <Restrictions>  
<RestrictionList>  
</RestrictionList>  
</Restrictions>  
    <Properties>  
<PropertyList>  
   </PropertyList>  
</Properties>  
</Discover>  
```  
  
#### <a name="get-a-list-of-data-sources-for-a-tabular-model-using-a-schema-rowset-query"></a>스키마 행 집합 쿼리를 사용하여 테이블 형식 모델의 데이터 원본 목록 가져오기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 쿼리할 데이터베이스가 들어 있는 인스턴스를 엽니다. 데이터베이스 아이콘을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택한 다음 **XMLA**를 선택합니다.  
  
    > [!WARNING]  
    >  제한 목록을 변경하거나 연결 대화 상자에서 데이터베이스를 지정하는 방법으로는 XMLA 쿼리의 컨텍스트를 설정할 수 없습니다. 쿼리할 데이터베이스에서 XMLA 쿼리 창을 열어야 합니다.  
  
2.  **템플릿 탐색기**를 열고 **스키마 행 집합 검색**템플릿을 비어 있는 쿼리 창으로 끌어옵니다.  
  
3.  템플릿에서 대체 합니다 [RequestType 요소 &#40;XMLA&#41; ](../xmla/xml-elements-properties/type-element-xmla.md) 요소를 다음 텍스트로: `<RequestType>MDSCHEMA_INPUT_DATASOURCES</RequestType>`  
  
4.  **실행**을 클릭합니다.  
  
     예상 결과:  
  
    ```  
    <CATALOG_NAME>AW Internet Sales Tabular Model_ 24715b71-ea74-4828-aefc-d4c12c15db64</CATALOG_NAME>   
    <DATASOURCE_NAME>SqlServer localhost AdventureWorksDW2012</DATASOURCE_NAME>   
    <DATASOURCE_TYPE>Relational</DATASOURCE_TYPE>   
    <CREATED_ON>2011-10-12T20:27:05.196667</CREATED_ON>   
    <LAST_SCHEMA_UPDATE>2011-10-12T20:27:05.196667</LAST_SCHEMA_UPDATE>   
    <DESCRIPTION />   
    <TIMEOUT>0</TIMEOUT>   
    <DBMS_NAME>Microsoft SQL Server</DBMS_NAME>   
    <DBMS_VERSION>11.00.1724</DBMS_VERSION>  
  
    ```  
  
##  <a name="bkmk_Ref"></a> Analysis Services 템플릿 참조  
 다음은 마이닝 구조와 마이닝 모델, 큐브, 테이블 형식 모델 등 데이터베이스 내의 Analysis Services 데이터베이스 및 개체로 작업할 수 있도록 제공되는 템플릿입니다.  
  
|범주|항목 템플릿|Description|  
|--------------|-------------------|-----------------|  
|DMX\Model Content|Content Query|DMX SELECT FROM 사용 하는 방법을 보여 줍니다  *\<모델 >* 합니다. 지정한 마이닝 모델에 대 한 마이닝 모델 스키마 행 집합 콘텐츠를 검색 하려면 콘텐츠 문입니다.|  
||Continuous Column Values|DMX SELECT DISTINCT FROM 사용 하는 방법을 보여 줍니다  *\<모델 >* DMX 사용 하 여 문을 `RangeMin` 고 `RangeMax` 의 연속 열에서 지정 된 범위의 값 집합을 검색 하는 함수는 지정한 마이닝 모델입니다.|  
||Discrete Column Values|DMX SELECT DISTINCT FROM 사용 하는 방법을 보여 줍니다  *\<모델 >* 문을 지정한 마이닝 모델의 불연속 열에서 값의 전체 집합을 검색 합니다.|  
||Drillthrough Query|DMX SELECT * FROM Model.CASES 문에 DMX IsInNode 함수를 사용하여 드릴스루 쿼리를 수행하는 방법을 보여 줍니다.|  
||Model Attributes|DMX System.GetModelAttributes 함수를 사용하여 모델에 사용되는 특성 목록을 반환하는 방법을 보여 줍니다.|  
||PMML Content|DMX SELECT를 사용 하는 방법을 보여 줍니다 \* FROM  *\<모델 >* 합니다. 이 기능을 지 원하는 알고리즘에 대 한 마이닝 모델의 PMML Predictive Model Markup Language () 표현을 검색 PMML 문입니다.|  
|DMX\Model Management|Add Model|DMX ALTER MINING MODEL STRUCTURE 문을 사용하여 마이닝 모델을 추가하는 방법을 보여 줍니다.|  
||Clear Model|DMX DELETE * FROM MINING MODEL 문을 사용하여 지정한 마이닝 모델의 콘텐츠를 삭제하는 방법을 보여 줍니다.|  
||Clear Structure Cases|DMX DELETE FROM MINING STRUCTURE 문을 사용하여 마이닝 모델 구조 사례를 지우는 방법을 보여 줍니다.|  
||Clear Structure|DMX DELETE FROM MINING STRUCTURE 문을 사용하여 마이닝 모델 구조를 지우는 방법을 보여 줍니다.|  
||Create from PMML|FROM PMML 절과 함께 DMX CREATE MINING MODEL 문을 사용하여 PMML 표현에서 마이닝 모델을 만드는 방법을 보여 줍니다.|  
||Create Structure Nested|DMX CREATE MINING STRUCTURE 문에 중첩 열 정의 목록을 사용하여 중첩 열이 있는 마이닝 모델을 만드는 방법을 보여 줍니다.|  
||Create Structure|DMX CREATE MINING STRUCTURE 문을 사용하여 마이닝 모델을 만드는 방법을 보여 줍니다.|  
||Drop Model|DMX DROP MINING MODEL 문을 사용하여 기존 마이닝 모델을 삭제하는 방법을 보여 줍니다.|  
||Drop Structure|DMX DROP MINING STRUCTURE 문을 사용하여 기존 마이닝 구조를 삭제하는 방법을 보여 줍니다.|  
||Export Model|DMX EXPORT MINING MODEL 문에 WITH DEPENDENCIES 및 PASSWORD 절을 사용하여 마이닝 모델이 종속된 데이터 원본과 데이터 원본 뷰를 포함하여 마이닝 모델을 파일로 내보내는 방법을 보여 줍니다.|  
||Export Structure|DMX EXPORT MINING STRUCTURE 문에 WITH DEPENDENCIES 절을 사용하여 마이닝 구조에 포함된 모든 마이닝 모델 및 마이닝 구조가 종속된 데이터 원본과 데이터 원본 뷰를 포함하여 마이닝 구조를 파일로 내보내는 방법을 보여 줍니다.|  
||가져오기|DMX IMPORT FROM 문에 WITH PASSWORD 절을 사용하여 가져오기를 수행하는 방법을 보여 줍니다.|  
||Rename Model|DMX RENAME MINING MODEL 문을 사용하여 기존 마이닝 모델의 이름을 바꾸는 방법을 보여 줍니다.|  
||Rename Structure|DMX DROP MINING STRUCTRE 문을 사용하여 기존 마이닝 구조를 삭제하는 방법을 보여 줍니다.|  
||Train Model|DMX INSERT INTO MINING MODEL 문을 사용하여 이전에 성향이 습득된 구조 내의 마이닝 모델 성향을 습득하는 방법을 보여 줍니다.|  
||Train Nested Structure|DMX INSERT INTO MINING STRUCTURE 문을 SHAPE 원본 데이터 쿼리와 결합하여 기존 데이터 원본에서 쿼리를 사용하여 검색한 중첩 테이블이 포함된 데이터가 있는 중첩 열을 포함하는 마이닝 모델의 성향을 습득하는 방법을 보여 줍니다.|  
||Train Structure|DMX INSERT INTO MINING STRUCTURE 문을 OPENQUERY 원본 데이터 쿼리와 결합하여 마이닝 구조의 성향을 습득하는 방법을 보여 줍니다.|  
|DMX\Prediction Queries|Base Prediction|DMX SELECT FROM 결합 하는 방법을 보여 줍니다  *\<모델 >* PREDICTION JOIN 문을 OPENQUERY 원본 데이터 쿼리와에서 쿼리를 사용 하 여 검색 한 데이터를 사용 하 여 마이닝 모델에 대해 예측 쿼리를 실행 하는 기존 데이터 원본입니다.|  
||Nested Prediction|DMX SELECT FROM 결합 하는 방법을 보여 줍니다  *\<모델 >* PREDICTION JOIN 문을 SHAPE 및 OPENQUERY 원본 데이터 쿼리와 중첩 된 포함 된 데이터를 사용 하 여 마이닝 모델에 대해 예측 쿼리를 실행 하려면 쿼리를 사용 하 여 기존 데이터 원본에서 검색할 테이블입니다.|  
||Nested Singleton Prediction|DMX SELECT FROM 사용 하는 방법을 보여 줍니다  *\<모델 >* 예측 쿼리에서 열에 명시적으로 지정 된 단일 값을 사용 하 여 마이닝 모델에 대해 예측 쿼리를 실행 하려면 NATURAL PREDICTION JOIN 절 와 이름이 같은 마이닝 모델의 열 이름과 일치 하는 마이닝 모델의 중첩 열 UNION 문을 사용 하 여 만든 중첩된 테이블의 값 집합 포함 되어 있습니다.|  
||Singleton Prediction|DMX SELECT FROM 사용 하는 방법을 보여 줍니다 \<모델 > NATURAL PREDICTION JOIN 문을 예측 쿼리에서 열에 일치 하는 열에 명시적으로 지정 된 단일 값을 사용 하 여 마이닝 모델에 대해 예측 쿼리를 실행 하려면 마이닝 모델입니다.|  
||Stored Procedure Call|DMX CALL 문을 사용하여 저장 프로시저를 호출하는 방법을 보여 줍니다.|  
|MDX\Expressions|Moving Average-Fixed|MDX를 사용 하는 방법을 보여 줍니다 `ParallelPeriod` 고 `CurrentMember` 고정된 된 수의 시간 차원에서 계층에 포함 된 기간 동안의 측정값 이동 평균을 제공 하는 계산된 측정값을 만드는 일반적인 순서로 정렬 된 집합을 사용 하는 함수입니다.|  
||Moving Average-Variable|MDX를 사용 하는 방법을 보여 줍니다 `CASE` 내에 있는 문의 `Avg` 다양 한 시간 차원의 계층에에서 포함 된 기간 동안의 측정값 이동 평균을 제공 하는 계산된 측정값을 만드는 함수입니다.|  
||Periods to Date|계산 멤버에서 MDX `PeriodsToDate` 함수를 사용하는 방법을 보여 줍니다.|  
||Ratio to Parent|MDX를 사용 하는 방법을 보여 줍니다 `Parent` 지정한 계층에서 부모 멤버의 각 자식에 대 한 측정값의 비율을 나타내는 계산된 측정값을 만드는 함수입니다.|  
||Ratio to Total|All 멤버를 사용하여 지정한 계층에 있는 각 멤버에 대한 측정값의 비율을 나타내는 계산 측정값을 만드는 방법을 보여 줍니다.|  
|MDX\Queries|기본 쿼리|MDX 쿼리 생성에 사용할 수 있는 기본 MDX SELECT 문을 보여 줍니다.|  
||KPI Query|MDX를 사용 하는 방법을 보여 줍니다 `KPIValue` 및 `KPIGoal` 함수를 MDX 쿼리에서 핵심 성과 지표 (KPI) 정보를 검색 합니다.|  
||Sub-select Query|다른 SELECT 문으로 정의한 하위 큐브에서 정보를 검색하는 MDX SELECT 문을 만드는 방법을 보여 줍니다.|  
||With Calculated Member|SELECT 문에 MDX WITH 절을 사용하여 MDX 쿼리에 대한 계산 멤버를 정의하는 방법을 보여 줍니다.|  
||With Named Set|SELECT 문에 MDX WITH 절을 사용하여 MDX 쿼리에 대한 명명된 집합을 정의하는 방법을 보여 줍니다.|  
|XMLA\Management|백업|XMLA를 사용 하는 방법을 보여 줍니다 `Backup` 명령을 백업 하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 파일에 있습니다.|  
||취소|XMLA를 사용 하는 방법을 보여 줍니다 `Cancel` 명령을 (관리자 또는 서버 관리자 이외의 사용자 인 경우)에 대 한 현재 세션에서 실행 중인 모든 작업 취소, 데이터베이스 (관리자 인 경우) 또는 인스턴스 (서버 관리자 용입니다.)|  
||Create Remote Partition Database|ASSL([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) 데이터베이스 요소와 함께 XMLA `Create` 명령을 사용하여 원격 파티션 저장을 위한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 및 데이터 원본을 만드는 방법을 보여 줍니다.|  
||DELETE|XMLA를 사용 하는 방법을 보여 줍니다 `Delete` 기존 삭제 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다.|  
||Process Dimension|XMLA `Batch` 명령을 `Parallel` 요소 및 `Process` 명령과 결합하고 병렬 일괄 처리 작업을 사용하여 차원 특성을 업데이트하는 방법을 보여 줍니다.|  
||Process Partition|XMLA를 사용 하는 방법을 보여 줍니다 `Batch` 명령과 결합 하 고는 `Parallel` 요소 및 `Process` 명령을 병렬 일괄 처리 작업을 사용 하 여 파티션을 완전히 처리 합니다.|  
||복원|XMLA를 사용 하는 방법을 보여 줍니다 `Restore` 복원 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기존 백업 파일에서 데이터베이스입니다.|  
||동기화|XMLA를 사용 하는 방법을 보여 줍니다 `Synchronize` 다른 동기화 하는 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] SkipMembership 옵션을 사용 하 여 SynchronizeSecurity 태그에 대 한 데이터베이스입니다.|  
|XMLA\Schema Rowsets|스키마 행 집합 검색|XMLA `Discover` 메서드를 사용하여 DISCOVER_SCHEMA_ROWSETS 스키마 행 집합의 콘텐츠를 검색하는 방법을 보여 줍니다.|  
|XMLA\Server Status|Connections|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` DISCOVER_CONNECTIONS 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
||에서|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` DISCOVER_JOBS 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
||위치|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` 위치 백업 파일의 경로 지정 하며 DISCOVER_LOCATIONS 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
||잠금|XMLA `Discover` 메서드를 사용하여 DISCOVER_LOCKS 스키마 행 집합의 콘텐츠를 검색하는 방법을 보여 줍니다.|  
||Memory Grant|XMLA `Discover` 메서드를 사용하여 DISCOVER_MEMORYGRANT 스키마 행 집합의 콘텐츠를 검색하는 방법을 보여 줍니다.|  
||성능 카운터|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` DISCOVER_PERFORMANCE_COUNTERS 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
||세션|XMLA `Discover` 메서드를 사용하여 DISCOVER_SESSIONS 스키마 행 집합의 콘텐츠를 검색하는 방법을 보여 줍니다.|  
||Traces|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` DISCOVER_TRACES 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
||트랜잭션|XMLA를 사용 하는 방법을 보여 줍니다 `Discover` DISCOVER_TRANSACTIONS 스키마 행 집합의 콘텐츠를 검색 하는 방법입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Multidimensional Expression &#40;MDX&#41; 참조](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services Scripting Language &#40;ASSL&#41; 참조](../scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Analysis Services Scripting Language &#40;ASSL&#41; 참조](../scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
  
