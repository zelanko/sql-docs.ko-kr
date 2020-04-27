---
title: 데이터 오류 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827151"
---
# <a name="error-handling-in-data"></a>데이터 오류 처리
  데이터 흐름 구성 요소가 열 데이터에 변환을 적용하거나, 원본에서 데이터를 추출하거나, 데이터를 대상으로 로드할 때 오류가 발생할 수 있습니다. 오류는 주로 예기치 않은 데이터 값으로 인해 발생합니다. 예를 들어 열에 숫자 대신 문자열이 포함되었기 때문에 데이터 변환이 실패하거나, 열의 데이터 형식은 숫자인데 데이터가 날짜여서 데이터베이스 열에 대한 삽입 작업이 실패하거나, 열 값이 0이어서 식 계산이 실패하고 잘못된 수치 연산이 발생할 수 있습니다.  
  
 오류는 일반적으로 다음과 같은 범주에 속합니다.  
  
-   변환으로 인해 유효 숫자나 비유효 숫자가 손실되거나 문자열이 잘리는 경우 발생하는 데이터 변환 오류. 데이터 변환 오류는 요청한 변환이 지원되지 않는 경우에도 발생합니다.  
  
-   런타임 시 계산되는 식이 잘못된 연산을 수행하거나 데이터 값이 누락 또는 잘못되어 구문이 잘못된 경우에 발생하는 식 계산 오류  
  
-   조회 작업이 조회 테이블에서 일치하는 항목을 찾지 못하는 경우에 발생하는 조회 오류  
  
 여러 데이터 흐름 구성 요소에서 지원되는 오류 출력을 통해 들어오고 나가는 데이터의 행 수준 오류를 구성 요소에서 처리하는 방법을 제어할 수 있습니다. 입력 또는 출력의 개별 열에 대해 옵션을 설정하여 잘림이나 오류가 발생할 경우 구성 요소에서 작동하는 방법을 지정합니다. 예를 들어 고객 이름 데이터가 잘린 경우 구성 요소가 실패하지만 덜 중요한 데이터가 포함된 다른 열의 오류는 무시하도록 지정할 수 있습니다.  
  
 오류 출력은 다른 변환의 입력에 연결되거나 오류가 없는 출력과는 다른 대상으로 로드될 수 있습니다. 예를 들어 오류 출력은 빈 열에 대해 문자열을 제공하는 파생 열 변환에 연결될 수 있습니다.  
  
 다음 다이어그램에서는 오류 출력이 포함된 간단한 데이터 흐름을 보여 줍니다.  
  
 ![오류 출력이 있는 데이터 흐름](../media/mw-dts-11.gif "오류 출력이 있는 데이터 흐름")  
  
 데이터 열 외에도 오류 출력에는 **ErrorCode** 및 **ErrorColumn** 열이 포함됩니다. **ErrorCode** 열은 오류를 식별하며 **ErrorColumn** 에는 오류 열의 계보 식별자가 포함됩니다. 이러한 열의 메타데이터를 보려면 오류 출력을 데이터 흐름의 다음 구성 요소로 연결하는 경로를 클릭합니다. **ErrorColumn** 열의 값이 0으로 설정되는 경우도 있습니다. 이는 오류 조건이 단일 열 대신 전체 행에 영향을 주는 경우 발생합니다. 조회 변환에서 조회가 실패하는 경우를 예로 들 수 있습니다.  
  
 자세한 내용은 [데이터 흐름](data-flow.md) 및 [Integration Services 경로](integration-services-paths.md)를 참조하세요.  
  
 Integration Services 오류, 경고 및 기타 메시지 목록은 [Integration Services Error and Message Reference](../integration-services-error-and-message-reference.md)를 참조하십시오.  
  
## <a name="error-and-truncation-options"></a>오류 및 잘림 옵션  
 오류는 오류 또는 잘림의 두 범주로 분류됩니다. 오류는 명확한 실패를 나타내며 NULL 결과를 생성합니다. 이러한 오류에는 데이터 변환 오류 또는 식 계산 오류가 포함될 수 있습니다. 예를 들어 영문자가 포함된 문자열을 숫자로 변환하려고 시도하면 오류가 발생합니다. 캐스트가 잘못되거나 호환되지 않는 데이터 형식을 사용하는 경우 데이터 변환, 식 평가, 변수와 속성 및 데이터 열에 식 결과를 할당하는 작업이 실패할 수 있습니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../expressions/cast-ssis-expression.md), [식에서의 Integration Services 데이터 형식](../expressions/integration-services-data-types-in-expressions.md) 및 [Integration Services 데이터 형식](integration-services-data-types.md)을 참조하세요.  
  
 잘림은 오류보다 덜 심각합니다. 잘림은 사용 가능하거나 심지어 필요한 결과를 생성하기도 합니다. 잘림은 필요에 따라 오류 또는 허용 가능한 조건으로 취급될 수 있습니다. 예를 들어 한 자만 수용할 수 있는 열에 15자의 문자열을 삽입하는 경우 해당 문자열을 잘라내도록 할 수 있습니다.  
  
 원본, 변환 및 대상에서 오류 및 잘림이 처리되는 방법을 구성할 수 있습니다. 다음 표에서는 옵션에 대해 설명합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|구성 요소 실패|오류 또는 잘림이 발생하면 데이터 흐름 태스크가 실패합니다. 실패는 오류 또는 잘림에 대한 기본 옵션입니다.|  
|오류 무시|오류 또는 잘림이 무시되고 데이터 행이 변환 또는 원본의 출력으로 전달됩니다.|  
|행 리디렉션|오류 또는 잘림이 발생한 데이터 행이 원본, 변환 또는 대상의 오류 출력으로 전달됩니다.|  
  
## <a name="adding-the-error-description"></a>오류 설명 추가  
 기본적으로 오류 출력에는 숫자 오류 코드가 제공되며 일반적으로 오류가 발생한 열의 ID가 포함됩니다. 스크립트 구성 요소를 사용하면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 메서드를 호출하는 단일 스크립트 줄을 통해 추가 열에 오류 설명을 포함할 수 있습니다.  
  
 스크립트 구성 요소는 캡처할 오류를 포함하는 데이터 흐름 구성 요소의 임의 다운스트림에서 데이터 흐름의 오류 세그먼트에 추가할 수 있지만 대상에 작성되는 오류 행 바로 앞에 배치하는 것이 일반적입니다. 이렇게 하면 스크립트가 작성된 오류 행에 대한 설명만 조회합니다. 예를 들어 데이터 흐름의 오류 세그먼트가 일부 오류를 수정한 다음 오류 대상에 이러한 행을 쓰지 않을 수 있습니다. 자세한 내용은 [스크립트 구성 요소를 사용 하 여 오류 출력 향상](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)을 참조 하세요.  
  
### <a name="to-configure-an-error-output"></a>오류 출력을 구성하려면  
  
-   [데이터 흐름 구성 요소에서 오류 출력 구성](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](data-flow.md)   
 [변환을 사용 하 여 데이터 변환](transformations/transform-data-with-transformations.md)   
 [경로를 사용 하 여 구성 요소 연결](../connect-components-with-paths.md)   
 [데이터 흐름 태스크](../control-flow/data-flow-task.md)   
 [데이터 흐름](data-flow.md)  
  
  
