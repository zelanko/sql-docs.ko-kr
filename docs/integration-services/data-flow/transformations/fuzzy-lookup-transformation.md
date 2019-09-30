---
title: 유사 항목 조회 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fuzzylookuptrans.f1
- sql13.dts.designer.fuzzylookuptransformation.referencetable.f1
- sql13.dts.designer.fuzzylookuptransformation.columns.f1
- sql13.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 723c8f8b34ceb9e96ae6da196a64f766b18857ef
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291500"
---
# <a name="fuzzy-lookup-transformation"></a>유사 항목 조회 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  유사 항목 조회 변환은 데이터 표준화, 데이터 수정, 누락된 값 제공 등 데이터 정리 태스크를 수행합니다.  
  
> [!NOTE]  
>  성능 및 메모리 제한 사항을 포함하여 유사 항목 조회 변환에 대한 자세한 내용은 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(SQL Server Integration Services 2005에서 유사 항목 조회 및 유사 항목 그룹화) 백서를 참조하세요.  
  
 유사 항목 조회 변환 작업은 유사 항목 일치를 사용한다는 점에서 조회 변환과 다릅니다. 조회 변환은 동등 조인을 사용하여 참조 테이블에서 일치하는 레코드를 찾으며 일치하는 레코드가 하나 이상 있는 레코드와 일치하는 레코드가 없는 레코드를 반환합니다. 반대로 유사 항목 조회 변환은 유사 일치를 사용하여 참조 테이블에서 하나 이상의 근접하게 일치하는 항목을 반환합니다.  
  
 유사 항목 조회 변환은 패키지 데이터 흐름에서 종종 조회 변환 수행 후 이어지는 경우가 많습니다. 즉, 먼저 조회 변환이 정확히 일치하는 항목을 찾습니다. 이 시도가 실패하면 유사 항목 조회 변환이 수행되어 참조 테이블에서 근접한 항목을 제공합니다.  
  
 변환 작업은 입력 데이터를 정리 및 확장하는 데 사용하는 값을 포함하는 참조 데이터 원본에 액세스해야 합니다. 참조 데이터 원본은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 있는 테이블이어야 합니다. 입력 열의 값과 참조 테이블에 있는 값 사이의 일치 항목은 정확히 일치하는 항목 또는 유사 항목일 수 있습니다. 유사 항목 조회의 경우 변환 작업에는 최소 한 개 이상의 일치하는 열이 있어야 합니다. 정확한 일치만 사용하려는 경우 대신 조회 변환을 사용하십시오.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며  
  
 **DT_WSTR** 및 **DT_STR** 데이터 형식의 입력 열만 유사 일치에서 사용할 수 있습니다. 정확히 일치에는 **DT_TEXT**, **DT_NTEXT**및 **DT_IMAGE**를 제외한 모든 DTS 데이터 형식을 사용할 수 있습니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요. 입력과 참조 테이블 사이에서 조인에 참여하는 열은 호환 가능한 데이터 형식이어야 합니다. 예를 들어 DTS **DT_WSTR** 데이터 형식의 열을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nvarchar** 데이터 형식의 열에 조인하는 것은 유효하지만 **DT_WSTR** 데이터 형식의 열을 **int** 데이터 형식의 열에 조인하는 것은 유효하지 않습니다.  
  
 최대 메모리 양, 행 비교 알고리즘, 변환에서 사용하는 인덱스 및 참조 테이블의 캐싱을 지정하여 이 변환을 사용자 지정할 수 있습니다.  
  
 유사 항목 조회 변환에 사용하는 메모리 크기는 MaxMemoryUsage 사용자 지정 속성을 설정하여 구성할 수 있습니다. 크기(MB)를 지정하거나 값 0을 사용할 수 있습니다. 이렇게 하면 변환에 요구 사항 및 사용 가능한 실제 메모리를 기준으로 하여 동적 메모리 크기를 사용할 수 있습니다. MaxMemoryUsage 사용자 지정 속성은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
