---
title: 느린 변경 차원 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d334d7aac70cdbadef5bdeede6d9f3a53c74caa7
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51638330"
---
# <a name="slowly-changing-dimension-transformation"></a>느린 변경 차원 변환
  느린 변경 차원 변환은 데이터 웨어하우스 차원 테이블의 레코드 업데이트 및 삽입을 조정합니다. 예를 들어 이 변환을 사용하면 AdventureWorks OLTP 데이터베이스의 Production.Products 테이블의 데이터로 [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] 데이터베이스의 DimProduct 테이블의 레코드를 삽입 및 업데이트하는 변환 출력을 구성할 수 있습니다.  
  
> [!IMPORTANT]  
>  느린 변경 차원 마법사에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 연결만 지원합니다.  
  
 느린 변경 차원 변환은 느린 변경 차원을 관리하기 위한 다음과 같은 기능을 제공합니다.  
  
-   들어오는 행과 조회 테이블의 행을 일치시켜서 새로운 행과 기존 행을 식별합니다.  
  
-   변경이 허용되지 않는 경우 변경 내용이 포함된 들어오는 행을 식별합니다.  
  
-   업데이트가 필요한 유추 멤버 레코드를 식별합니다.  
  
-   새로운 레코드 삽입 및 기존 레코드 업데이트가 필요한 기록 변경 내용이 포함된 들어오는 행을 식별합니다.  
  
-   만료된 행을 포함하여 기존 레코드의 업데이트가 필요한 변경 내용이 포함된 들어오는 행을 검색합니다.  
  
 느린 변경 차원 변환은 네 가지 유형의 변경인 변경 특성, 기록 특성, 고정 특성 및 유추 멤버를 지원합니다.  
  
-   변경 특성 변경 내용은 기존 레코드를 덮어씁니다. 이러한 종류의 변경 내용은 Type 1 변경 내용과 동일합니다. 느린 변경 차원 변환은 이러한 행을 **변경 특성 업데이트 내용 출력**이라는 출력으로 보냅니다.  
  
-   기록 특성 변경 내용은 기존 레코드를 업데이트하는 대신 새 레코드를 만듭니다. 기존 레코드에서 허용되는 유일한 변경 내용은 레코드가 현재 상태 또는 만료된 상태인지 여부를 나타내는 열에 대한 업데이트입니다. 이러한 종류의 변경 내용은 Type 2 변경 내용과 동일합니다. 느린 변경 차원 변환은 이러한 행을 **기록 특성 삽입 내용 출력** 및 **새 출력**이라는 출력으로 보냅니다.  
  
-   고정 특성 변경 내용은 열 값이 변경되지 않도록 지정합니다. 느린 변경 차원 변환은 변경 내용을 검색하고 변경 내용이 포함된 행을 **고정 특성 출력**이라는 출력으로 보낼 수 있습니다.  
  
-   유추 멤버는 행이 차원 테이블의 유추 멤버 레코드임을 나타냅니다. 유추 멤버는 팩트 테이블이 아직 로드되지 않은 차원 멤버를 참조하는 경우 존재합니다. 관련 차원 데이터가 있을 것이라는 가정하에 이후 차원 데이터 로드 시에 제공되는 최소한의 유추 멤버 레코드가 생성됩니다. 느린 변경 차원 변환은 이러한 행을 **유추 멤버 업데이트 내용 출력**이라는 출력으로 보냅니다. 유추 멤버에 대한 데이터가 로드되면 새 레코드를 만드는 대신 기존 레코드를 업데이트할 수 있습니다.  
  
> [!NOTE]  
>  느린 변경 차원 변환은 차원 테이블 변경이 필요한 Type 3 변경 내용을 지원하지 않습니다. 고정 특성 업데이트 유형의 열을 식별하면 Type 3 변경 내용이 될 가능성이 있는 데이터 값을 캡처할 수 있습니다.  
  
 런타임 시 느린 변경 차원 변환은 먼저 들어오는 행을 조회 테이블의 레코드와 일치시키려고 시도합니다. 일치 항목이 없으면 들어오는 행이 새 레코드이고, 따라서 느린 변경 차원 변환은 추가 작업을 수행하지 않고 이 행을 **새 출력**으로 보냅니다.  
  
 일치 항목이 있으면 느린 변경 차원 변환은 행에 변경 내용이 들어 있는지 검색합니다. 행에 변경 내용이 있으면, 느린 변경 차원은 각 열에 대한 업데이트 유형을 확인하고 행을 **변경 특성 업데이트 내용 출력**, **고정 특성 출력**, **기록 특성 삽입 내용 출력**또는 **유추 멤버 업데이트 내용 출력**으로 보냅니다. 행이 변경되지 않았으면 느린 변경 차원 변환은 행을 **변경되지 않은 출력**으로 보냅니다.  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>느린 변경 차원 변환 출력  
 느린 변경 차원 변환에는 하나의 입력과 최대 6개의 출력이 포함됩니다. 출력은 행의 업데이트 및 삽입 요구 사항과 일치하는 데이터 흐름의 하위 집합으로 행을 보냅니다. 이 변환은 오류 출력을 지원하지 않습니다.  
  
 다음 표에서는 변환 출력과 이후의 데이터 흐름 요구 사항에 대해 설명합니다. 요구 사항은 느린 변경 차원 마법사에서 만드는 데이터 흐름을 설명합니다.  
  
