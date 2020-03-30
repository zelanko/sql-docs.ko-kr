---
title: 유사 항목 그룹화 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fuzzygroupingtrans.f1
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e8cec010923591d3fc05ef2920578bdebc4f9f5c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297933"
---
# <a name="fuzzy-grouping-transformation"></a>유사 항목 그룹화 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  유사 항목 그룹화 변환에서는 중복되기 쉬운 데이터 행을 식별하고 데이터 표준화에 사용할 데이터의 중복 행을 선택하여 데이터 정리 태스크를 수행합니다.  
  
> [!NOTE]  
>  성능 및 메모리 제한 사항을 포함하여 유사 항목 그룹화 변환에 대한 자세한 내용은 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(SQL Server Integration Services 2005에서 유사 항목 조회 및 유사 항목 그룹화) 백서를 참조하세요.  
  
 유사 항목 그룹화 변환에는 변환 알고리즘이 작업을 수행하는 데 필요한 임시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블을 만들기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결이 필요합니다. 연결은 데이터베이스에 테이블을 만드는 권한을 가진 사용자로 확인되어야 합니다.  
  
 변환을 구성하려면 중복을 식별하는 데 사용할 입력 열을 선택하고 각 열에 대해 일치 유형으로 유사 항목 일치 또는 정확한 일치를 선택해야 합니다. 정확한 일치를 사용하면 해당 열에 동일한 값을 가진 행만 그룹화됩니다. DT_TEXT, DT_NTEXT 및 DT_IMAGE를 제외한 모든 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식의 열에 정확한 일치를 적용할 수 있습니다. 유사 항목 일치는 비슷한 값을 가진 행을 그룹화합니다. 데이터의 근사 일치 방식은 사용자 정의 유사성 점수에 기반합니다. DT_WSTR 및 DT_STR 데이터 형식을 가진 열만 유사 항목 일치에서 사용할 수 있습니다. 자세한 내용은 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 변환 출력에는 모든 입력 열, 표준화된 데이터를 가진 한 개 이상의 열 및 유사성 점수를 가진 열이 포함됩니다. 점수는 0과 1 사이의 10진수 값입니다. 정식 행의 점수는 1이며 유사 항목 그룹 내 다른 행의 점수는 정식 행과 일치하는 정도를 나타냅니다. 정식 행과 더 비슷하게 일치할수록 점수가 1에 가까워집니다. 유사 항목 그룹에 정식 행과 정확하게 중복되는 행이 포함된 경우 해당 행의 점수는 1입니다. 변환에서는 중복 행을 제거하지 않고 정식 행과 비슷한 행을 연결하는 키를 만들어 그룹화합니다.  
  
 변환에서는 각 입력 열당 다음 추가 열을 포함하여 한 개의 출력 행을 생성합니다.  
  
-   **_key_in**열, 각 행을 고유하게 식별합니다.  
  
-   **_key_out**열, 중복 행의 그룹을 식별합니다. **_key_out** 열은 정식 데이터 행에 **_key_in** 열 값을 가집니다. **_key_out** 에 동일한 값을 가진 행은 동일한 그룹의 일부입니다. 그룹의 **_key_out**값은 정식 데이터 행의 **_key_in** 값에 해당합니다.  
  
