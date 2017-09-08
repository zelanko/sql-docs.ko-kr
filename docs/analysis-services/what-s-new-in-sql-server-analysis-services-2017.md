---
title: "기능 &#39; s SQL Server 2017 Analysis Services의 새로운 기능 | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 572af6f86f015c88141bb6e78b781b5825be155c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>기능 &#39; s SQL Server 2017 Analysis Services의 새로운 기능
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>SQL Server 2017 Analysis Services RC2
이 릴리스에는 새로운 기능이 없습니다. 이 릴리스에서 향상 된 기능에는 버그 수정 및 성능 포함 됩니다.

## <a name="sql-server-2017-analysis-services-rc1"></a>SQL Server 2017 Analysis Services RC1
이 릴리스의 새로운 기능은 없습니다,이 릴리스에 추가 기능을 포함 하는 반면 [동적 관리 뷰](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) 1400 하 고 1200 호환성 수준의 테이블 형식 모델에 대 한 합니다.

DISCOVER_CALC_DEPENDENCY 이제 테이블 형식 1200 및 1400 모델과 함께 작동합니다. 테이블 형식 1400 모델 M 파티션, M 식 및 구조화 된 데이터 소스 간의 종속성을 표시합니다. 자세한 내용은 참조는 [Analysis Services 블로그](https://blogs.msdn.microsoft.com/analysisservices/)합니다.

MDSCHEMA_MEASUREGROUP_DIMENSIONS 개선 측정값 차원이 표시 하도록 다양 한 클라이언트 도구에서 사용 되는이 DMV에 대 한 포함 됩니다. 예를 들어 Excel 피벗 테이블에서 탐색 기능에는 사용자를 크로스-선택한 측정값을 관련 차원 데이터로 드릴을 수 있습니다. 이 릴리스에서 잘못 된 값이 이전에 표시 된 카디널리티 열을 수정 합니다.

## <a name="sql-server-analysis-services-ctp-21"></a>SQL Server Analysis Services CTP 2.1
이 릴리스에는 새로운 기능이 없습니다. 이 릴리스에서 향상 된 기능 포함 버그 수정 및 성능 및 향상 된 기능 [동적 관리 뷰](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV). Dmv는 로컬 서버 작업 및 서버 상태에 대 한 정보를 반환 하는 SQL Server Profiler에서 쿼리 합니다. 자세한 내용은 참조는 [Analysis Services 블로그](https://blogs.msdn.microsoft.com/analysisservices/)합니다.

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services CTP 2.0
이 릴리스에 테이블 형식 모델에 대 한 향상 된 여러 새로운 기능 포함 하 여:

* 테이블 형식 모델의 메타데이터를 보호하는 개체 수준 보안
* 응답성 개발자 환경에 대 한 트랜잭션 성능이 개선 되었습니다.
* 1200 및 1400 모델 종속성 분석을 사용 하도록 설정 및 보고에 대 한 동적 관리 뷰 개선 되었습니다.
* 자세한 행 식에 대 한 제작 환경에 개선 되었습니다.
* 계층 구조 및 열에는 Power BI 필드 목록에 더 유용한 위치에 표시 되어야 하 다시 사용 합니다.
* 날짜 필드를 기반으로 하는 날짜 차원에 대 한 관계를 쉽게 만들 날짜 관계입니다.
* Analysis Services에 대 한 기본 설치 옵션은 이제 테이블 형식 모드에 대 한 합니다.
* 새 데이터 가져오기 (Power Qery) 데이터 원본.
* SSDT용 DAX 편집기
* M 쿼리에 대 한 기존 DirectQuery 데이터 원본 지원 합니다.
* 보기, 편집, 스크립팅 구조화 된 데이터 원본에 대 한 지원 같은 SSMS 개선 합니다.

이 CTP 2.0 버전에 대 한 자세한 내용을 보려면 참조는 [Analysis Services 블로그](https://blogs.msdn.microsoft.com/analysisservices/)합니다.

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>Windows 1.4 CTP에서 SQL Server Analysis Services
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate) 및 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate) 미리 보기 릴리스에서 SQL Server 2017 미리 보기 릴리스와 일치 합니다. 최신 새 기능을 사용 해야 합니다. 자세한 내용은 참조는 [Analysis Services 블로그](https://blogs.msdn.microsoft.com/analysisservices/)합니다.



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>Windows 1.3 CTP에서 SQL Server Analysis Services

### <a name="encoding-hints"></a>인코딩 힌트

이 릴리스에서 인코딩 힌트 (데이터 새로 고침) 큰 메모리 내 테이블 형식 모델의 처리를 최적화 하는 데 사용 하는 고급 기능을 소개 합니다. 인코딩을 더 잘 이해 하려면 참조 [성능 튜닝의 테이블 형식 모델 SQL Server 2012 Analysis Services에서](https://msdn.microsoft.com/library/dn393915.aspx) 인코딩 더 잘 이해 하는 백서입니다. 여기에서 설명 하는 인코딩 프로세스 1.3 CTP에에서 적용 됩니다.

* 값 인코딩을 일반적으로 집계의 경우에 사용 되는 열에 대 한 쿼리 성능을 향상을 제공 합니다.

* 해시 인코딩을 group by 열 (대개 차원 테이블 값) 및 외래 키에 대 한 선호 됩니다. 문자열 열은 항상 인코딩된 해시입니다.

숫자 열이 인코딩 방법 중 하나를 사용할 수 있습니다. Analysis Services의 처리를 시작 테이블 (또는 제외 파티션) 테이블이 없거나 테이블 비어 있으면 또는 전체 테이블 처리 작업이 수행 되는 샘플 값 취해집니다 값 또는 해시 인코딩 적용 여부를 확인 하려면 각 숫자 열에 대 한 . 기본적으로 값 인코딩을 선택한 경우 열에 고유한 값의 샘플을 충분히 큰 – 해시 인코딩을 일반적으로 제공 보다 효율적인 압축 합니다. 열은 데이터 분포에 대 한 추가 정보에 따라 부분적으로 처리 한 후 인코딩 방법 변경를 인코딩 프로세스를 다시 시작 Analysis Services에 대 한 것 같습니다. 이 물론 처리 시간이 늘어나고 비효율적입니다. 성능 조정 백서 다시 자세히는 인코딩을 설명 및 SQL Server Profiler를 사용 하 여 요소를 검색 하는 방법을 설명 합니다.

CTP 1.3에 인코딩 힌트에서 데이터 프로 파일링 및/또는 응답으로 다시 추적 이벤트를 인코딩 사전 지식이 지정 된 인코딩 방법에 대 한 기본 설정을 지정 하는 모델을 허용 합니다. 이후 해시 인코딩된 열에 대 한 집계는 인코딩된 값 열에 대해 값 인코딩을 지정할 수 있습니다 이러한 열에 대 한 힌트로 보다 속도가 느립니다. 기본 설정이 적용 됨; 보장 되지 않습니다. 따라서이 설정 달리 힌트입니다. 인코딩 힌트를 지정 하려면 열에 EncodingHint 속성을 설정 합니다. 가능한 값은 "Default", "Value" 및 "해시"입니다. 작성 시점에는 속성이 표시 되지 않습니다 아직 ssdt에서 JSON 기반 메타 데이터, TMSL Tabular Model Scripting Language (), 또는 테이블 형식 개체 모델 (TOM)를 사용 하 여 설정할 수 있도록 합니다. JSON 기반 메타 데이터는 Model.bim 파일에서의 다음 코드 조각은 Sales Amount 열에 대 한 인코딩 값을 지정 합니다.

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

### <a name="extended-events-not-working-in-ctp-13"></a>확장 이벤트 CTP 1.3에서 작동 하지 않음
확장 이벤트는 SSAS CTP 1.3에서 작동 하지 않습니다. 다음 CTP에서 수정 프로그램을 계획 합니다.

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>Windows CTP 1.2의 SQL Server Analysis Services

이 릴리스에는 새로운 기능이 없습니다. 향상된 기능에는 버그 수정 및 성능이 포함됩니다.

새 쿼리 편집기 메뉴 및 빠른 액세스 기능을 사용 하 여 CTP 1.1에서 도입 된 새로운 최신 데이터 가져오기 환경을 향상 시켰습니다는 최신 미리 보기 버전의 SSDT SQL Server 데이터 도구 (), SQL Server 2017 CTP 1.2와 일치 합니다. 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>Windows CTP1.1의 SQL Server Analysis Services 

이 릴리스에서는 테이블 형식 모델에 대한 향상된 기능을 소개합니다. 

### <a name="1400-compatibility-level-for-tabular-models"></a>테이블 형식 모델에 대한&1400; 호환성 수준
  이 문서에서 설명하는 기능을 활용하려면 기존 또는 새 테이블 형식 모델을 1400 호환성 수준으로 설정해야 합니다. 1400 호환성 수준의 모델은 SQL Server 2016 SP1 이전 버전에 배포하거나 하위 호환성 수준으로 다운그레이드할 수 없습니다.
  
  새로 만들거나 기존 테이블 형식 모델 프로젝트를 1400 호환성 수준으로 업그레이드하려면 **SSDT(SQL Server Data Tools) 17.0 RC2** [미리 보기 릴리스](https://go.microsoft.com/fwlink?LinkId=837939)를 다운로드 및 설치합니다. 
  
SSDT에서 새 테이블 형식 모델 프로젝트를 만들 때 새 1400 호환성 수준을 선택할 수 있습니다. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> SSDT(SQL Server Data Tools) 12월 릴리스의 통합 작업 영역에서는 1400 호환성 수준을 지원합니다. 작업 영역 서버 인스턴스에서 새 테이블 형식 모델 프로젝트를 만드는 경우 해당 인스턴스 또는 프로젝트를 배포하는 모든 인스턴스는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1이어야 합니다. 

솔루션 탐색기에서 SSDT에서는 기존 테이블 형식 모델을 업그레이드 하려면 마우스 오른쪽 단추로 클릭 **Model.bim**, 한 다음 **속성**로 설정 된 **호환성 수준이** 속성 를 **SQL Server 2017 (1400)**합니다. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>최신 데이터 가져오기 환경
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1 릴리스와 함께 제공되는 SSDT(SQL Server Data Tools)의 최신 미리 보기 릴리스에서는 1400 호환성 수준의 테이블 형식 모델에 대한 최신 **데이터 가져오기** 환경이 도입되었습니다. 이 새로운 기능은 Power BI Desktop 및 Microsoft Excel 2016의 유사한 기능을 기반으로 합니다.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> 이 릴리스에서는 제한된 개수의 데이터 원본이 지원됩니다. 향후 업데이트에서 추가 데이터 원본 및 기능을 지원할 예정입니다.

최신 데이터 가져오기 환경에 대한 자세한 내용은 [Analysis Services 팀 블로그](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/)를 참조하세요.

## <a name="ragged-hierarchies"></a>비정형 계층 구조
테이블 형식 모델에서 부모-자식 계층 구조를 모델링할 수 있습니다. 수준 수가 서로 다른 계층 구조를 종종 비정형 계층 구조라고 합니다. 기본적으로, 비정형 계층 구조에서는 최하위 자식 아래 수준을 위한 공백이 표시됩니다. 조직 차트에서 비정형 계층 구조의 예는 다음과 같습니다.

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

이 릴리스에서는 **멤버 숨기기** 속성이 도입되었습니다. 계층 구조에 대한 **멤버 숨기기** 속성을 **빈 멤버 숨기기**로 설정할 수 있습니다.

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > 모델의 빈 멤버는 빈 문자열 아니라 DAX 빈 값으로 표시됩니다.

**빈 멤버 숨기기**로 설정하고 모델을 배포한 경우 읽기 쉬운 계층 구조 버전이 Excel 등의 보고 클라이언트에 표시됩니다.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>정보 행
이제 측정값에 영향을 주는 사용자 지정 행 집합을 정의할 수 있습니다. 정보 행은 다차원 모델의 기본 드릴스루 작업과 비슷합니다. 따라서 최종 사용자가 집계된 수준보다 자세히 정보를 볼 수 있습니다. 

다음 피벗 테이블은 Adventure Works 샘플 테이블 형식 모델의 연도별 인터넷 총 매출액을 보여 줍니다. 측정값에서 집계된 값이 포함된 셀을 마우스 오른쪽 단추로 클릭한 다음 **자세한 정보 표시** 를 클릭하면 정보 행을 볼 수 있습니다.

![AS_Show_Details](../analysis-services/media/as-show-details.png)

기본적으로 Internet Sales 테이블의 관련 데이터가 표시됩니다. 고객 이름 및 주문 정보와 같은 유용한 정보를 표시하는 데 필요한 열이 테이블에 없을 수 있기 때문에 이 제한된 동작은 사용자에게 의미가 없는 경우가 많습니다. 정보 행을 사용하여 측정값의 **정보 행 식** 속성을 지정할 수 있습니다.

#### <a name="detail-rows-expression-property-for-measures"></a>측정값의 정보 행 식 속성
측정값의 **정보 행 식** 속성을 통해 모델 작성자는 최종 사용자에게 반환되는 열과 행을 사용자 지정할 수 있습니다.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

[SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) DAX 함수는 일반적으로 정보 행 식에서 사용됩니다. 다음 예제에서는 샘플 Adventure Works 테이블 형식 모델의 Internet Sales 테이블 행에 대해 반환할 열을 정의합니다.

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

속성을 정의하고 모델을 배포한 후 사용자가 **자세한 정보 표시**를 선택하면 사용자 지정 행 집합이 반환됩니다. 선택한 셀의 필터 컨텍스트가 자동으로 적용됩니다. 이 예제에서는 2010 값에 대한 행만 표시됩니다.

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>테이블의 기본 정보 행 식 속성
측정값 외에 테이블에는 정보 행 식을 정의하는 속성도 있습니다. **기본 정보 행 식** 속성은 테이블 내 모든 측정값의 기본값으로 사용됩니다. 해당 식이 정의되지 않은 측정값은 테이블에서 식을 상속하며 테이블에 대해 정의된 행 집합을 표시합니다. 이렇게 하면 식을 재사용할 수 있으며, 나중에 테이블에 추가된 새 측정값이 자동으로 식을 상속합니다.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>DETAILROWS DAX 함수
이 릴리스에는 정보 행 식에서 정의된 행 집합을 반환하는 새 `DETAILROWS` DAX 함수가 포함되어 있습니다. 테이블 형식 모델에서 정의된 정보 행 식과도 호환되는 MDX의 `DRILLTHROUGH` 문과 유사하게 작동합니다.

다음 DAX 쿼리는 측정값 또는 해당 테이블에 대해 정보 행 식에서 정의된 행 집합을 반환합니다. 식이 정의되지 않은 경우 측정값을 포함하는 테이블인 Internet Sales 테이블에 대한 데이터가 반환됩니다.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>향상된 DAX 기능
이 릴리스에는 DAX 식에 대한 `IN` 연산자가 포함되어 있습니다. 이것은 [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) 절에서 여러 값을 지정하는 데 자주 사용되는 `WHERE` 연산자와 유사합니다.

이전에는 다음 측정값 식과 같이 논리적 `OR` 연산자를 사용하여 다중 값 필터를 지정하는 것이 일반적이었습니다.

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

`IN` 연산자를 사용하면 이 작업이 간소화됩니다.
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

이 경우 `IN` 연산자는 지정된 색마다 하나씩, 3개의 행이 포함된 단일 열 테이블을 참조합니다. 테이블 생성자 구문은 중괄호를 사용합니다.

`IN` 연산자는 `CONTAINSROW` 함수와 기능적으로 동일합니다.
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

`IN` 연산자를 테이블 생성자와 함께 효과적으로 사용할 수도 있습니다. 예를 들어 다음 측정값은 제품 색 및 범주를 결합하여 필터링합니다.
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

새 `IN` 연산자를 사용하면 위의 측정값 식은 이제 아래 식과 동일합니다.
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```


## <a name="table-level-security"></a>테이블 수준 보안
이 릴리스에서는 테이블 수준 보안이 도입되었습니다. 테이블 데이터에 대한 액세스 제한 외에도 중요한 테이블 이름을 보호할 수 있습니다. 이렇게 하면 악의적인 사용자가 해당 테이블이 있는지 검색할 수 없습니다.

JSON 기반 메타데이터, TMSL(Tabular Model Scripting Language) 또는 TOM(테이블 형식 개체 모델)을 사용하여 테이블 수준 보안을 설정해야 합니다. 

예를 들어 다음 코드는 **TablePermission** 클래스의 **MetadataPermission** 속성을 **None**으로 설정하여 샘플 Adventure Works 테이블 형식 모델의 Product 테이블을 보호하는 데 도움이 됩니다.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```