|출력|설명|데이터 흐름 요구 사항|  
|------------|-----------------|----------------------------|  
|**변경 특성 업데이트 내용 출력**|조회 테이블의 레코드가 업데이트됩니다. 이 출력은 변경 특성 행에 대해 사용됩니다.|OLE DB 명령 변환은 UPDATE 문을 사용하여 레코드를 업데이트합니다.|  
|**고정 특성 출력**|변경되지 않아야 하는 행의 값이 조회 테이블의 값과 일치하지 않습니다. 이 출력은 고정 특성 행에 대해 사용됩니다.|기본 데이터 흐름이 생성되지 않습니다. 고정 특성 열의 변경 내용이 발견되어도 계속되도록 변환이 구성된 경우에는 이러한 행을 캡처하는 데이터 흐름을 만들어야 합니다.|  
|**기록 특성 삽입 내용 출력**|조회 테이블에 일치하는 행이 적어도 한 개 이상 있습니다. “현재”로 표시된 행은 이제 "만료됨"으로 표시해야 합니다. 이 출력은 기록 특성 행에 대해 사용됩니다.|파생 열 변환은 만료된 행과 현재 행을 표시하기 위한 열을 만듭니다. OLE DB 명령 변환은 이제 "만료됨"으로 표시되어야 하는 레코드를 업데이트합니다. 새 열 값이 있는 행은 새 출력으로 전송됩니다. 여기서 해당 행은 삽입되고 "현재"로 표시됩니다.|  
|**유추 멤버 업데이트 내용 출력**|유추 차원 멤버에 대한 행이 삽입됩니다. 이 출력은 유추 멤버 행에 대해 사용됩니다.|OLE DB 명령 변환은 SQL UPDATE 문을 사용하여 레코드를 업데이트합니다.|  
|**새 출력**|조회 테이블에 일치하는 행이 없습니다. 차원 테이블에 행이 추가됩니다. 이 출력은 새 행에 대해 사용되며 기록 특성 행으로 변경됩니다.|파생 열 변환은 현재 행 표시를 설정하고 OLE DB 대상이 행을 삽입합니다.|  
|**변경되지 않은 출력**|조회 테이블의 값이 행 값과 일치합니다. 이 출력은 변경되지 않은 출력에 대해 사용됩니다.|느린 변경 차원 변환에서 아무 작업도 실행되지 않기 때문에 기본 데이터 흐름이 생성되지 않습니다. 이러한 행을 캡처하려면 이 출력에 대한 데이터 흐름을 만들어야 합니다.|  
  
## <a name="business-keys"></a>비즈니스 키  
 느린 변경 차원 변환에는 적어도 하나 이상의 비즈니스 키 열이 필요합니다.  
  
 느린 변경 차원 변환은 Null 비즈니스 키를 지원하지 않습니다. 데이터에 비즈니스 키가 Null인 행이 있으면 해당 행을 데이터 흐름에서 제거해야 합니다. 조건부 분할 변환을 사용하면 비즈니스 키 열에 Null 값이 포함된 행을 필터링할 수 있습니다. 자세한 내용은 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)을 참조하세요.  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>느린 변경 차원 변환의 성능 최적화  
 느린 변경 차원 변환의 성능을 향상하는 방법은 [데이터 흐름 성능 기능](../../../integration-services/data-flow/data-flow-performance-features.md)을 참조하세요.  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>느린 변경 차원 변환 문제 해결  
 느린 변경 차원 변환이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 느린 변경 차원 변환이 수행하는 외부 데이터 원본에 대한 연결, 명령 및 쿼리 문제를 해결할 수 있습니다. 느린 변경 차원 변환이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>느린 변경 차원 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>느린 변경 차원 변환 출력 구성  
 특히 Type 1 및 Type 2 변경 내용이 사용되는 경우에는 차원 테이블의 행 업데이트 및 삽입을 조정하는 태스크가 복잡할 수 있습니다. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너는 느린 변경 차원에 대한 지원을 구성하기 위한 두 가지 방법을 제공합니다.  
  
-   **고급 편집기** 대화 상자에서는 연결을 선택하고, 공용 및 사용자 지정 구성 요소 속성을 설정하고, 입력 열을 선택하고, 6개의 출력에 열 속성을 설정할 수 있습니다. 느린 변경 차원에 대한 지원 구성 태스크를 완료하려면 느린 변경 차원 변환에서 사용되는 출력에 대한 데이터 흐름을 수동으로 만들어야 합니다. 자세한 내용은 [Data Flow](../../../integration-services/data-flow/data-flow.md)을 참조하세요.  
  
-   차원 로드 마법사에서는 단계별 안내에 따라 느린 변경 차원 변환을 구성하고 변환 출력에 대한 데이터 흐름을 작성할 수 있습니다. 느린 변경 차원에 대한 구성을 변경하려면 차원 로드 마법사를 다시 실행하십시오. 자세한 내용은 [느린 변경 차원 마법사를 사용하여 출력 구성](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   blogs.msdn.com의 블로그 항목 - [느린 변경 차원 마법사 최적화](https://go.microsoft.com/fwlink/?LinkId=199481)  
  
  