-   **_score**, 입력 행 및 정식 행 간의 유사성을 나타내는 0과 1 사이의 값입니다.  
  
 이것은 기본 열 이름이며 다른 이름을 사용하도록 유사 항목 그룹화 변환을 구성할 수 있습니다. 출력에서는 유사 항목 그룹화에 참여하는 각 열에 유사성 점수를 제공합니다.  
  
 유사 항목 그룹화 변환에는 수행할 그룹화를 사용자 지정하는 두 가지 기능인 토큰 구분 기호 및 유사성 임계값이 포함됩니다. 변환에서는 데이터를 토큰화하는 기본 구분 기호 집합을 제공하지만 새 구분 기호를 추가하여 데이터 토큰화 정도를 향상시킬 수 있습니다.  
  
 유사성 임계값은 변환에서 얼마나 엄격하게 중복을 식별하는지를 지정합니다. 유사성 임계값은 구성 요소 및 열 수준에서 설정할 수 있습니다. 열 수준 유사성 임계값은 유사 항목 일치를 수행하는 열에서만 사용할 수 있습니다. 유사성 범위는 0에서 1 사이입니다. 임계값이 1에 가까울수록 서로 유사한 행과 열이 중복된 것으로 간주되기 쉽습니다. 구성 요소 및 열 수준에서 MinSimilarity 속성을 설정하여 행 및 열 사이의 유사성 임계값을 지정하세요. 구성 요소 수준에서 지정된 유사성을 만족하려면 모든 행이 모든 열에 걸쳐 구성 요소 수준에서 지정된 유사성 임계값 보다 크거나 같은 유사성을 가져야 합니다.  
  
 유사 항목 그룹화 변환에서는 유사성 내부 측정값을 계산하고 MinSimilarity에 지정된 값보다 유사도가 떨어지는 행을 그룹화에서 제외합니다.  
  
 다른 최소 유사성 임계값을 사용하고 유사 항목 그룹화 변환을 여러 번 적용하여 데이터에 사용 중인 유사성 임계값을 확인할 수 있습니다. 변환 출력의 점수 열은 런타임에 그룹 내 각 행에 대한 유사성 점수를 포함합니다. 사용자의 데이터에 적절한 유사성 임계값을 알아내는 데 이 값을 사용할 수 있습니다. 유사성을 높이려면 점수 열의 값 보다 큰 값으로 MinSimilarity을 설정해야 합니다.  
  
 유사 항목 그룹화 변환 입력에 열 속성을 설정하여 변환에서 수행하는 그룹화를 사용자 지정할 수 있습니다. 예를 들어 FuzzyComparisonFlags 속성은 변환에서 열에 문자열 데이터를 비교하는 방법을 지정하며 ExactFuzzy 속성은 변환에서 유사 항목 일치를 수행하는지 또는 정확한 일치를 수행하는지를 지정합니다.  
  
 유사 항목 그룹화 변환에서 사용하는 메모리 양은 MaxMemoryUsage 사용자 지정 속성을 설정하여 구성할 수 있습니다. 크기(MB)를 지정하거나 값 0을 사용하여 변환에서 요구 사항 및 사용 가능한 실제 메모리를 기반으로 메모리를 동적으로 사용하도록 할 수 있습니다. MaxMemoryUsage 사용자 지정 속성은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
## <a name="row-comparison"></a>행 비교  
 유사 항목 그룹화 변환을 구성하는 경우 변환에서 변환 입력 내의 행을 비교하는 데 사용할 비교 알고리즘을 지정할 수 있습니다. Exhaustive 속성을 **true**로 설정하면 변환에서는 입력의 모든 각 행을 입력의 다른 행과 비교합니다. 이 비교 알고리즘을 사용하면 더 정확한 결과를 얻을 수 있지만 입력 행의 수가 많으면 변환 성능이 느려집니다. 성능 문제를 방지하려면 패키지 개발 시에만 Exhaustive 속성을 **true** 로 설정하는 것이 좋습니다.  
  
