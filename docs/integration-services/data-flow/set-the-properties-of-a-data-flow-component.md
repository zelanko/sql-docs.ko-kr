---
title: 데이터 흐름 구성 요소의 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 988675dd00135599fa053acb5cb96d58e81d9e14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628581"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>데이터 흐름 구성 요소의 속성 설정
  원본, 대상 및 변환을 비롯한 데이터 흐름 구성 요소 속성을 설정하려면 다음 기능 중 하나를 사용합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 제공하는 구성 요소 편집기. 이러한 편집기에는 각 데이터 흐름 구성 요소의 사용자 지정 속성만 포함됩니다.  
  
-   **속성** 창에는 각 요소에 대한 구성 요소 수준의 사용자 지정 속성뿐만 아니라 모든 데이터 흐름 요소에 공통적인 속성이 나열됩니다.  
  
-   **고급 편집기** 대화 상자에서는 각 구성 요소의 사용자 지정 속성에 액세스할 수 있습니다. 또한 **고급 편집기** 대화 상자에서는 모든 데이터 흐름 구성 요소에 공통적인 속성(입력, 출력, 오류 출력, 열 및 외부 열의 속성)에 액세스할 수 있습니다.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>구성 요소 편집기를 사용하여 데이터 흐름 구성 요소의 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보고 수정하려는 구성 요소 속성이 들어 있는 데이터 흐름이 포함된 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 구성 요소를 두 번 클릭합니다.  
  
5.  구성 요소 편집기에서 속성 값을 보거나 수정한 후 편집기를 닫습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>속성 창에서 데이터 흐름 구성 요소의 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보고 수정하려는 구성 요소 속성이 들어 있는 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  속성 값을 보거나 수정한 후 **속성** 창을 닫습니다.  
  
    > [!NOTE]  
    >  여러 속성이 읽기 전용이며 수정될 수 없습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>고급 편집기를 사용하여 데이터 흐름 구성 요소의 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보거나 수정하려는 구성 요소가 들어 있는 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 디자이너에서 데이터 흐름 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **고급 편집기 표시**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 입력을 지원하는 데이터 흐름 구성 요소에서는 **고급 편집기**를 사용할 수 없습니다.  
  
5.  **고급 편집기** 대화 상자에서 다음 단계 중 하나를 수행합니다.  
  
    -   구성 요소에서 사용하는 연결을 보고 지정하려면 **연결 관리자** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  **연결 관리자** 탭은 연결 관리자를 사용하여 파일 및 데이터베이스와 같은 데이터 원본에 연결하는 데이터 흐름 구성 요소에서만 사용할 수 있습니다.  
  
    -   구성 요소 수준의 속성을 보고 수정하려면 **구성 요소 속성** 탭을 클릭합니다.  
  
    -   외부 열과 사용 가능한 출력 간의 매핑을 보고 수정하려면 **열 매핑** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  **열 매핑** 탭은 원본 또는 대상을 보거나 편집하는 경우에만 사용할 수 있습니다.  
  
    -   사용 가능한 입력 열 목록을 보고 출력 열의 이름을 업데이트하려면 **입력 열** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  입력 열 탭은 변환 또는 대상에서 작업할 경우에만 사용할 수 있습니다. 자세한 내용은 [Integration Services Transformations](../../integration-services/data-flow/transformations/integration-services-transformations.md)을 참조하세요.  
  
    -   입력, 출력 및 오류 출력의 속성과 여기에 포함된 열의 속성을 보고 수정하려면 **입/출력 속성** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  원본에는 입력이 없습니다. 대상에는 선택적 오류 출력 외에는 출력이 없습니다.  
  
6.  속성 값을 보거나 수정합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  

## <a name="common-properties-of-data-flow-components"></a>데이터 흐름 구성 요소의 공용 속성
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델의 데이터 흐름 개체에는 구성 요소 수준, 입/출력 수준 및 입/출력 열 수준의 공통 속성과 사용자 지정 속성이 있습니다. 많은 속성은 데이터 흐름 엔진이 런타임에 할당하는 읽기 전용 값을 갖습니다.  
  
 이 항목에서는 데이터 흐름 개체의 공용 속성을 나열하고 설명합니다.  
  