## <a name="controlling-fuzzy-matching-behavior"></a>유사 항목 일치 동작의 제어  
 유사 항목 조회 변환이 수행하는 조회를 사용자 지정할 수 있는 기능으로는 각 입력 행당 반환할 수 있는 최대 일치 항목 개수, 토큰 구분 기호 및 유사성 임계값의 세 가지가 있습니다.  
  
 변환은 지정된 최대 일치 항목 개수까지 0개 이상의 일치 항목을 반환합니다. 최대 일치 항목 개수를 지정하면 변환이 항상 최대 일치 항목 개수만큼의 항목을 반환하는 것이 아니라 최대 그만큼의 일치 항목을 반환할 수 있음을 의미합니다. 최대 일치 항목 개수를 1보다 큰 값으로 설정하면 변환의 출력에는 각 조회당 하나 이상의 행이 포함되며 일부 행은 중복될 수 있습니다.  
  
 변환은 데이터를 토큰화하는 데 사용하는 기본 구분 기호 집합을 제공하지만 필요하다면 데이터에 맞는 토큰 구분 기호를 추가할 수 있습니다. 기본 구문 기호는 Delimiters 속성에 포함됩니다. 토큰화는 데이터 내에서 서로 비교되는 단위를 정의하므로 중요합니다.  
  
 유사성 임계값은 구성 요소 및 조인 수준에서 설정할 수 있습니다. 조인 수준의 유사성 임계값은 변환이 입력 열과 참조 테이블 사이에서 유사 항목 일치를 수행하는 경우에만 사용할 수 있습니다. 유사성 범위는 0에서 1 사이입니다. 임계값이 1에 가까울수록 서로 유사한 행과 열이 중복된 것으로 간주되기 쉽습니다. 구성 요소 및 조인 수준에서 MinSimilarity 속성을 설정하여 유사성 임계값을 지정할 수 있습니다. 구성 요소 수준에서 지정한 유사성에 부합하려면 모든 행의 모든 일치에 대한 유사성이 구성 요소 수준에서 지정한 유사성 임계값보다 크거나 같아야 합니다. 즉, 행 또는 조인 수준의 일치가 특정 유사성에 도달하지 못할 경우 구성 요소 수준의 높은 유사성을 지정할 수 없습니다.  
  
 각 일치 항목에는 유사성 점수와 신뢰성 점수가 포함됩니다. 유사성 점수는 입력 레코드와 유사 항목 조회 변환이 참조 테이블에서 반환하는 레코드 사이의 문자적 유사성에 대한 수치적 측정 단위입니다. 신뢰성 점수는 특정 값이 참조 테이블에 있는 일치 항목 중에서 가장 유사한 일치 항목이 될 수 있는 가능성을 측정하는 단위입니다. 레코드에 할당되는 신뢰성 점수는 반환되는 다른 일치 레코드에 따라 달라집니다. 예를 들어 *St.* 및 *Saint* 에 대한 조회는 다른 일치 항목에 관계없이 낮은 유사성 점수를 반환합니다. *Saint* 가 반환되는 유일한 일치 항목인 경우 신뢰성 점수는 높아집니다. 하지만 *Saint* 및 *St.* 가 모두 참조 테이블에 있는 경우 *St.* 에 대한 신뢰성은 높고 *Saint* 에 대한 신뢰성은 낮습니다. 높은 유사성이 높은 신뢰성을 의미하지는 않습니다. 예를 들어 *Chapter 4*값을 조회하는 경우 *Chapter 1*, *Chapter 2*및 *Chapter 3* 의 반환 결과는 높은 유사성 점수를 갖지만 어떤 결과가 가장 일치하는 항목인지 분명하지 않기 때문에 신뢰성 점수는 낮습니다.  
  
 유사성 점수는 0과 1 사이의 소수 값으로 표시되며 여기서 유사성 점수 1은 입력 열의 값과 참조 테이블의 값이 정확히 일치함을 의미합니다. 신뢰성 점수 역시 0과 1 사이의 소수 값으로 표시되며 일치 항목에 대한 신뢰성을 나타냅니다. 사용 가능한 일치 항목이 없는 경우 0의 유사성 및 신뢰성 점수가 해당 행에 할당되고 참조 테이블에서 복사된 출력 열은 Null 값을 포함합니다.  
  
 유사 항목 조회가 참조 테이블에서 적절한 일치 항목을 찾지 못하는 경우도 있습니다. 조회에 사용한 입력 값이 하나의 짧은 단어일 때 이러한 경우가 발생할 수 있습니다. 예를 들어 행에 있는 해당 열 또는 다른 열에 다른 토큰이 열에 없는 경우 *helo* 는 참조 테이블에 있는 *hello* 값과 일치하지 않습니다.  
  
 변환의 출력 열에는 통과 열로 표시된 입력 열, 조회 테이블에서 선택된 열, 그리고 다음과 같은 추가 열이 포함됩니다.  
  
