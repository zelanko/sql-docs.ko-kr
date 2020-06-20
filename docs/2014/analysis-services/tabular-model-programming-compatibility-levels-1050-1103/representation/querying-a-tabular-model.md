---
title: 테이블 형식 모델 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: b01d45d9-4598-4ded-9a9e-e3419cc3df8e
author: minewiskan
ms.author: owend
ms.openlocfilehash: aa42e1125629ddef24e4815a2b1ed89283912832
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940074"
---
# <a name="querying-a-tabular-model"></a>테이블 형식 모델 쿼리
  테이블 형식 모델을 쿼리 하는 개발자는 테이블 형식 데이터베이스에서 데이터를 검색 하는 것을 의미 합니다. 이 목표를 달성 하기 위해 DAX에서 테이블 쿼리를 사용 하거나 MDX를 사용 하 고 큐브에서 들어오는 데이터를 검색 하는 두 가지 옵션이 있습니다. 그러나 테이블 형식 모델의 기본 모드에 따라 DAX 테이블 쿼리만 사용하도록 제한될 수 있습니다. DirectQuery 모드를 사용하려면 DAX 테이블 쿼리를 사용해야 합니다.  
  
## <a name="querying-with-adomdnet"></a>ADOMD.Net을 사용하여 쿼리  
 ADOMD.Net을 사용하여 테이블 형식 모델을 쿼리하는 작업은 단순하고 유연합니다. DAX의 테이블 형식 쿼리 식 또는 MDX 문을 서버로 보내 결과를 가져올 수 있습니다.  
  
 다음 코드에서는 쿼리 문을 테이블 형식 모델에 전달하고 결과를 받는 방법을 보여 줍니다.  
  
```csharp  
//Function: tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
//   - arg: qry, the tabular query or MDX expression to be evaluated  
//   - arg: cnx, an active and opened ADOMD connection to the database where 'qry' is to be evaluated  
//  
// This function takes a query or mdx expression -qry-, a connection -cnx-  
// and runs the query it against a Tabular Model using ADOMD.net  
//  
// Important note:  
//    If the MDX query contains more than 2 axes (ON COLUMNS, ON ROWS), each axis will come as a new column  
//    If the (All) value of the members in any axis have not been defined, a blank cell is returned. This might be misleading  
//    if the model also has missing values... which are also represented with blank cells.  
private DataTable tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
{  
    ADOMD.AdomdDataAdapter currentDataAdapter = new ADOMD.AdomdDataAdapter(qry, cnx);  
    DataTable tabularResults = new DataTable();  
    currentDataAdapter.Fill(tabularResults);  
    return tabularResults;  
}  
  
```  
  
### <a name="example"></a>예제  
 위의 코드를 다음 MDX 식에 사용하는 경우:  
  
```  
SELECT { [Measures].[Internet Total Sales], [Measures].[Reseller Total Sales], [Measures].[Total Sales] } ON COLUMNS  
     , NON EMPTY [Product Category].[Product Category Name].MEMBERS ON ROWS "  
     , NON EMPTY [Date].[Calendar Year].members ON 2 \n"  
FROM [Model]  
  
```  
  
 샘플 모델 'Adventure Works DW Tabular Denali CTP3'의 경우에는 다음 값을 결과 테이블로 받아야 합니다.  
  
|Calendar Year|Product Category 이름|Internet Total Sales|Reseller Total Sales|Total Sales|  
|-------------------|---------------------------|--------------------------|--------------------------|-----------------|  
|||$29358677.22|$80450596.98|$109809274.20|  
||액세서리|$700759.96|$571297.93|$1272057.89|  
||자전거|$28318144.65|$66302381.56|$94620526.21|  
||의류|$339772.61|$1777840.84|$2117613.45|  
||구성 요소||$11799076.66|$11799076.66|  
|2001||$3266373.66|$8065435.31|$11331808.96|  
|2001|액세서리||$20235.36|$20235.36|  
|2001|자전거|$3266373.66|$7395348.63|$10661722.28|  
|2001|의류||$34376.34|$34376.34|  
|2001|구성 요소||$615474.98|$615474.98|  
|2002||$6530343.53|$24144429.65|$30674773.18|  
|2002|액세서리||$92735.35|$92735.35|  
|2002|자전거|$6530343.53|$19956014.67|$26486358.20|  
|2002|의류||$485587.15|$485587.15|  
|2002|구성 요소||$3610092.47|$3610092.47|  
|2003||$9791060.30|$32202669.43|$41993729.72|  
|2003|액세서리|$293709.71|$296532.88|$590242.59|  
|2003|자전거|$9359102.62|$25551775.07|$34910877.69|  
|2003|의류|$138247.97|$871864.19|$1010112.16|  
|2003|구성 요소||$5482497.29|$5482497.29|  
|2004||$9770899.74|$16038062.60|$25808962.34|  
|2004|액세서리|$407050.25|$161794.33|$568844.58|  
|2004|자전거|$9162324.85|$13399243.18|$22561568.03|  
|2004|의류|$201524.64|$386013.16|$587537.80|  
|2004|구성 요소||$2091011.92|$2091011.92|  
  
 MDX 식이 이 DAX 테이블 쿼리 식으로 바뀐 경우:  
  
```  
DEFINE  
   MEASURE 'Product Category'[Internet Sales] = SUM( 'Internet Sales'[Sales Amount])  
   MEASURE 'Product Category'[Reseller Sales] = SUM('Reseller Sales'[Sales Amount]) \n"  
   EVALUATE ADDCOLUMNS('Product Category', \"Internet Sales - All Years\", 'Product Category'[Internet Sales], \"Reseller Sales - All Years\", 'Product Category'[Reseller Sales])  
  
```  
  
 그리고 위의 샘플 모델 'Adventure Works DW Tabular Denali CTP3'에 대해 위의 샘플 코드를 사용하여 서버로 보내면 다음 값을 결과 테이블로 받아야 합니다.  
  
|Product Category Id|Product Category Alternate Id|Product Category 이름|Internet Sales|Reseller Sales|  
|-------------------------|-----------------------------------|---------------------------|--------------------|--------------------|  
|4|4|액세서리|$700759.96|$571297.93|  
|1|1|자전거|$28318144.65|$66302381.56|  
|3|3|의류|$339772.61|$1777840.84|  
|2|2|구성 요소||$11799076.66|  
  
  
