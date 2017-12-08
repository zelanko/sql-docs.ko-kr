---
title: "DISCOVER_CALC_DEPENDENCY 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0926c2eef3b0b733d9d334a5ed59a96a24826c42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discovercalcdependency-rowset"></a>DISCOVER_CALC_DEPENDENCY 행 집합
  계산 간 종속성과 해당 계산에서 참조하는 개체에 대한 보고서입니다. 클라이언트 응용 프로그램에 이 정보를 사용하여 복잡한 수식과 관련된 문제를 보고하거나 관련 개체가 삭제 또는 수정될 때 경고할 수 있습니다. 행 집합을 사용하여 측정값 또는 계산 열에 사용된 DAX 식을 추출할 수도 있습니다.  
  
 **다음에 적용:** 테이블 형식 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_CALC_DEPENDENCY** 행 집합에는 다음 열이 포함되어 있습니다. 테이블은 데이터 형식을 지정하고, 반환되는 행을 제한하도록 열을 제한할 수 있는지 여부를 나타내며, 각 열에 대한 설명을 제공합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**A S E _**|**DBTYPE_WSTR**|예|종속성 분석이 요청된 개체를 포함하는 데이터베이스 이름을 지정합니다. 생략하는 경우 현재 데이터베이스가 사용됩니다.<br /><br /> 이 열을 사용하여 **DISCOVER_DEPENDENCY_CALC** 행 집합을 제한할 수 있습니다.|  
|**OBJECT_TYPE**|**DBTYPE_WSTR**|예|종속성 분석이 요청된 개체의 유형을 나타냅니다. 개체의 유형은 다음 중 하나여야 합니다.<br /><br /> **ACTIVE_RELATIONSHIP**: 활성 관계<br /><br /> **CALC_COLUMN**: 계산된 열<br /><br /> **HIERARCHY**: 계층<br /><br /> **MEASURE**: 측정값<br /><br /> **RELATIONSHIP**: 관계<br /><br /> **KPI**: KPI(핵심 성과 지표)<br /><br /> <br /><br /> **DISCOVER_DEPENDENCY_CALC** 이 열을 사용 하 여 행 집합을 제한할 수 있습니다.|  
|**쿼리**|**DBTYPE_WSTR**|예|[!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)]에서 만든 테이블 형식 모델의 경우 해당 쿼리 또는 식에 대한 종속성 그래프를 표시하도록 DAX 쿼리 또는 식을 포함할 수 있습니다. QUERY 제한은 DAX 쿼리에 사용되는 개체를 결정하는 방법을 클라이언트 응용 프로그램에 제공합니다.<br /><br /> **QUERY** 제한은 DMV 쿼리의 XMLA 또는 WHERE 절에 지정할 수 있습니다. 자세한 내용은 "예" 섹션을 참조하십시오.|  
|**TABLE**|**DBTYPE_WSTR**||종속성 정보가 생성된 개체를 포함하는 테이블의 이름입니다.|  
|**개체**|**DBTYPE_WSTR**||종속성 정보가 생성된 개체의 이름입니다. 개체가 측정값 또는 계산된 열인 경우 측정값의 이름을 사용합니다. 개체가 관계인 경우 관계에 참가하는 열이 포함된 테이블(또는 큐브 차원)의 이름을 사용합니다.|  
|**식**|**DBTYPE_WSTR**||종속성을 찾는 개체를 포함하는 수식입니다.|  
|**REFERENCED_OBJECT_TYPE**|**DBTYPE_WSTR**||참조된 개체에 종속된 개체의 유형을 반환합니다. 반환된 개체의 유형은 다음 중 하나일 수 있습니다.<br /><br /> **CALC_COLUMN**: 계산된 열<br /><br /> **COLUMN**: 데이터 열<br /><br /> **MEASURE**: 측정값<br /><br /> **RELATIONSHIP**: 관계<br /><br /> **KPI**: KPI(핵심 성과 지표)|  
|**REFERENCED_TABLE**|**DBTYPE_ WSTR**||종속 개체를 포함하는 테이블의 이름입니다.|  
|**REFERENCED_OBJECT**|**DBTYPE_ WSTR**||참조된 개체에 종속된 개체의 이름입니다. 측정값 및 계산된 열인 경우 측정값 또는 열의 이름을 사용합니다. 관계인 경우 종속 개체가 포함된 테이블(또는 큐브 차원)의 정규화된 이름을 사용합니다.|  
|**REFERENCED_EXPRESSION**|**DBTYPE_WSTR**||계산된 열 또는 측정값에 있는 수식 중 참조된 개체에 종속된 수식입니다.|  
  