-   [Components](#components)  
  
-   [입력](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [출력](#outputs)  
  
-   [출력 열](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 데이터 흐름의 구성 요소는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|구성 요소의 CLSID입니다.|  
|ContactInfo|String|구성 요소 개발자의 연락처 정보입니다.|  
|설명|String|데이터 흐름 구성 요소에 대한 설명입니다. 이 속성의 기본값은 데이터 흐름 구성 요소의 이름입니다.|  
|ID|정수|구성 요소의 인스턴스를 고유하게 식별하는 값입니다.|  
|IdentificationString|String|구성 요소를 식별합니다.|  
|IsDefaultLocale|Boolean|구성 요소가 속해 있는 데이터 흐름 태스크의 로캘이 구성 요소에 사용되는지 여부를 나타냅니다.|  
|LocaleID|정수|패키지가 실행될 때 데이터 흐름 구성 요소에서 사용하는 로캘입니다. 데이터 흐름 구성 요소에는 모든 Windows 로캘을 사용할 수 있습니다.|  
|속성|String|데이터 흐름 구성 요소의 이름입니다.|  
|PipelineVersion|정수|구성 요소가 내부에서 실행되도록 디자인된 데이터 흐름 태스크의 버전입니다.|  
|UsesDispositions|Boolean|구성 요소에 오류 출력이 있는지 여부를 나타냅니다.|  
|ValidateExternalMetadata|Boolean|외부 열 메타데이터의 유효성이 검사되었는지 여부를 나타냅니다. 이 속성의 기본값은 **True**입니다.|  
|버전 옵션|정수|구성 요소의 버전입니다.|  
  
###  <a name="inputs"></a> 입력 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 변환 및 대상은 입력을 포함합니다. 데이터 흐름 구성 요소의 입력은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 입력 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|설명|String|입력에 대한 설명입니다.|  
|ErrorOrTruncationOperation|String|행을 처리할 때 발생할 수 있는 오류 또는 잘림 유형을 지정하는 선택적 문자열입니다.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|오류 처리를 지정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
|HasSideEffects|Boolean|구성 요소가 다운스트림 구성 요소에 연결되어 있지 않은 경우 및 **RunInOptimizedMode** 가 **true**일 경우 데이터 흐름의 실행 계획에서 구성 요소를 제거할 수 있는지 여부를 나타냅니다.|  
|ID|정수|입력을 고유하게 식별하는 값입니다.|  
|IdentificationString|String|입력을 식별하는 문자열입니다.|  
|IsSorted|Boolean|입력의 데이터가 정렬되었는지 여부를 나타냅니다.|  
|속성|String|입력의 이름입니다.|  
|SourceLocale|정수|입력 데이터의 LCID(로캘 ID)입니다.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|행을 처리할 때 발생하는 잘림을 구성 요소가 처리하는 방법을 결정하는 값입니다. 입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
  
 대상 및 일부 변환은 오류 출력을 지원하지 않으므로 이러한 구성 요소의 ErrorRowDisposition 및 TruncationRowDisposition 속성은 읽기 전용입니다.  
  
###  <a name="inputcolumns"></a> 입력 열 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 입력은 입력 열 모음을 포함합니다. 데이터 흐름 구성 요소의 입력 열은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 입력 열 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|ComparisonFlags|정수|문자 데이터 형식을 갖는 열의 비교를 지정하는 플래그 집합입니다. 자세한 내용은 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)을(를) 참조하세요.|  
|설명|String|입력 열에 대해 설명합니다.|  
|ErrorOrTruncationOperation|String|행을 처리할 때 발생할 수 있는 오류 또는 잘림 유형을 지정하는 선택적 문자열입니다.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|오류 처리를 지정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|입력 열에 할당된 외부 메타데이터 열의 ID입니다.|  
|ID|정수|입력 열을 고유하게 식별하는 값입니다.|  
|IdentificationString|String|입력 열을 식별하는 문자열입니다.|  
|LineageID|정수|업스트림 열의 ID입니다.|  
|LineageIdentificationString|String|업스트림 열의 이름을 포함하는 ID 문자열입니다.|  
|속성|String|입력 열의 이름입니다.|  
|SortKeyPosition|정수|열 정렬 여부, 정렬 순서 및 여러 열이 정렬되는 순서를 나타내는 값입니다. 값 **0** 은 열이 정렬되어 있지 않음을 나타냅니다.  자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|행을 처리할 때 발생하는 잘림을 구성 요소가 처리하는 방법을 결정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
|UpstreamComponentName|String|업스트림 구성 요소의 이름입니다.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|입력 열이 구성 요소에서 사용되는 방식을 결정하는 값입니다.|  
  
 입력 열은 "데이터 형식 속성"에 설명된 데이터 형식 속성도 포함합니다.  
  
###  <a name="outputs"></a> 출력 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 원본 및 변환은 출력을 포함합니다. 데이터 흐름 구성 요소의 출력은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 출력 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|경로에서 출력이 분리될 경우 데이터 흐름 엔진이 출력을 삭제할지 여부를 결정하는 값입니다.|  
|설명|String|출력에 대해 설명합니다.|  
|ErrorOrTruncationOperation|String|행을 처리할 때 발생할 수 있는 오류 또는 잘림 유형을 지정하는 선택적 문자열입니다.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|오류 처리를 지정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
|ExclusionGroup|정수|함께 사용할 수 없는 출력 그룹을 식별하는 값입니다.|  
|HasSideEffects|Boolean|구성 요소가 업스트림 구성 요소에 연결되어 있지 않은 경우 및 **RunInOptimizedMode** 가 **true**일 경우 데이터 흐름의 실행 계획에서 구성 요소를 제거할 수 있는지 여부를 나타내는 값입니다.|  
|ID|정수|출력을 고유하게 식별하는 값입니다.|  
|IdentificationString|String|출력을 식별하는 문자열입니다.|  
|IsErrorOut|Boolean|출력이 오류 출력인지 여부를 나타냅니다.|  
|IsSorted|Boolean|출력이 정렬되었는지 여부를 나타냅니다. 기본값은 **False**입니다.<br /><br /> **\*\* 중요 \*\*** **IsSorted** 속성의 값을 **True**로 설정해도 데이터가 졍렬되지는 않습니다. 이 속성은 데이터가 이전에 정렬되었다는 정보를 다운스트림 구성 요소에 제공하기만 합니다. 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.|  
|속성|String|출력의 이름입니다.|  
|SynchronousInputID|정수|출력과 동시에 수행되는 입력의 ID입니다.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|행을 처리할 때 발생하는 잘림을 구성 요소가 처리하는 방법을 결정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다.|  
  
###  <a name="outputcolumns"></a> 출력 열 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 출력은 출력 열 모음을 포함합니다. 데이터 흐름 구성 요소의 출력 열은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 출력 열 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|ComparisonFlags|정수|문자 데이터 형식을 갖는 열의 비교를 지정하는 플래그 집합입니다. 자세한 내용은 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)을(를) 참조하세요.|  
|설명|String|출력 열에 대해 설명합니다.|  
|ErrorOrTruncationOperation|String|행을 처리할 때 발생할 수 있는 오류 또는 잘림 유형을 지정하는 선택적 문자열입니다.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|오류 처리를 지정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다. 기본값은 **Fail component**입니다.|  
|ExternalMetadataColumnID|정수|입력 열에 할당된 외부 메타데이터 열의 ID입니다.|  
|ID|정수|출력 열을 고유하게 식별하는 값입니다.|  
|IdentificationString|String|출력 열을 식별하는 문자열입니다.|  
|LineageID|정수|출력 열의 ID입니다. 다운스트림 구성 요소는 이 값을 사용하여 열을 참조합니다.|  
|LineageIdentificationString|String|열의 이름을 포함하는 ID 문자열입니다.|  
|속성|String|출력 열의 이름입니다.|  
|SortKeyPosition|정수|열 정렬 여부, 정렬 순서 및 여러 열이 정렬되는 순서를 나타내는 값입니다. 값 **0** 은 열이 정렬되어 있지 않음을 나타냅니다. 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.|  
|SpecialFlags|정수|출력 열의 특수 플래그를 포함하는 값입니다.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|행을 처리할 때 발생하는 잘림을 구성 요소가 처리하는 방법을 결정하는 값입니다. 가능한 값은 **Fail component**, **Ignore failure**및 **Redirect row**입니다. 기본값은 **Fail component**입니다.|  
  
 출력 열은 데이터 형식 속성 집합도 포함합니다.  
  
### <a name="external-metadata-column-properties"></a>외부 메타데이터 열 속성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 입력 및 출력은 외부 메타데이터 열 모음을 포함할 수 있습니다. 데이터 흐름 구성 요소의 외부 메타데이터 열은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 인터페이스를 구현합니다.  
  
 다음 표에서는 데이터 흐름 구성 요소의 외부 메타데이터 열 속성에 대해 설명합니다. 일부 속성에는 데이터 흐름 엔진이 런타임에 할당한 읽기 전용 값이 있습니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|설명|String|외부 열에 대해 설명합니다.|  
|ID|정수|열을 고유하게 식별하는 값입니다.|  
|IdentificationString|String|열을 식별하는 문자열입니다.|  
|속성|String|외부 열의 이름입니다.|  
  
 외부 메타데이터 열은 데이터 형식 속성 집합도 포함합니다.  
  
### <a name="data-type-properties"></a>데이터 형식 속성  
 출력 열과 외부 메타데이터 열은 데이터 형식 속성 집합을 포함합니다. 열의 데이터 형식에 따라 읽기/쓰기 속성 또는 읽기 전용 속성이 될 수 있습니다.  
  
 다음 표에서는 출력 열 및 외부 메타데이터 열의 데이터 형식 속성에 대해 설명합니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|CodePage|정수|유니코드가 아닌 문자열 데이터에 대한 코드 페이지를 지정합니다.|  
|DataType|Integer(열거형)|열의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.|  
|길이|정수|열의 길이(문자 수)입니다.|  
|전체 자릿수|정수|숫자 열의 전체 자릿수입니다.|  
|소수 자릿수|정수|숫자 열의 소수 자릿수입니다.|  

## <a name="custom-properties-of-data-flow-components"></a>데이터 흐름 구성 요소의 사용자 지정 속성
사용자 지정 속성에 자세한 내용은 다음 항목을 참조하세요.  
  
-   [ADO.NET 사용자 지정 속성](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [CDC 제어 태스크 사용자 지정 속성](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [CDC 원본 사용자 지정 속성](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [데이터 마이닝 모델 학습 대상 사용자 지정 속성](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [DataReader 대상 사용자 지정 속성](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [차원 처리 대상 사용자 지정 속성](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Excel 사용자 지정 속성](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [플랫 파일 사용자 지정 속성](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [ODBC 대상 사용자 지정 속성](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [ODBC 원본 사용자 지정 속성](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)OLE DB 사용자 지정 속성  
  
-   [파티션 처리 대상 사용자 지정 속성](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [원시 파일 사용자 지정 속성](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [레코드 집합 대상 사용자 지정 속성](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [SQL Server Compact Edition 대상 사용자 지정 속성](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [SQL Server 대상 사용자 지정 속성](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [변환 사용자 지정 속성](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [XML 원본 사용자 지정 속성](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 식 사용
이 절차에서는 조건부 분할 변환 또는 파생 열 변환에 식을 추가하는 방법을 설명합니다. 조건부 분할 변환에서는 데이터 행을 변환 출력으로 바꾸는 조건을 정의하는 데 식을 사용하며 파생 열 변환에서는 열에 할당된 값을 정의하는 데 식을 사용합니다.  
  
 변환에서 식을 구현하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 원본이 이미 들어 있어야 합니다. 
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **제어 흐름** 탭을 클릭하고 식을 구현할 데이터 흐름이 포함된 데이터 흐름 태스크를 클릭합니다.  
  
4.  **데이터 흐름** 탭을 클릭하고 **도구 상자** 에서 조건부 분할 변환 또는 파생 열 변환을 디자인 화면으로 끌어 옵니다.  
  
5.  원본 또는 변환의 녹색 연결선을 조건부 분할 변환 또는 파생 열 변환으로 끌어 옵니다.  
  
6.  변환을 두 번 클릭하여 대화 상자를 엽니다.  
  
7.  왼쪽 창에서 **변수** 를 확장하여 시스템 및 사용자 정의 변수를 표시하고 **열** 을 확장하여 변환 입력 열을 표시합니다.  
  
8.  오른쪽 창에서 **수치 연산 함수**, **문자열 함수**, **날짜/시간 함수**, **NULL 함수**, **형식 캐스트**및 **연산자** 를 확장하여 식 문법이 제공하는 함수, 캐스트 및 연산자에 액세스합니다.  
  
9. 변환에 따라 다음 중 하나를 수행하여 식을 작성합니다.  
  
    -   **조건부 분할 변환 편집기** 대화 상자에서 변수, 열, 함수, 연산자 및 캐스트를 **조건** 열로 끌어 옵니다. 또는 **조건** 열에 직접 식을 입력할 수 있습니다.  
  
    -   **파생 열 변환 편집기** 대화 상자에서 변수, 열, 함수, 연산자 및 캐스트를 **식** 열로 끌어 옵니다. 또는 **식** 열에 직접 식을 입력할 수 있습니다.  
  
        > [!NOTE]  
        >  **조건** 열이나 **식** 열에서 포커스가 제거될 때 식 구문이 유효하지 않은 경우 식 텍스트가 강조 표시될 수 있습니다.  
  
10. **확인** 을 클릭하여 대화 상자를 종료합니다.  
  
    > [!NOTE]  
    >  식이 유효하지 않으면 식의 구문 오류를 설명하는 경고가 나타납니다.  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>식으로 설정할 수 있는 데이터 흐름 속성
데이터 흐름 태스크 컨테이너에서 사용할 수 있는 속성 식을 사용하여 데이터 흐름 개체의 특정 속성 값을 지정할 수 있습니다.  
  
 속성 식을 사용하는 방법은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 속성 식을 사용하여 배포된 패키지의 각 인스턴스 구성을 사용자 지정할 수 있습니다. 또한 속성 식을 사용하여 **dtexec** 명령 프롬프트 유틸리티로 **/set** 옵션을 사용해 패키지의 런타임 제약 조건을 지정할 수도 있습니다. 예를 들어 정렬 변환에 사용된 **MaximumThreads** 또는 유사 항목 그룹화 및 유사 항목 조회 변환의 **MaxMemoryUsage** 를 제약할 수 있습니다. 제약 받지 않을 경우 이러한 변환은 메모리에 대량의 데이터를 캐시할 수 있습니다.  
  
 이 항목에 나열된 데이터 흐름 개체의 속성 중 하나에 대한 속성 식을 지정하려면 디자이너의 **제어 흐름** 화면에서 데이터 흐름 태스크를 선택하거나 개별 구성 요소나 경로를 선택하지 않고 디자이너의 **데이터 흐름** 탭을 선택하여 데이터 흐름 태스크에 대한 **속성** 창을 표시합니다. **식** 속성을 선택하고 줄임표(...)를 클릭하여 **속성 식 편집기** 대화 상자를 표시합니다. **속성** 목록을 드롭다운하여 속성을 선택한 다음 **식** 입력란에 식을 입력하거나 줄임표(...)를 클릭하여 **식 작성기** 대화 상자를 표시합니다.  
  
 **속성** 목록에는 디자이너의 **데이터 흐름** 화면에 이미 배치한 이러한 데이터 흐름 개체에 사용할 수 있는 속성만 표시됩니다. 따라서 **속성** 목록을 사용하여 속성 식을 지원하는 데이터 흐름 개체의 가능한 모든 속성을 확인할 수는 없습니다. 예를 들어 ADO NET 원본을 디자이너 화면에 배치했으면 **속성** 목록에 **[ADO NET Source].[SqlCommand]** 속성에 대한 항목이 포함됩니다. 목록에는 데이터 흐름 태스크 자체의 수많은 속성도 표시됩니다.  
 
 다음 목록의 속성 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
### <a name="data-flow-sources"></a>데이터 흐름 원본  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|ADO.NET 원본|TableOrViewName 속성<br /><br /> SQLCommand 속성|  
|XML 원본|XMLData 속성<br /><br /> XMLSchemaDefinition 속성|  
  
### <a name="data-flow-transformations"></a>데이터 흐름 변환  
 이러한 사용자 지정 속성에 대한 자세한 내용은 [Transformation Custom Properties](../../integration-services/data-flow/transformations/transformation-custom-properties.md)을 참조하십시오.  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|조건부 분할 변환|FriendlyExpression 속성|  
|파생 열 변환|FriendlyExpression 속성|  
|유사 항목 그룹화 변환|MaxMemoryUsage 속성|  
|유사 항목 조회 변환|MaxMemoryUsage 속성|  
|조회 변환|SQLCommand 속성<br /><br /> SqlCommandParam 속성|  
|OLE DB 명령 변환|SQLCommand 속성|  
|비율 샘플링 변환|SamplingValue 속성|  
|피벗 변환|PivotKeyValue 속성|  
|행 샘플링 변환|SamplingValue 속성|  
|정렬 변환|MaximumThreads 속성|  
|피벗 해제 변환|PivotKeyValue 속성|  
  
### <a name="data-flow-destinations"></a>데이터 흐름 대상  
  
|데이터 흐름 개체|속성|  
|----------------------|--------------|  
|ADO.NET 대상|TableOrViewName 속성<br /><br /> BatchSize 속성<br /><br /> CommandTimeout 속성|  
|플랫 파일 대상|Header 속성|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상|TableName 속성|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상|BulkInsertTableName 속성<br /><br /> BulkInsertFirstRow 속성<br /><br /> BulkInsertLastRow 속성<br /><br /> BulkInsertOrder 속성<br /><br /> Timeout 속성|  