## <a name="temporary-tables-and-indexes"></a>임시 테이블 및 인덱스  
 유사 항목 그룹화 변환에서는 런타임에 변환에서 연결하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 테이블 및 인덱스와 같은 크기가 큰 임시 개체를 만듭니다. 테이블 및 인덱스의 크기는 변환 입력 내 행의 수 및 유사 항목 그룹화 변환에서 만든 토큰의 수에 비례합니다.  
  
 변환은 또한 임시 테이블을 쿼리합니다. 따라서 프로덕션 서버에 사용 가능한 디스크 공간이 제한되는 경우 프로덕션 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 아닌 인스턴스로 유사 항목 그룹화 변환을 연결해야 합니다.  
  
 변환에서 사용하는 테이블 및 인덱스가 로컬 컴퓨터에 있는 경우 변환의 성능이 향상될 수 있습니다.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>유사 항목 그룹화 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 태스크의 속성 설정 방법에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [유사 항목 그룹화 변환을 사용하여 유사한 데이터 행 식별](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>유사 항목 그룹화 변환 편집기(연결 관리자 탭)
  **유사 항목 그룹화 변환 편집기** 대화 상자의 **연결 관리자** 탭을 사용하여 기존 연결을 선택하거나 새 연결을 만들 수 있습니다.  
  
> [!NOTE]  
>  연결에 지정된 서버에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행해야 합니다. 유사 항목 그룹화 변환에서는 변환에 대한 전체 입력만큼 클 수 있는 임시 데이터 개체를 tempdb에 만듭니다. 실행되는 동안 변환에서는 이러한 임시 개체에 대한 서버 쿼리를 실행합니다. 이 작업은 전체적인 서버 성능에 영향을 줄 수 있습니다.  
  
### <a name="options"></a>옵션  
 **캐시 없음**  
 목록 상자를 사용하여 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 단추를 사용하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
## <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>유사 항목 그룹화 변환 편집기(열 탭)
  **유사 항목 그룹화 변환 편집기** 대화 상자의 **열** 탭을 사용하여 중복 값을 가진 행을 그룹화하는 데 사용할 열을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 중복 값을 가진 행을 그룹화하는 데 사용할 입력 열을 이 목록에서 선택합니다.  
  
 **이름**  
 사용 가능한 입력 열 이름을 표시합니다.  
  
 **통과**  
 입력 열을 변환의 출력에 포함할지 여부를 선택합니다. 그룹화에 사용되는 모든 열이 자동으로 출력에 복사됩니다. 이 열을 선택하여 추가 열을 포함할 수 있습니다.  
  
 **입력 열**  
 **사용 가능한 입력 열** 목록에서 이전에 선택한 입력 열 중 하나를 선택합니다.  
  
 **출력 별칭**  
 해당 출력 열을 설명하는 이름을 입력합니다. 기본적으로 출력 열 이름은 입력 열 이름과 같습니다.  
  
 **그룹 출력 별칭**  
 그룹화된 중복의 정식 값이 포함될 열을 설명하는 이름을 입력합니다. 이 출력 열의 기본 이름은 입력 열 이름에 _clean이 추가된 것입니다.  
  
 **일치 유형**  
 유사 항목 일치 또는 정확히 일치를 선택합니다. 유사 항목 일치 유형에서 모든 열이 충분히 유사할 경우 중복 행으로 간주됩니다. 또한 특정 열에 대해 정확히 일치를 지정하면 정확히 일치 열에 동일한 값이 포함된 행만 중복 가능한 것으로 간주됩니다. 따라서 특정 열에 확실하게 오류 없음이나 불일치가 포함되어 있으면 해당 열에 대해 정확히 일치를 지정하여 다른 열에 대한 유사 항목 일치의 정확도를 높일 수 있습니다.  
  
 **최소 유사성**  
 슬라이더를 사용하여 조인 수준에서 유사성 임계값을 설정합니다. 값이 1에 가까울수록 조회 값과 원본 값이 근접하여 일치 항목으로 처리됩니다. 임계값을 높이면 고려할 레코드 수가 감소하기 때문에 비교 속도를 향상시킬 수 있습니다.  
  
 **유사성 출력 별칭**  
 선택한 조인에 대한 유사성 점수가 포함된 새 출력 열의 이름을 지정합니다. 이 값을 비워 놓으면 출력 열이 생성되지 않습니다.  
  
 **숫자**  
 열 데이터 비교 시 선행 및 후행 숫자의 의미를 지정합니다. 예를 들어 선행 숫자가 의미가 있을 경우 "123 Main Street"는 "456 Main Street"와 그룹화되지 않습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Neither**|선행 및 후행 숫자 모두 의미가 없습니다.|  
|**Leading**|선행 숫자만 의미가 있습니다.|  
|**Trailing**|후행 숫자만 의미가 있습니다.|  
|**LeadingAndTrailing**|선행 및 후행 숫자 모두 의미가 있습니다.|  
  
 **비교 플래그**  
 문자열 비교 옵션에 대한 자세한 내용은 [문자열 데이터 비교](../../../integration-services/data-flow/comparing-string-data.md)를 참조하세요.  
  
## <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>유사 항목 그룹화 변환 편집기(고급 탭)
  **유사 항목 그룹화 변환 편집기** 대화 상자의 **고급** 탭을 사용하여 입/출력 열을 지정하고, 유사성 임계값을 설정하고, 구분 기호를 정의할 수 있습니다.  
  
> [!NOTE]  
>  유사 항목 그룹화 변환의 **Exhaustive** 및 **MaxMemoryUsage** 속성은 **유사 항목 그룹화 변환 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)의 유사 항목 그룹화 변환 섹션을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **입력 키 열 이름**  
 각 입력 행에 대한 고유 식별자를 포함하는 출력 열의 이름을 지정합니다. **_key_in** 열에는 각 행을 고유하게 식별하는 값이 있습니다.  
  
 **출력 키 열 이름**  
 중복 행 그룹의 정식 행에 대한 고유 식별자를 포함하는 출력 열의 이름을 지정합니다. **_key_out** 열은 정식 데이터 행의 **_key_in** 값에 해당합니다.  
  
 **유사성 점수 열 이름**  
 유사성 점수를 포함하는 열의 이름을 지정합니다. 유사성 점수는 입력 행과 정식 행의 유사성을 나타내는 0과 1 사이의 값입니다. 정식 행과 더 비슷하게 일치할수록 점수가 1에 가까워집니다.  
  
 **유사성 임계값**  
 슬라이더를 사용하여 유사성 임계값을 설정합니다. 임계값이 1에 가까울수록 두 행이 보다 유사하여 중복으로 처리됩니다. 임계값을 높이면 고려할 레코드 수가 감소하기 때문에 비교 속도를 향상시킬 수 있습니다.  
  
 **토큰 구분 기호**  
 변환에서 데이터 토큰화에 사용할 수 있는 기본 구분 기호 집합을 제공하지만 필요에 따라 목록을 편집하여 구분 기호를 추가 또는 제거할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [유사 항목 조회 변환](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
