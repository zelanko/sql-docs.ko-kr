---
title: 용어 조회 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
- sql13.dts.designer.termlookup.termlookup.f1
- sql13.dts.designer.termlookup.referencetable.f1
- sql13.dts.designer.termlookup.advanced.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 61dad85fb7857b8694712f79b860f58d88e7d650
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291200"
---
# <a name="term-lookup-transformation"></a>용어 조회 변환

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  용어 조회 변환은 변환 입력 열의 텍스트에서 추출된 용어와 참조 테이블에 있는 용어가 일치하는지 확인합니다. 그런 다음 조회 테이블의 용어가 입력 데이터 집합에서 발생한 횟수를 계산하고 해당 개수를 참조 테이블의 용어와 함께 변환 출력의 열에 기록합니다. 이러한 변환은 입력 텍스트를 기준으로 단어 빈도 통계가 모두 포함된 사용자 지정 단어 목록을 만들 때 유용합니다.  
  
 용어 조회 변환은 조회를 수행하기 전에 용어 추출 변환과 동일한 다음과 같은 방식을 사용하여 입력 열의 텍스트에서 단어를 추출합니다.  
  
-   텍스트를 여러 문장으로 구분합니다.  
  
-   문장을 여러 단어로 구분합니다.  
  
-   단어를 기본 형태로 변환합니다.  
  
 용어 조회 변환에서 대/소문자를 구분하여 일치하는 용어를 검색할 수 있도록 구성하여 용어 검색 방법의 사용자 지정 수위를 높일 수 있습니다.  
  
## <a name="matches"></a>일치  
 용어 조회에서는 조회를 수행하고 다음 규칙에 따라 값을 반환합니다.  
  
-   대/소문자 구분 검색을 수행하도록 변환이 구성된 경우 대/소문자가 다른 일치 항목은 무시됩니다. 예를 들어 *student* 와 *STUDENT* 는 별개의 단어로 취급됩니다.  
  
    > [!NOTE]  
    >  소문자로 표기된 단어는 문장 처음에 대문자로 표시된 단어와 일치합니다. 예를 들어 *Student* 가 문장의 첫 단어인 경우 *student* 와 *Student* 는 일치하는 단어로 검색됩니다.  
  
-   명사 또는 명사구의 복수 형태가 참조 테이블에 있는 경우 조회에서는 명사 또는 명사구의 복수 형태만 검색합니다. 예를 들어 모든 *students* 는 *student*와 별개로 카운트됩니다.  
  
-   참조 테이블에 단어의 단수 형태만 있는 경우 단어 또는 구의 단수 및 복수 형태는 모두 단수 형태로 검색됩니다. 예를 들어 조회 테이블에 *student*가 있는 경우 변환에서는 *student* 와 *students*가 검색되며, 두 단어 모두 조회 용어 *student*에 일치하는 단어로 카운트됩니다.  
  
-   입력 열의 텍스트가 분류된 명사구인 경우 명사구의 마지막 단어만 기본 형태로 변환됩니다. 예를 들어 *doctors appointments* 의 분류된 형태는 *doctors appointment*입니다.  
  
 참조 집합에서 겹치는 용어가 조회 항목에 포함되어 있을 경우(즉, 하위 용어가 하나를 초과하는 참조 레코드에 있는 경우) 용어 조회 변환에서는 하나의 조회 결과만 반환합니다. 다음 예에서는 겹치는 하위 용어가 조회 항목에 포함되어 있는 때의 결과를 보여 줍니다. 이 경우 겹치는 하위 용어는 *Windows*이며 두 개의 참조 용어에 들어 있습니다. 그러나 변환에서는 두 개의 결과를 반환하지 않고 *Windows*라는 하나의 참조 용어만 반환합니다. 두 번째 참조 용어인 *Windows 7 Professional*은 반환되지 않습니다.  
  
|항목|값|  
|----------|-----------|  
|입력 용어|Windows 7 Professional|  
|참조 용어|Windows, Windows 7 Professional|  
|출력|Windows|  
  
 용어 조회 변환에서는 특수 문자가 포함된 명사 및 명사구를 검색할 수 있으며 참조 테이블의 데이터에는 이러한 문자가 포함될 수 있습니다. %, @, &, $, #, \*, :, ;, ., **,** , !, ?, \<, >, +, =, ^, ~, |, \\, /, (, ), [, ], {, }, “, ‘ 등이 특수 문자에 해당합니다.  
  
## <a name="data-types"></a>데이터 형식  
 용어 조회 변환에서는 데이터 형식이 DT_WSTR 또는 DT_NTEXT인 열만 사용할 수 있습니다. 열에 텍스트가 있지만 데이터 형식이 다른 경우 데이터 변환으로 데이터 흐름에 DT_WSTR 또는 DT_NTEXT 데이터 형식의 열을 추가하고 열 값을 새 열로 복사할 수 있습니다. 그런 다음 데이터 변환의 출력을 용어 조회 변환에 대한 입력으로 사용할 수 있습니다. 자세한 내용은 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)을 참조하세요.  
  
