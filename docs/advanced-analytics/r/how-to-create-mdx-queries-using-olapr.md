---
title: OlapR를 사용 하 여 SQL Server 기계 학습의 R에서 쿼리를 MDX를 만드는 방법 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76602c41fd6f8d300c240a6072f2a6decec18e3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203595"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>OlapR를 사용 하 여 R에서 MDX 쿼리를 작성 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) 패키지 SQL Server Analysis Services에서 호스트 되는 큐브에 대해 MDX 쿼리를 지원 합니다. 기존 큐브에 대 한 쿼리를 작성 하 고, 차원 및 기타 큐브 개체를 탐색 하 고, 데이터를 검색 하는 기존 MDX 쿼리에 붙여 넣는 수 있습니다.

설명의 두 가지 주요 용도 **olapR** 패키지:

+ [R을 olapR 패키지에서 제공 하는 생성자를 사용 하 여 MDX 쿼리를 작성합니다](#buildMDX)
+ [OlapR와 OLAP 공급자를 사용 하 여 기존, 유효한 MDX 쿼리를 실행 합니다.](#executeMDX)

다음 작업이 지원 되지 않습니다.

+ 테이블 형식 모델에 대 한 DAX 쿼리
+ 새 OLAP 개체 만들기
+ 측정값 또는 합계를 포함 하 여 파티션 쓰기 저장이 가능한

## <a name="buildMDX"></a> R에서 MDX 쿼리 작성

1. OLAP 데이터 원본(SSAS 인스턴스) 및 MSOLAP 공급자를 지정하는 연결 문자열을 정의합니다.

2. `OlapConnection(connectionString)` 함수를 사용하여 MDX 쿼리에 대한 핸들을 만들고 연결 문자열을 전달합니다.

3. `Query()` 생성자를 사용하여 쿼리 개체를 인스턴스화합니다.

4. 다음과 같은 도우미 함수를 사용하여 MDX 쿼리에 포함할 차원 및 측정값에 대한 자세한 정보를 제공합니다.

     + `cube()` SSAS 데이터베이스의 이름을 지정합니다. 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름과 인스턴스 이름을 제공 합니다. 
     + `columns()` 사용할 측정값의 이름을 제공는 **ON COLUMNS** 인수입니다.
     + `rows()` 사용할 측정값의 이름을 제공는 **ON 행** 인수입니다.
     + `slicers()` 슬라이서로 사용할 필드 또는 멤버를 지정합니다. 슬라이서는 모든 MDX 쿼리 데이터에 적용되는 필터와 유사합니다.
     
     + `axis()` 쿼리에서 사용할 추가 축의 이름을 지정합니다. 
     
         OLAP 큐브에는 최대 128개의 쿼리 축이 포함될 수 있습니다. 일반적으로 처음 네 개의 축 라고 **열**, **행**, **페이지**, 및 **장**합니다. 
         
         쿼리가 비교적 단순한 경우 `columns`, `rows`등의 함수를 사용하여 쿼리를 작성할 수 있습니다. 그러나 인덱스 값이 0이 아닌 `axis()` 함수를 사용하여 한정자가 많은 MDX 쿼리를 작성하거나 추가 차원을 한정자로 추가할 수도 있습니다.

5. 다음 함수는 결과의 형태에 따라 중 하나로 핸들과 완료 된 MDX 쿼리를 전달 합니다. 

  + `executeMD` 다차원 배열을 반환합니다.
  + `execute2D` 2차원(테이블 형식) 데이터 프레임을 반환합니다.

## <a name="executeMDX"></a> R에서 유효한 MDX 쿼리를 실행 합니다.

1. OLAP 데이터 원본(SSAS 인스턴스) 및 MSOLAP 공급자를 지정하는 연결 문자열을 정의합니다.

2. `OlapConnection(connectionString)` 함수를 사용하여 MDX 쿼리에 대한 핸들을 만들고 연결 문자열을 전달합니다.

3. R 변수를 정의하여 MDX 쿼리 텍스트를 저장합니다.

4. 결과의 형태에 따라 핸들 및 MDX 쿼리를 포함하는 변수를 `executeMD` 또는 `execute2D`함수에 전달합니다.

    + `executeMD` 다차원 배열을 반환합니다.
    + `execute2D` 2차원(테이블 형식) 데이터 프레임을 반환합니다.

## <a name="examples"></a>예

다음 예제는 해당 프로젝트는 Analysis Services에 쉽게 복원할 수 있는 백업 파일을 포함 하 여 여러 버전에서 광범위 하 게 사용할 수 있으므로 AdventureWorks 데이터 마트 및 큐브 프로젝트 기반 합니다. 기존 큐브를 설정 하지 않은 경우 이러한 옵션 중 하나를 사용 하 여 예제 큐브를 가져옵니다.

+ 4 단원까지 Analysis Services 자습서에 따라 이러한 예에서 사용 되는 큐브를 만들기: [OLAP 큐브 만들기](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)

+ 백업으로 기존 큐브를 다운로드 하 고 Analysis Services의 인스턴스로 복원 합니다. 이 사이트는 압축 된 형식에서 완전히 처리 된 큐브를 제공 하는 예를 들어: [Adventure Works 다차원 모델 SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)합니다. 파일을 추출한 다음 SSAS 인스턴스에 복원 합니다. 자세한 내용은 참조 [백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md), 또는 [Restore-asdatabase 등이 Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)합니다.

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
+ 이 쿼리는 포함 하는 세 개의 열이 있는 테이블을 반환 된 _롤업_ 모든 국가의 인터넷 판매 부문의 요약 합니다.
+ WHERE 절은 지정 된 _slicer 축_합니다. 이 예에서는 슬라이서에서 사용의 멤버는 **SalesTerritory** 오스트레일리아에서 판매만 계산에 사용 되는 쿼리를 필터링 하는 차원입니다.

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

명명 된 인스턴스의 수 R에서 제어 문자 간주 될 수 있는 모든 문자를 이스케이프 해야  예를 들어 다음 연결 문자열 ContosoHQ 이라는 서버에 OLAP01, 인스턴스를 참조 합니다.

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP;"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>미리 정의된 MDX 문자열로 이 쿼리를 실행하려면

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

SQL Server Management Studio에서 MDX 작성기를 사용 하 여 쿼리를 정의한 다음 MDX 문자열을 저장 하는 경우에 다음과 같이 0부터 시작 하는 축 번호 됩니다. 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

미리 정의된 MDX 문자열로 이 쿼리를 실행할 수도 있습니다. 그러나 사용 하 여 R을 사용 하 여 동일한 쿼리를 작성 하는 `axis()` 함수를 1부터 시작 하는 축 매기 해야 합니다.

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. SSAS 인스턴스에서 큐브 및 해당 필드 탐색

`explore` 함수를 사용하여 쿼리를 구성하는 데 사용할 큐브, 차원 또는 멤버 목록을 반환할 수 있습니다. 다른 OLAP 검색 도구에 액세스할 수 없는 경우 또는 MDX 쿼리를 프로그래밍 방식으로 조작하거나 구성하려는 경우에 유용합니다.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>지정된 연결에서 사용할 수 있는 큐브를 나열하려면

보기 권한이 있는 인스턴스에서 모든 큐브 또는 큐브 뷰를 보려면 핸들을 `explore`에 대한 인수로 제공합니다.

> [!IMPORTANT]
> 최종 결과 **하지** 큐브; True 이면 메타 데이터 작업이 성공 했음을 단순히 나타냅니다. 인수가 유효하지 않을 경우 오류가 발생합니다.

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

원본을 정의하고 핸들을 만든 후 반환할 큐브, 차원 및 계층을 지정합니다. 반환 결과 접두사로 사용 하는 항목에에서 **->** 이전 멤버의 자식 항목을 나타냅니다.

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


## <a name="see-also"></a>참고 항목

[OLAP 큐브에서 데이터를 사용 하 여 R에서](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