-   **_Similarity**- 입력과 참조 열의 값 사이의 유사성을 나타내는 열입니다.  
  
-   **_Confidence**- 일치 항목의 신뢰성을 나타내는 열입니다.  
  
 변환은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결을 사용하여 유사 항목 조회 알고리즘에 필요한 임시 테이블을 만듭니다.  
  
## <a name="running-the-fuzzy-lookup-transformation"></a>유사 항목 조회 변환의 실행  
 패키지가 변환을 처음 실행할 때 변환은 참조 테이블을 복사하고 정수 데이터 형식의 열을 새 테이블에 추가한 다음 키 열에서 인덱스를 작성합니다. 그런 다음 변환은 참조 테이블의 복사본에서 일치 인덱스라고 하는 인덱스를 작성합니다. 일치 인덱스는 입력 열의 값을 토큰화한 결과를 저장하며 변환은 조회 작업에 토큰을 사용합니다. 일치 인덱스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 있는 테이블입니다.  
  
 패키지가 다시 실행될 때 변환은 기존 일치 인덱스를 사용하거나 새 인덱스를 만들 수 있습니다. 참조 테이블이 정적인 경우 패키지는 반복되는 데이터 정리 세션을 위해 매번 인덱스를 다시 작성하는 비용이 많이 드는 과정을 피해갈 수 있습니다. 기존 인덱스를 사용하도록 선택한 경우 인덱스는 패키지가 처음 실행될 때 만들어집니다. 여러 유사 항목 조회 변환이 같은 참조 테이블을 사용하는 경우 모두 같은 인덱스를 사용할 수 있습니다. 인덱스를 다시 사용하려면 해당 조회 작업이 동일해야 하며 조회가 같은 열을 사용해야 합니다. 인덱스의 이름 및 인덱스를 저장하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결은 사용자 선택이 가능합니다.  
  
 변환이 일치 인덱스를 저장하는 경우 일치 인덱스를 자동으로 유지 관리할 수 있습니다. 이는 참조 테이블에 있는 레코드가 업데이트될 때마다 일치 인덱스도 업데이트됨을 의미합니다. 패키지가 실행될 때 인덱스를 다시 작성할 필요가 없으므로 일치 인덱스를 유지 관리하면 처리 시간을 절약할 수 있습니다. 변환의 일치 인덱스 관리 방법을 지정할 수 있습니다.  
  
 다음 표에서는 일치 인덱스 옵션에 대해 설명합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|새 인덱스를 만들어 저장하고 유지 관리합니다. 변환은 참조 테이블에 트리거를 설치하여 참조 테이블 및 인덱스 테이블이 계속 동기화되도록 유지합니다.|  
|**GenerateAndPersistNewIndex**|새 인덱스를 만들고 저장하지만 유지 관리하지 않습니다.|  
|**GenerateNewIndex**|새 인덱스를 만들지만 저장하지 않습니다.|  
|**ReuseExistingIndex**|기존 인덱스를 다시 사용합니다.|  
  
