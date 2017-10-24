---
title: "olapR을 사용하여 MDX 쿼리를 만드는 방법 | Microsoft 문서"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: 3
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adcc1c80fdd04cfa3f49b550e5ea5fd8cc34003a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-mdx-queries-using-olapr"></a>olapR을 사용하여 MDX 쿼리를 만드는 방법
## <a name="how-to-build-an-mdx-query-from-r"></a>R에서 MDX 쿼리를 작성하는 방법

1. OLAP 데이터 원본(SSAS 인스턴스) 및 MSOLAP 공급자를 지정하는 연결 문자열을 정의합니다.

2. `OlapConnection(connectionString)` 함수를 사용하여 MDX 쿼리에 대한 핸들을 만들고 연결 문자열을 전달합니다.

3. `Query()` 생성자를 사용하여 쿼리 개체를 인스턴스화합니다.

4. 다음과 같은 도우미 함수를 사용하여 MDX 쿼리에 포함할 차원 및 측정값에 대한 자세한 정보를 제공합니다.
     + `cube()` SSAS 데이터베이스의 이름을 지정합니다.
     + `columns()` ON COLUMNS 인수에서 사용할 측정값의 이름을 제공합니다.  
     + `rows()` ON ROWS 인수에서 사용할 측정값의 이름을 제공합니다.
     + `slicers()` 슬라이서로 사용할 필드 또는 멤버를 지정합니다. 슬라이서는 모든 MDX 쿼리 데이터에 적용되는 필터와 유사합니다.
     
     + `axis()` 쿼리에서 사용할 추가 축의 이름을 지정합니다. OLAP 큐브에는 최대 128개의 쿼리 축이 포함될 수 있습니다. 일반적으로 처음 네 개의 축을 열, 행, 페이지 및 장이라고 합니다. 쿼리가 비교적 단순한 경우 `columns`, `rows`등의 함수를 사용하여 쿼리를 작성할 수 있습니다.     
     그러나 인덱스 값이 0이 아닌 `axis()` 함수를 사용하여 한정자가 많은 MDX 쿼리를 작성하거나 추가 차원을 한정자로 추가할 수도 있습니다.

5. 결과의 형태에 따라 핸들 및 완성된 MDX 쿼리를 `executeMD` 또는 `execute2D`함수에 전달합니다.

  + `executeMD` 다차원 배열을 반환합니다.
  + `execute2D` 2차원(테이블 형식) 데이터 프레임을 반환합니다.


## <a name="how-to-run-an-existing-mdx-query-from-r"></a>R에서 기존 MDX 쿼리를 실행하는 방법

1. OLAP 데이터 원본(SSAS 인스턴스) 및 MSOLAP 공급자를 지정하는 연결 문자열을 정의합니다.

2. `OlapConnection(connectionString)` 함수를 사용하여 MDX 쿼리에 대한 핸들을 만들고 연결 문자열을 전달합니다.

3. R 변수를 정의하여 MDX 쿼리 텍스트를 저장합니다.

4. 결과의 형태에 따라 핸들 및 MDX 쿼리를 포함하는 변수를 `executeMD` 또는 `execute2D`함수에 전달합니다.

    + `executeMD` 다차원 배열을 반환합니다.
    + `execute2D` 2차원(테이블 형식) 데이터 프레임을 반환합니다.



## <a name="examples"></a>예

### <a name="1-basic-mdx-with-slicer"></a>1. 슬라이서가 포함된 기본 MDX

이 MDX 쿼리는 인터넷 판매 개수 및 판매액의 개수 및 금액에 대한 _측정값_을 선택하여 열 축에 배치합니다. SalesTerritory 차원의 멤버를 *슬라이서*로 추가하여 오스트레일리아의 판매만 계산에 사용되도록 쿼리를 필터링합니다.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ 열에서 쉼표로 구분된 문자열의 요소로 여러 측정값을 지정할 수 있습니다.
+ 행 축은 "제품군" 차원의 가능한 모든 값(모든 MEMBERS)을 사용합니다. 
+ 이 쿼리는 모든 국가의 인터넷 판매에 대한 _롤업_ 요약을 포함하며 열이 세 개인 테이블을 반환합니다. 
+ WHERE 절은 _slicer 축_입니다. 슬라이서는 SalesTerritory 차원의 멤버를 사용하여 오스트레일리아의 판매만 계산에 사용되도록 쿼리를 필터링합니다.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>olapR에서 제공하는 함수를 사용하여 이 쿼리를 작성하려면

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>미리 정의된 MDX 문자열로 이 쿼리를 실행하려면

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

SQL Server Management Studio에서 MDX 작성기를 사용하여 쿼리를 정의한 다음 MDX 문자열을 저장하는 경우 다음과 같이 0부터 시작하여 축에 번호를 지정합니다. 

~~~~
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Country].[Australia]
~~~~

미리 정의된 MDX 문자열로 이 쿼리를 실행할 수도 있습니다. 그러나 R에서 `axis()` 함수를 사용하여 동일한 쿼리를 작성하려면 1부터 시작하여 축에 번호를 지정해야 합니다.


### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. SSAS 인스턴스에서 큐브 및 해당 필드 탐색

`explore` 함수를 사용하여 쿼리를 구성하는 데 사용할 큐브, 차원 또는 멤버 목록을 반환할 수 있습니다. 다른 OLAP 검색 도구에 액세스할 수 없는 경우 또는 MDX 쿼리를 프로그래밍 방식으로 조작하거나 구성하려는 경우에 유용합니다.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>지정된 연결에서 사용할 수 있는 큐브를 나열하려면

보기 권한이 있는 인스턴스에서 모든 큐브 또는 큐브 뷰를 보려면 핸들을 `explore`에 대한 인수로 제공합니다.
최종 결과는 큐브가 아닙니다. True는 단순히 메타데이터 작업이 성공했음을 나타냅니다. 인수가 유효하지 않을 경우 오류가 발생합니다.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| 결과  |  
| ----|
| _Analysis Services Tutorial_|
|_Internet Sales_|
|_Reseller Sales_|
|_Sales Summary_|
|_[1] TRUE_|
     


#### <a name="to-get-a-list-of-cube-dimensions"></a>큐브 차원의 목록을 가져오려면

큐브 또는 큐브 뷰의 모든 차원을 보려면 큐브 또는 큐브 뷰 이름을 지정합니다.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| 결과  |  
| ----|
| _Customer_|
|_Date_|
|_Region_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>지정된 차원 및 계층의 모든 멤버를 반환하려면

원본을 정의하고 핸들을 만든 후 반환할 큐브, 차원 및 계층을 지정합니다.
앞에 **->** 접두사가 있는 반환 결과의 항목은 이전 멤버의 자식을 나타냅니다.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| 결과  |  
| ----|
| _Accessories_|
|_Bikes_|
|_Clothing_|
|_Components_|
|-> Assembly Components|
|-> Assembly Components|



## <a name="see-also"></a>관련 항목:

[R에서 OLAP 큐브의 데이터 사용](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md)

