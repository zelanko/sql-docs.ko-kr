---
title: 데이터 원본 및 바인딩 (SSAS 다차원) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76afbfcd2cd7668cfc65fc5078a1015ac33bc964
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178954"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>데이터 원본 및 바인딩(SSAS 다차원)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  큐브, 차원 및 기타 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체는 데이터 원본에 바인딩될 수 있습니다. 데이터 원본은 다음 개체 중 하나일 수 있습니다.  
  
-   관계형 데이터 원본.  
  
-   행 집합(또는 장으로 구성된 행 집합)을 출력하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 파이프라인.  
  
 데이터 원본의 표현 방법은 데이터 원본의 형식에 따라 달라집니다. 예를 들어 관계형 데이터 원본은 연결 문자열로 구분됩니다. 데이터 원본에 대한 자세한 내용은 [Data Sources in Multidimensional Models](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)를 참조하세요.  
  
 사용되는 데이터 원본에 관계없이 DSC(데이터 원본 뷰)에는 데이터 원본에 대한 메타데이터가 포함됩니다. 따라서 큐브 또는 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 바인딩은 DSV에 대한 바인딩으로 표현됩니다. 이러한 바인딩은 논리 개체-뷰, 계산된 열 및 데이터 원본에 물리적으로 존재 하지 않는 관계와 같은 개체에 대 한 바인딩이 포함할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 식을 DSV로 캡슐화하는 계산 열을 추가한 다음 해당 OLAP 측정값을 DSV의 이 열에 바인딩합니다. DSV에 대한 자세한 내용은 [Data Source Views in Multidimensional Models](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)를 참조하십시오.  
  
 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체는 자체적인 방식으로 데이터 원본에 바인딩됩니다. 또한 이러한 개체에 대한 데이터 바인딩과 데이터 원본 정의는 데이터 바인딩된 개체(예: 차원)의 정의와 인라인으로 제공되거나 별도의 정의 집합으로 아웃오브 라인으로 제공될 수 있습니다.  
  
## <a name="analysis-services-data-types"></a>Analysis Services 데이터 형식  
 바인딩에 사용되는 데이터 형식은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 지원하는 데이터 형식과 일치해야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 정의되어 있는 데이터 형식은 다음과 같습니다.  
  