### <a name="maintenance-of-the-match-index-table"></a>일치 인덱스 테이블의 유지 관리  
 **GenerateAndMaintainNewIndex** 옵션은 참조 테이블에 트리거를 설치하여 일치 인덱스 테이블과 참조 테이블이 계속 동기화되도록 유지합니다. 설치된 트리거를 제거해야 하는 경우 MatchIndexName 속성에서 지정한 이름을 입력 매개 변수 값으로 하여 **sp_FuzzyLookupTableMaintenanceUnInstall** 저장 프로시저를 실행합니다.  
  
 **sp_FuzzyLookupTableMaintenanceUnInstall** 저장 프로시저를 실행하기 전에 유지 관리된 일치 인덱스 테이블을 삭제해서는 안 됩니다. 일치 인덱스 테이블이 삭제되면 참조 테이블의 트리거는 제대로 실행되지 않습니다. 참조 테이블에 대한 모든 후속 업데이트는 참조 테이블의 트리거를 수동으로 제거할 때까지 계속 실패합니다.  
  
 SQL TRUNCATE TABLE 명령은 DELETE 트리거를 호출하지 않습니다. 참조 테이블에서 TRUNCATE TABLE 명령을 사용하면 참조 테이블과 일치 인덱스는 더 이상 동기화되지 않으며 유사 항목 조회 변환이 실패합니다. 일치 인덱스를 유지 관리하는 트리거가 참조 테이블에 설치되어 있으므로 TRUNCATE TABLE 명령 대신 SQL DELETE 명령을 사용해야 합니다.  
  
> [!NOTE]  
>  **유사 항목 조회 변환 편집기** 의 **참조 테이블** 에서 **저장된 인덱스 유지 관리**를 선택하면 변환은 관리 저장 프로시저를 사용하여 인덱스를 유지 관리합니다. 이러한 관리 저장 프로시저는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 CLR(공용 언어 런타임) 통합 기능을 사용합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 CLR 통합은 사용되지 않습니다. **저장된 인덱스 유지 관리** 기능을 사용하려면 CLR 통합을 사용하도록 설정해야 합니다. 자세한 내용은 [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md)을 참조하세요.  
>   
>  **저장된 인덱스 유지 관리** 옵션에는 CLR 통합이 필요하므로 CLR 통합이 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 있는 참조 테이블을 선택하는 경우에만 이 기능이 작동합니다.  
  
## <a name="row-comparison"></a>행 비교  
 유사 항목 조회 변환을 구성하는 경우 변환에서 참조 테이블에서 일치하는 레코드를 찾는 데 사용할 비교 알고리즘을 지정할 수 있습니다. Exhaustive 속성을 **True**로 설정하면 변환에서는 입력의 각 행을 참조 테이블의 모든 행과 비교합니다. 이 비교 알고리즘은 보다 정확한 결과를 생성할 수 있지만 참조 테이블의 행 개수가 많으면 변환이 느리게 수행될 수 있습니다. Exhaustive 속성을 **True**로 설정하면 전체 참조 테이블이 메모리에 로드됩니다. 성능 문제를 방지하려면 패키지 개발 시에만 Exhaustive 속성을 **True** 로 설정하는 것이 좋습니다.  
  
 Exhaustive 속성을 **False**로 설정하면 유사 항목 조회 변환은 입력 레코드와 공통된 인덱싱된 토큰이나 부분 문자열(부분 문자열은 *q-gram*이라고 함)이 하나 이상 있는 일치 항목만 반환합니다. 조회 효율성을 최대화하기 위해 테이블의 각 행에 있는 토큰의 하위 집합만 유사 항목 조회 변환에서 일치 항목을 찾는 데 사용하는 반전된 인덱스 구조에 인덱싱됩니다. 입력 데이터 세트가 작으면 Exhaustive를 **True**로 설정하여 인덱스 테이블에 공통된 토큰이 없는 일치 항목이 누락되지 않도록 합니다.  
  
