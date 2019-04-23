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
manager: craigg
ms.openlocfilehash: 61b6f366843b326a8983c27c3d5ee945604756f0
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156270"
---
# <a name="querying-a-tabular-model"></a>테이블 형식 모델 쿼리
  개발자는 테이블 형식 데이터베이스에서 데이터를 검색할 의미 테이블 형식 모델 쿼리 이 목표를 위해 두 가지 옵션이 있습니다: dax에서 테이블 쿼리를 사용 하거나 MDX 및 검색 데이터를 큐브에서 튀어 사용 합니다. 그러나 테이블 형식 모델의 기본 모드에 따라 DAX 테이블 쿼리만 사용하도록 제한될 수 있습니다. DirectQuery 모드를 사용하려면 DAX 테이블 쿼리를 사용해야 합니다.  
  
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
|||$     29,358,677.22|$     80,450,596.98|$   109,809,274.20|  
||Accessories|$           700,759.96|$           571,297.93|$        1,272,057.89|  
||Bikes|$     28,318,144.65|$     66,302,381.56|$     94,620,526.21|  
||Clothing|$           339,772.61|$        1,777,840.84|$        2,117,613.45|  
||구성 요소||$     11,799,076.66|$     11,799,076.66|  
|2001||$        3,266,373.66|$        8,065,435.31|$     11,331,808.96|  
|2001|Accessories||$              20,235.36|$              20,235.36|  
|2001|Bikes|$        3,266,373.66|$        7,395,348.63|$     10,661,722.28|  
|2001|Clothing||$              34,376.34|$              34,376.34|  
|2001|구성 요소||$           615,474.98|$           615,474.98|  
|2002||$        6,530,343.53|$     24,144,429.65|$     30,674,773.18|  
|2002|Accessories||$              92,735.35|$              92,735.35|  
|2002|Bikes|$        6,530,343.53|$     19,956,014.67|$     26,486,358.20|  
|2002|Clothing||$           485,587.15|$           485,587.15|  
|2002|구성 요소||$        3,610,092.47|$        3,610,092.47|  
|2003||$        9,791,060.30|$     32,202,669.43|$     41,993,729.72|  
|2003|Accessories|$           293,709.71|$           296,532.88|$           590,242.59|  
|2003|Bikes|$        9,359,102.62|$     25,551,775.07|$     34,910,877.69|  
|2003|Clothing|$           138,247.97|$           871,864.19|$        1,010,112.16|  
|2003|구성 요소||$        5,482,497.29|$        5,482,497.29|  
|2004||$        9,770,899.74|$     16,038,062.60|$     25,808,962.34|  
|2004|Accessories|$           407,050.25|$           161,794.33|$           568,844.58|  
|2004|Bikes|$        9,162,324.85|$     13,399,243.18|$     22,561,568.03|  
|2004|Clothing|$           201,524.64|$           386,013.16|$           587,537.80|  
|2004|구성 요소||$        2,091,011.92|$        2,091,011.92|  
  
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
|4|4|Accessories|$        700,759.96|$        571,297.93|  
|1|1|Bikes|$  28,318,144.65|$  66,302,381.56|  
|3|3|Clothing|$        339,772.61|$    1,777,840.84|  
|2|2|구성 요소||$  11,799,076.66|  
  
  