|Analysis Services 데이터 형식|설명|  
|---------------------------------|-----------------|  
|BigInt|부호 있는 64비트 정수입니다. 이 데이터 형식은 Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Int64 데이터 형식 및 OLE DB의 DBTYPE_I8 데이터 형식에 매핑됩니다.|  
|Bool|부울 값입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Boolean 데이터 형식 및 OLE DB의 DBTYPE_BOOL 데이터 형식에 매핑됩니다.|  
|Currency|정확성이 통화 단위의 10/1,000인 -263(또는 -922,337,203,685,477.5808)에서 263-1(또는 +922,337,203,685,477.5807)까지의 통화 값입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Decimal 데이터 형식 및 OLE DB의 DBTYPE_CY 데이터 형식에 매핑됩니다.|  
|Date|배정밀도 부동 소수점 숫자로 저장되는 날짜 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 날짜 수이고, 소수 부분은 하루를 분수로 표시한 수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 DateTime 데이터 형식 및 OLE DB의 DBTYPE_DATE 데이터 형식에 매핑됩니다.|  
|Double|-1.79E+308부터 1.79E+308 사이의 배정밀도 부동 소수점 숫자입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Double 데이터 형식 및 OLE DB의 DBTYPE_R8 데이터 형식에 매핑됩니다.|  
|정수|부호 있는 32비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Int32 데이터 형식 및 OLE DB의 DBTYPE_I4 데이터 형식에 매핑됩니다.|  
|Single|-3.40E+38부터 3.40E+38 사이의 단정밀도 부동 소수점 숫자입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Single 데이터 형식 및 OLE DB의 DBTYPE_R4 데이터 형식에 매핑됩니다.|  
|SmallInt|부호 있는 16비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 Int16 데이터 형식 및 OLE DB의 DBTYPE_I2 데이터 형식에 매핑됩니다.|  
|TinyInt|부호 있는 8비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 SByte 데이터 형식 및 OLE DB의 DBTYPE_I1 데이터 형식에 매핑됩니다.<br /><br /> 참고: 데이터 원본은 데이터 형식이 tinyint 인 필드가 포함 하 고 데이터 원본 뷰에서 정수로 변환 됩니다 AutoIncrement 속성이 True로 설정 됩니다.|  
|UnsignedBigInt|부호 없는 64비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 UInt64 데이터 형식 및 OLE DB의 DBTYPE_UI8 데이터 형식에 매핑됩니다.|  
|UnsignedInt|부호 없는 32비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 UInt32 데이터 형식 및 OLE DB의 DBTYPE_UI4 데이터 형식에 매핑됩니다.|  
|UnsignedSmallInt|부호 없는 16비트 정수입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 UInt16 데이터 형식 및 OLE DB의 DBTYPE_UI2 데이터 형식에 매핑됩니다.|  
|WChar|유니코드 문자의 Null로 끝나는 스트림입니다. 이 데이터 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 String 데이터 형식 및 OLE DB의 DBTYPE_WSTR 데이터 형식에 매핑됩니다.|  
  
 데이터 원본으로부터 받은 모든 데이터는 대개 처리 중에 바인딩에 지정된 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 형식으로 변환됩니다. String을 Int로 변환할 때와 같이 변환을 수행할 수 없는 경우 오류가 발생합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서는 일반적으로 바인딩의 데이터 형식을 데이터 원본의 유형에 가장 일치하는 형식으로 설정합니다. 예를 들어 SQL 유형의 Date, DateTime, SmallDateTime, DateTime2, DateTimeOffset은 [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date에 매핑되고 SQL 유형의 Time은 String에 매핑됩니다.  
  
## <a name="bindings-for-dimensions"></a>차원에 대한 바인딩  
 차원의 각 특성은 DSV의 열에 바인딩됩니다. 차원의 모든 특성은 하나의 데이터 원본에서 가져와야 합니다. 그러나 특성은 다른 테이블의 열에 바인딩될 수 있습니다. 테이블 간의 관계는 DSV에 정의됩니다. 동일한 테이블에 둘 이상의 관계 집합이 있는 경우 역할 '별칭' 테이블을 DSV의 명명 된 쿼리를 할 수 있습니다. DSV에서 식과 필터는 명명된 계산 및 명명된 쿼리를 사용하여 정의됩니다.  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>MeasureGroups, Measures 및 Partitions에 대한 바인딩  
 각 측정값 그룹에는 다음과 같은 기본 바인딩이 있습니다.  
  
-   측정값 그룹은 DSV의 테이블에 바인딩됩니다(예: **MeasureGroup.Source**).  
  
-   각 측정값은 해당 테이블의 열에 바인딩됩니다(예: **Measure.ValueColumn.Source**).  
  
-   각 측정값 그룹 차원에는 측정값 그룹의 세분성을 정의하는 *세분성 특성* 집합이 있습니다. 이러한 각 특성은 특성 키를 포함하는 팩트 테이블의 열에 바인딩되어야 합니다. 세분성 특성에 대한 자세한 내용은 이 항목의 뒷부분에 있는 MeasureGroup 세분성 특성을 참조하십시오.  
  
 이러한 기본 바인딩은 파티션별로 선택적으로 재정의할 수 있습니다. 각 파티션은 다른 데이터 원본, 테이블이나 쿼리 이름, 또는 필터 식을 지정할 수 있습니다. 가장 일반적인 분할 전략은 동일한 데이터 원본을 사용하여 파티션별로 테이블을 재정의하는 것입니다. 대안으로는 파티션별로 다른 필터를 적용하거나 데이터 원본을 바꾸는 것이 있습니다.  
  
 기본 데이터 원본은 DSV에 정의되어 관계의 세부 정보를 포함한 스키마 정보를 제공해야 합니다. 파티션 수준에서 정의되는 추가 테이블 또는 쿼리는 DSV에 나열되지 않아도 되지만 측정값 그룹에 대해 정의된 기본 테이블과 같은 스키마를 갖거나 최소한 측정값 또는 세분성 특성에 사용된 모든 열을 포함해야 합니다. 측정값 및 세분성 특성별로 세분화된 바인딩은 파티션 수준에서 재정의할 수 없으며 측정값 그룹에 대해 정의된 것과 동일한 열에 있는 것으로 가정됩니다. 따라서 파티션에서 실제로 다른 스키마를 가진 데이터 원본을 사용하는 경우 파티션에 대해 정의된 **TableDefinition** 쿼리의 결과는 측정값 그룹에 의해 사용된 스키마와 동일한 스키마여야 합니다.  
  
### <a name="measuregroup-granularity-attributes"></a>MeasureGroup 세분성 특성  
 측정값 그룹의 세분성이 데이터베이스에 알려진 세분성에 일치하고 팩트 테이블에서 차원 테이블로 직접적인 관계가 있는 경우 세분성 특성은 적절한 외래 키 열 또는 팩트 테이블의 열에만 바인딩되면 됩니다. 예를 들어 다음 팩트 테이블 및 차원 테이블을 살펴보십시오.  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 주문된 제품별로 분석해 보면 Sales 차원 역할의 Ordered Product의 경우 Product 세분성 특성은 Sales.OrderedProductID에 바인딩될 것입니다.  
  
 한편 **GranularityAttributes** 가 팩트 테이블의 열로 존재하지 않는 경우도 있습니다. 예를 들어 **GranularityAttributes** 는 다음과 같은 경우에는 열로 존재하지 않을 것입니다.  
  
-   OLAP 세분성이 원본의 세분성보다 성긴 경우.  
  
-   중간 테이블이 팩트 테이블과 차원 테이블 사이에 개입하는 경우.  
  
-   차원 키가 차원 테이블의 기본 키와 다른 경우.  
  
 이러한 경우에는 모두 GranularityAttributes가 팩트 테이블에 존재하도록 DSV가 정의되어야 합니다. 예를 들어 명명된 쿼리 또는 계산 열을 사용할 수 있습니다.  
  
 예를 들어 위와 같은 테이블에서 세분성이 Category별이라면 Sales의 뷰는 다음과 같이 사용될 수 있습니다.  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 이 경우 GranularityAttribute Category는 SalesWithCategory.OrderedProductCategory에 바인딩됩니다.  
  
### <a name="migrating-from-decision-support-objects"></a>의사 결정 지원 개체에서 마이그레이션  
 DSO(의사 결정 지원 개체) 8.0을 사용하면 **PartitionMeasures** 를 다시 바인딩할 수 있습니다. 따라서 이러한 경우 마이그레이션 전략은 적절한 쿼리를 작성하는 것입니다.  
  
 마찬가지로 DSO 8.0에서 허용하긴 하지만 파티션 내에서 차원 특성은 다시 바인딩할 수 없습니다. 이러한 경우 마이그레이션 전략은 DSV에서 필요한 명명된 쿼리를 정의하여 차원에 사용된 테이블 및 열과 동일한 테이블 및 열이 파티션에 대한 DSV에 있도록 하는 것입니다. 이와 같은 경우에는 From/Join/Filter 절이 관련 테이블의 구조화된 집합이 아닌 하나의 명명된 쿼리에 매핑되는 간단한 마이그레이션을 채택해야 할 수도 있습니다. DSO 8.0은 파티션이 동일한 데이터 원본을 사용하는 경우에도 PartitionDimensions의 재바인딩을 허용하므로 마이그레이션 시 동일한 데이터 원본에 대해 여러 DSV가 필요할 수 있습니다.  
  
 DSO 8.0에서 해당 바인딩은 최적화된 스키마가 사용되는지 여부에 따라 차원 테이블의 기본 키 또는 팩트 테이블의 외래 키 중 하나에 바인딩되어 두 가지 방법으로 표현할 수 있습니다. ASSL에서는 이 두 가지 다른 형식이 구분되지 않습니다.  
  
 차원 테이블을 포함하지 않는 데이터 원본을 사용하는 파티션에 대해서도 동일한 바인딩 접근 방식이 적용됩니다. 바인딩이 차원 테이블의 기본 키 열이 아니라 팩트 테이블의 외래 키 열에 대해 수행되기 때문입니다.  
  
## <a name="bindings-for-mining-models"></a>마이닝 모델에 대한 바인딩  
 마이닝 모델은 관계형 또는 OLAP입니다. 관계형 마이닝 모델에 대한 데이터 바인딩은 OLAP 마이닝 모델에 대한 바인딩과 상당히 다릅니다.  
  
### <a name="bindings-for-a-relational-mining-model"></a>관계형 마이닝 모델에 대한 바인딩  
 관계형 마이닝 모델은 DSV에 정의된 관계를 기반으로 어느 열이 어느 데이터 원본에 바인딩되는지에 대한 모호함을 해결합니다. 관계형 마이닝 모델에서 데이터 바인딩은 다음과 같은 규칙을 따릅니다.  
  
-   각 비중첩 테이블 열은 사례 테이블 또는 사례 테이블과 관련된 테이블의 열에 바인딩됩니다(다 대 일 또는 일 대 일 관계에 따름). DSV는 테이블 간의 관계를 정의합니다.  
  
-   각 중첩 테이블 열은 원본 테이블에 바인딩됩니다. 그러면 중첩 테이블 열이 소유한 열은 원본 테이블 또는 이 원본 테이블과 관련된 테이블의 열에 바인딩됩니다. 이 경우에도 바인딩은 다 대 일 또는 일 대 일 관계를 따릅니다. 마이닝 모델 바인딩은 중첩 테이블에 조인 경로를 제공하지 않습니다. 대신 이 정보는 DSV에 정의된 관계가 제공합니다.  
  
### <a name="bindings-for-an-olap-mining-model"></a>OLAP 마이닝 모델에 대한 바인딩  
 OLAP 마이닝 모델에는 DSV에 해당하는 요소가 없습니다. 따라서 데이터 바인딩은 열과 데이터 원본 사이에 모호함이 없도록 해야 합니다. 예를 들어 마이닝 모델은 Sales 큐브를 기반으로 하고 열은 Qty, Amount 및 Product Name을 기반으로 할 수 있습니다. 또는 마이닝 모델은 Product를 기반으로 하고 열은 Product Name, Product Color 및 Sales Qty가 있는 중첩 테이블을 기반으로 할 수 있습니다.  
  
 OLAP 마이닝 모델에서 데이터 바인딩은 다음과 같은 규칙을 따릅니다.  
  
-   각 비중첩 테이블 열은 큐브의 측정값, 해당 큐브의 차원의 특성(차원 역할의 경우 모호함을 없애기 위해 **CubeDimension** 지정) 또는 차원의 특성에 바인딩됩니다.  
  
-   각 중첩 테이블 열은 **CubeDimension**에 바인딩됩니다. 즉 차원에서 관련된 큐브로, 또는 드물지만 중첩 테이블의 경우 큐브에서 차원 중 하나로 이동하는 방법을 정의합니다.  
  
## <a name="out-of-line-bindings"></a>아웃오브 라인 바인딩  
 아웃오브 라인 바인딩을 사용하여 명령을 실행하는 동안 일시적으로 기존 데이터 바인딩을 변경할 수 있습니다. 아웃오브 라인 바인딩은 명령에 포함되며 지속되지 않는 바인딩을 지칭합니다. 아웃오브 라인 바인딩은 이러한 특정 명령이 실행되는 동안에만 적용됩니다. 반면 인라인 바인딩은 ASSL 개체 정의에 포함되며 서버 메타데이터 내에서 개체 정의와 함께 지속됩니다.  
  
 ASSL에서는 **Process** 명령 또는 일괄 처리에 포함되지 않은 경우 **Batch** 명령에서 확장 바인딩 지정이 허용됩니다. 확장 바인딩이 **Batch** 명령에 지정되는 경우 **Batch** 명령에 지정되는 모든 바인딩은 일괄 처리의 모든 **Process** 명령이 실행되는 새 바인딩 컨텍스트를 생성합니다. 이 새 바인딩 컨텍스트에는 **Process** 명령으로 인해 간접적으로 처리되는 개체가 포함됩니다.  
  
 명령에 아웃오브 라인 바인딩이 지정되면 이러한 바인딩은 지정된 개체에 대한 지속형 DDL에 포함된 인라인 바인딩을 다시 정의합니다. 이렇게 처리되는 개체에는 **Process** 명령에서 직접 명명된 개체 또는, 처리의 일부로 자동으로 처리 작업이 시작되는 기타 개체가 포함될 수 있습니다.  
  
 확장 바인딩은 옵션인 **Bindings** 컬렉션 개체를 처리 명령으로 포함하여 지정합니다. 옵션인 **Bindings** 컬렉션에는 다음 요소가 포함됩니다.  
  
|속성|카디널리티|type|설명|  
|--------------|-----------------|----------|-----------------|  
|**Binding**|0-n|**Binding**|새 바인딩의 컬렉션을 제공합니다.|  
|**DataSource**|0-1|**DataSource**|사용되었을 수 있는 서버의 **DataSource** 를 대체합니다.|  
|**DataSourceView**|0-1|**DataSourceView**|사용되었을 수 있는 서버의 **DataSourceView** 를<br /><br /> 대체합니다.|  
  
 아웃오브 라인 바인딩과 관련된 모든 요소는 선택 사항입니다. 지정되지 않은 요소에 대해 ASSL은 지속형 개체의 DDL에 포함된 사양을 사용합니다. **DataSource** 명령에서 **DataSourceView** 또는 **Process** 지정은 선택 사항입니다. **DataSource** 또는 **DataSourceView** 가 지정된 경우 이는 인스턴스화되지 않으며 **Process** 명령이 완료된 후 지속되지 않습니다.  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>아웃오브 라인 바인딩 유형 정의  
 확장 **Bindings** 컬렉션 내에서 ASSL은 **Binding**당 여러 개체에 대한 바인딩 컬렉션을 허용합니다. 각 **Bindings** 에는 확장 개체 참조가 있습니다. 확장 개체 참조는 개체 참조와 비슷하지만 보조 개체(예: 차원 특성 및 측정값 그룹 특성)도 참조할 수 있습니다. 이 개체에 일반적인 플랫 형식을 취합니다 합니다 **개체** 요소에 **프로세스** 명령을 제외한 합니다 \< *개체* > \< *개체/* > 태그는 표시 되지 않습니다.  
  
 바인딩이 지정 되는 각 개체 형식의 XML 요소로 식별 됩니다 \< *개체*> ID (예를 들어 **DimensionID**). 개체를 확인 한 후 폼을 사용 하 여 구체적으로 최대한 \< *개체*> ID는 일반적으로는 바인딩이 지정 되는 요소를 식별 한 다음 **원본**. 한 가지 일반적인 경우는 **Source** 가 **DataItem**의 속성인 경우로, 특성의 열 바인딩이 이에 해당합니다. 이 경우에는 **DataItem** 태그를 지정하지 않고 바인딩할 열에 바로 있는 것처럼 **Source** 속성만 지정합니다.  
  
 **KeyColumns** 는 **KeyColumns** 컬렉션 내의 순서에 의해 식별됩니다. 여기에서는 예를 들어 특성의 첫 번째와 세 번째 키 열만 지정할 수는 없습니다. 두 번째 키 열을 건너뛴다는 점을 나타낼 방법이 없기 때문입니다. 모든 키 열은 차원 특성에 대한 아웃오브 라인 바인딩에 있어야 합니다.  
  
 **Translations**는 ID가 없지만 언어에 의해 의미상으로 식별됩니다. 따라서 **Translations** 내의 **Binding** 는 언어 식별자를 포함해야 합니다.  
  
 **Binding** 내에 허용되는, DDL에 직접 존재하지 않는 한 가지 추가 요소는 **ParentColumnID**로, 이 요소는 데이터 마이닝을 위한 중첩 테이블에 사용됩니다. 이 경우 바인딩이 제공되는 중첩 테이블에 있는 부모 열을 식별해야 합니다.  
  
  