## <a name="caching-of-indexes-and-reference-tables"></a>인덱스 및 참조 테이블의 캐싱  
 유사 항목 조회 변환을 구성할 때 변환이 자체 작업을 수행하기 전에 메모리에서 인덱스와 참조 테이블을 부분적으로 캐시할지 여부를 지정할 수 있습니다. WarmCaches 속성을 **True**로 설정하면 인덱스와 참조 테이블이 메모리에 로드됩니다. 입력에 여러 행이 있는 경우 WarmCaches 속성을 **True** 로 설정하면 변환의 성능을 향상시킬 수 있습니다. 입력 행 개수가 적은 경우 WarmCaches 속성을 **False** 로 설정하면 큰 인덱스를 더 빨리 다시 사용할 수 있습니다.  
  
## <a name="temporary-tables-and-indexes"></a>임시 테이블 및 인덱스  
 유사 항목 조회 변환은 런타임에 변환이 연결하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 테이블 및 인덱스 등의 임시 개체를 만듭니다. 이러한 임시 테이블 및 인덱스의 크기는 참조 테이블에 있는 행 및 토큰 개수와 유사 항목 조회 변환이 만드는 토큰 개수에 비례하므로 많은 양의 디스크 공간을 소모할 수 있습니다. 변환은 또한 이 임시 테이블을 쿼리합니다. 그러므로 특히 프로덕션 서버가 사용 가능한 디스크 공간을 제한한 경우 유사 항목 조회 변환을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 비-프로덕션 인스턴스에 연결하는 방법을 고려해야 합니다.  
  
 변환에서 사용하는 테이블 및 인덱스가 로컬 컴퓨터에 있는 경우 변환의 성능이 향상될 수 있습니다. 유사 항목 조회 변환에서 사용하는 참조 테이블이 프로덕션 서버에 있는 경우 테이블을 비-프로덕션 서버에 복사하고 복사본을 액세스하도록 유사 항목 조회 변환을 구성하는 방법을 고려해야 합니다. 이렇게 하면 조회 쿼리가 프로덕션 서버의 리소스를 소모하지 않도록 방지할 수 있습니다. 또한 유사 항목 조회 변환이 일치 인덱스를 유지 관리하는 경우, 즉 MatchIndexOptions가 **GenerateAndMaintainNewIndex**로 설정되는 경우 변환은 데이터 정리 작업을 수행하는 동안 참조 테이블을 잠그고 다른 사용자와 애플리케이션이 해당 테이블에 액세스하지 못하게 할 수 있습니다.  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>유사 항목 조회 변환의 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 데이터 흐름 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>유사 항목 조회 변환 편집기(참조 테이블 탭)
  **유사 항목 조회 변환 편집기** 대화 상자의 **참조 테이블** 탭을 사용하여 조회 시 사용할 원본 테이블 및 인덱스를 지정할 수 있습니다. 참조 데이터 원본은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 있는 테이블이어야 합니다.  
  
> [!NOTE]  
>  유사 항목 조회 변환은 참조 테이블의 작업 복사본을 만듭니다. 아래에서 설명하는 인덱스는 일반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인덱스가 아닌 특수 테이블을 사용하여 이 작업 테이블에 생성됩니다. **저장된 인덱스 유지 관리**를 선택하지 않으면 변환에서 기존 원본 테이블을 수정하지 않습니다. 이 경우 변환에서는 참조 테이블에 대한 변경 내용을 기반으로 작업 테이블 및 조회 인덱스 테이블을 업데이트하는 트리거를 참조 테이블에 만듭니다.  
  
> [!NOTE]  
>  유사 항목 조회 변환의 **Exhaustive** 및 **MaxMemoryUsage** 속성은 **유사 항목 조회 변환 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 또한 **MaxOutputMatchesPerInput** 에 대해 100을 초과하는 값은 **고급 편집기**에서만 지정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)의 유사 항목 조회 변환 섹션을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **캐시 없음**  
 목록에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **새 인덱스 생성**  
 변환에서 조회 시 사용할 새 인덱스를 만들도록 지정합니다.  
  
 **참조 테이블 이름**  
 참조(조회) 테이블로 사용할 기존 테이블을 선택합니다.  
  
 **새 인덱스 저장**  
 새 조회 인덱스를 저장하려면 이 옵션을 선택합니다.  
  
 **새 인덱스 이름**  
 새 조회 인덱스를 저장하도록 선택한 경우 해당 인덱스를 설명하는 이름을 입력합니다.  
  
 **저장된 인덱스 유지 관리**  
 새 조회 인덱스를 저장하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 해당 인덱스를 유지 관리하도록 할지 여부를 지정합니다.  
  