## <a name="configuration-the-term-lookup-transformation"></a>용어 조회 변환 구성  
 용어 조회 변환 입력 열에는 열의 용도를 나타내는 InputColumnType 속성이 포함됩니다. InputColumnType에는 다음 값이 포함될 수 있습니다.  
  
-   값 0은 열이 출력에만 전달되며 조회에서 사용되지 않음을 나타냅니다.  
  
-   값 1은 열이 조회에서만 사용됨을 나타냅니다.  
  
-   값 2는 열이 출력에 전달되고 조회에서도 사용됨을 나타냅니다.  
  
 InputColumnType 속성이 0이나 2로 설정된 변환 출력 열에는 업스트림 데이터 흐름 구성 요소에 의해 열에 할당된 계보 식별자를 포함하는 열에 대한 CustomLineageID 속성이 포함됩니다.  
  
 용어 조회 변환은 변환 출력에 기본적으로 **Term** 과 **Frequency**라는 두 개의 열을 추가합니다. **Term** 은 조회 테이블의 용어를 포함하고 **Frequency** 는 참조 테이블의 용어가 입력 데이터 집합에서 발생한 횟수를 포함합니다. 이러한 열에는 CustomLineageID 속성이 포함되지 않습니다.  
  
 조회 테이블은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Access 데이터베이스의 테이블이어야 합니다. 용어 추출 변환의 출력이 테이블에 저장되는 경우 이 테이블을 참조 테이블로 사용할 수 있지만 다른 테이블도 사용할 수 있습니다. 플랫 파일, Excel 통합 문서 또는 다른 원본에 있는 텍스트는 용어 조회 변환을 사용하기 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스나 Access 데이터베이스로 가져와야 합니다.  
  
 용어 조회 변환은 별개의 OLE DB 연결을 사용하여 참조 테이블에 연결합니다. 자세한 내용은 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 용어 조회 변환은 완전히 사전 캐시된 모드에서 작동합니다. 용어 조회 변환은 런타임에 참조 테이블로부터 용어를 읽고 변환 입력 행을 처리하기 전에 이를 프라이빗 메모리에 저장합니다.  
  
 입력 열 행의 용어는 반복될 수 있기 때문에 용어 조회 변환의 출력에는 일반적으로 변환 입력보다 많은 수의 행이 포함됩니다.  
  
 이 변환에는 하나의 입력과 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="term-lookup-transformation-editor-term-lookup-tab"></a>용어 조회 변환 편집기(용어 조회 탭)
  **용어 조회 변환 편집기** 대화 상자의 **용어 조회** 탭을 사용하여 입력 열을 참조 테이블의 조회 열로 매핑하고 각 출력 열의 별칭을 제공할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 확인란을 사용하여 변경되지 않은 출력 열로 전달할 입력 열을 선택합니다. 입력 열을 **사용 가능한 참조 열** 목록으로 끌어서 참조 테이블의 조회 열로 매핑할 수 있습니다. 입력 및 조회 열에 일치하는 지원 데이터 형식 DT_NTEXT 또는 DT_WSTR이 있어야 합니다. 매핑 선을 선택하고 마우스 오른쪽 단추를 클릭하여 [관계 만들기](../../../integration-services/data-flow/transformations/create-relationships.md) 대화 상자에서 매핑을 편집합니다.  
  
 **사용 가능한 참조 열**  
 참조 테이블에서 사용 가능한 열을 표시합니다. 일치시킬 용어 목록이 포함된 열을 선택합니다.  
  
 **통과 열**  
 사용 가능한 입력 열 목록에서 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열** 테이블의 확인란이 달라집니다.  
  
 **출력 열 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 열 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 오류 발생의 원인이 되는 행에 대한 오류 처리 옵션을 지정할 수 있습니다.  
  
## <a name="term-lookup-transformation-editor-reference-table-tab"></a>용어 조회 변환 편집기(참조 테이블 탭)
  **용어 조회 변환 편집기** 대화 상자의 **참조 테이블** 탭을 사용하여 참조(조회) 테이블에 대한 연결을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **캐시 없음**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **참조 테이블 이름**  
 목록에서 항목을 골라 데이터베이스의 조회 테이블 또는 뷰를 선택합니다. 테이블 또는 뷰는 원본 열의 텍스트와 비교할 수 있는 기존 용어 목록이 있는 열을 포함해야 합니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 오류 발생의 원인이 되는 행에 대한 오류 처리 옵션을 지정할 수 있습니다.  
  
## <a name="term-lookup-transformation-editor-advanced-tab"></a>용어 조회 변환 편집기(고급 탭)
  **용어 조회 변환 편집기** 대화 상자의 **고급** 탭을 사용하여 조회에서 대/소문자를 구분할지 여부를 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **대/소문자 구분 용어 조회 사용**  
 조회에서 대/소문자를 구분할지 여부를 표시합니다. 기본값은 **False**입니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 대화 상자를 사용하여 오류 발생의 원인이 되는 행에 대한 오류 처리 옵션을 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)   
 [용어 추출 변환](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