## <a name="example"></a>예제  
 **기본 구문**  
  
 다음 쿼리는 현재 연결에서 기본 데이터베이스를 사용하여 이 행 집합의 모든 열 값을 반환하는 단순한 DMV 쿼리입니다. MDX 쿼리 창에서 이 쿼리를 실행하고 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 결과를 볼 수 있습니다. 에 설명 된 기술을 따르면 [Excel에서 Power Pivot Dmv 쿼리](http://go.microsoft.com/fwlink/?LinkID=235146) Excel에서 DMV 쿼리 결과 볼 수 있습니다.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>예제  
 **결과 정렬**  
  
 ORDER BY를 추가하여 행 집합을 테이블 또는 다른 열을 기준으로 정렬할 수 있습니다.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>예제  
 **WHERE 절을 사용 하 여 필터링**  
  
 다음 쿼리에서는 WHERE 절을 사용하여 제한을 추가하는 방법을 보여 줍니다. 다음 열을 WHERE 절에 대한 쿼리 필터로 사용할 수 있습니다. **Database_Name**, **Object_Type**, **Query**.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>예제  
 **측정값 및 계산 된 열 기본 DAX 식 보기에 대해 필터링**  
  
 이 쿼리에서는 측정값 또는 계산된 열을 선택하는 작업만으로 계산에 사용된 DAX 식을 볼 수 있습니다. EXPRESSION 열에 DAX 식이 포함되어 있습니다. DISCOVER_CALC_DEPENDENCY를 사용하여 모델에 사용된 DAX 식을 추출하려는 경우에는 이 쿼리만으로 충분합니다. 이 쿼리에서는 모델에 사용된 모든 식을 오름차순으로 반환합니다.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>예제  
 **쿼리를 사용 하 여 필터링**  
  
 QUERY 제한을 통해 DAX 쿼리를 제공하여 해당 쿼리에 사용된 모든 개체를 볼 수 있습니다. 'Evaluate Customer'와 같은 간단한 쿼리를 살펴 보겠습니다. 여기에서 설명한 것과 같이 이 쿼리에서는 고객 데이터 행을 반환하며 여기서 행 컴퍼지션은 Customer 테이블의 열을 기반으로 합니다. 이제 'Evaluate Customer' QUERY 제한을 사용하여 DISCOVER_CALC_DEPENDENCY를 실행하면 해당 쿼리에 사용된 열 또는 개체를 결과로 얻습니다. 이 경우에는 Customer 테이블의 열 목록을 결과로 얻습니다.  
  
 다음 쿼리 집합에서는 QUERY 제한의 구문을 보여 줍니다. [AdventureWorks Tabular Model SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) 에 대해 이 쿼리를 실행하여 결과 집합을 볼 수 있습니다.  
  
 첫 번째 쿼리에서는 공백을 포함하는 개체 이름에 대한 QUERY 제한을 지정하는 방법을 보여 줍니다. The second query, borrowed from [OLE DB 및 ADOMD.NET을 통해 DAX 쿼리 실행](http://go.microsoft.com/fwlink/?LinkId=254329)에서 가져온 두 번째 쿼리는 여러 테이블의 개체를 포함하는 좀 더 복잡한 쿼리입니다.  
  
> [!NOTE]  
>  쿼리에 큰따옴표가 사용되는 것처럼 보이지만 사실은 작은따옴표만 사용됩니다. 한 쌍의 작은따옴표로 묶습니다 ' Evaluate \<Tablename >', 작은 따옴표의 테이블 이름에 사용 되는 이중으로 추가 하 여 이스케이프 해야 합니다. 테이블 이름을 묶는 작은따옴표는 공백이 있는 테이블 이름에만 필요합니다.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>예제  
 **QUERY 제한 XMLA 예제**  
  
 XMLA Discover 명령을 사용하여 테이블의 쿼리 개체를 반환할 수 있습니다. XMLA는 결과를 원시 XML로 반환합니다. ADOMD.NET을 사용하여 결과를 더 읽기 쉬운 형식으로 구문 분석할 수 있습니다.  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [사용 하 여 동적 관리 뷰 &#40; Dmv &#41; Analysis Services를 모니터링 하려면](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