> [!NOTE]  
>  **유사 항목 조회 변환 편집기** 의 **참조 테이블** 에서 **저장된 인덱스 유지 관리**를 선택하면 변환은 관리 저장 프로시저를 사용하여 인덱스를 유지 관리합니다. 이러한 관리 저장 프로시저는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 CLR(공용 언어 런타임) 통합 기능을 사용합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 CLR 통합은 사용되지 않습니다. **저장된 인덱스 유지 관리** 기능을 사용하려면 CLR 통합을 사용하도록 설정해야 합니다. 자세한 내용은 [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md)을 참조하세요.  
>   
>  **저장된 인덱스 유지 관리** 옵션에는 CLR 통합이 필요하므로 CLR 통합이 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 있는 참조 테이블을 선택하는 경우에만 이 기능이 작동합니다.  
  
 **기존 인덱스 사용**  
 변환에서 조회 시 기존 인덱스를 사용하도록 지정합니다.  
  
 **기존 인덱스의 이름**  
 목록에서 이전에 만든 조회 인덱스를 선택합니다.  
  
## <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>유사 항목 조회 변환 편집기(열 탭)
  **유사 항목 조회 변환 편집기** 대화 상자의 **열** 탭을 사용하여 입력 및 출력 열의 속성을 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 입력 열을 사용 가능한 조회 열로 끌어 연결합니다. 이러한 열에는 일치하며 지원되는 데이터 형식이 있어야 합니다. 매핑 선을 선택하고 마우스 오른쪽 단추를 클릭하여 [관계 만들기](../../../integration-services/data-flow/transformations/create-relationships.md) 대화 상자에서 매핑을 편집합니다.  
  
 **이름**  
 사용 가능한 입력 열의 이름을 표시합니다.  
  
 **통과**  
 입력 열을 변환의 출력에 포함할지 여부를 지정합니다.  
  
 **사용 가능한 조회 열**  
 확인란을 사용하여 유사 항목 조회 작업을 수행할 열을 선택합니다.  
  
 **조회 열**  
 사용 가능한 참조 테이블 열 목록에서 조회 열을 선택합니다. 선택 내용에 따라 **사용 가능한 조회 열** 테이블의 확인란이 달라집니다. **사용 가능한 조회 열** 테이블에서 열을 선택하면 반환된 일치하는 각 행에 대한 참조 테이블 열 값이 포함된 출력 열이 생성됩니다.  
  
 **출력 별칭**  
 각 조회 열에 대한 출력의 별칭을 입력합니다. 기본값은 추가된 숫자 인덱스 값이 있는 조회 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>유사 항목 조회 변환 편집기(고급 탭)
  **유사 항목 조회 변환 편집기** 대화 상자의 **고급** 탭을 사용하여 유사 항목 조회 매개 변수를 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **조회당 출력에서 일치하는 최대 항목 수**  
 변환에서 각 입력 행에 대해 반환할 수 있는 일치하는 최대 항목 수를 지정합니다. 기본값은 **1**입니다.  
  
 **유사성 임계값**  
 슬라이더를 사용하여 구성 요소 수준에서 유사성 임계값을 설정합니다. 값이 1에 가까울수록 조회 값과 원본 값이 근접하여 일치 항목으로 처리됩니다. 임계값을 높이면 고려할 레코드 수가 감소하기 때문에 비교 속도를 향상시킬 수 있습니다.  
  
 **토큰 구분 기호**  
 변환에서 열 값을 토큰화하는 데 사용하는 구분 기호를 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [조회 변환](../../../integration-services/data-flow/transformations/lookup-transformation.md)   
 [유사 항목 그룹화 변환](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
