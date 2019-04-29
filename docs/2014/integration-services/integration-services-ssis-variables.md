---
title: Integration Services(SSIS) 변수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b824129d1687dce8471800f79d106328b9ee36f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892286"
---
# <a name="integration-services-ssis-variables"></a>Integration Services(SSIS) 변수
  변수에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지와 해당 컨테이너, 태스크 및 이벤트 처리기에서 런타임에 사용할 수 있는 값이 저장됩니다. 스크립트 태스크와 스크립트 구성 요소의 스크립트에서도 변수가 사용될 수 있습니다. 태스크 및 컨테이너의 순서를 워크플로에 지정하는 선행 제약 조건에서는 해당 제약 조건 정의에 식이 포함된 경우에 변수가 사용될 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 변수는 다음 용도로 사용될 수 있습니다.  
  
-   패키지 요소의 속성을 런타임에 업데이트합니다. 예를 들어 Foreach 루프 컨테이너에서 허용하는 동시 실행 파일 수를 동적으로 설정할 수 있습니다.  
  
-   메모리 내 조회 테이블을 포함시킵니다. 예를 들어 패키지에서 데이터 값이 포함된 변수를 로드하는 SQL 실행 태스크가 실행될 수 있습니다.  
  
-   데이터 값이 포함된 변수를 로드하고 이를 사용하여 WHERE 절에서 검색 조건을 지정합니다. 예를 들어 스크립트 태스크의 스크립트는 SQL 실행 태스크의 Transact-SQL 문에서 사용하는 변수 값을 업데이트할 수 있습니다.  
  
-   정수가 포함된 변수를 로드하고 이 값을 사용하여 패키지 제어 흐름 내의 반복 작업을 제어합니다. 예를 들어 For 루프 컨테이너의 계산 식에서 변수를 사용하여 반복 횟수를 제어할 수 있습니다.  
  
-   런타임 시 Transact-SQL 문에 대한 매개 변수 값을 채웁니다. 예를 들어 패키지에서 SQL 실행 태스크를 실행하고 변수를 사용하여 Transact-SQL 문의 매개 변수를 동적으로 설정할 수 있습니다.  
  
-   변수 값이 포함된 식을 작성합니다. 예를 들어 파생 열 변환에서 변수 값을 열 값으로 곱하여 얻은 결과를 열에 채울 수 있습니다.  
  
## <a name="system-and-user-defined-variables"></a>시스템 및 사용자 정의 변수  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 사용자 정의 변수와 시스템 변수라는 두 가지 유형의 변수를 지원합니다. 사용자 정의 변수는 패키지 개발자에 의해 정의되며 시스템 변수는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 의해 정의됩니다. 사용자 정의 변수는 패키지에 필요한 만큼 얼마든지 만들 수 있지만 시스템 변수는 추가로 만들 수 없습니다.  
  
 SQL 실행 태스크에서 SQL 문의 매개 변수에 변수를 매핑하는 데 사용하는 매개 변수 바인딩에 모든 변수, 즉 시스템 변수와 사용자 정의 변수를 사용할 수 있습니다. 자세한 내용은 [SQL 실행 태스크](control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하세요.  
  
> [!NOTE]  
>  사용자 정의 변수 및 시스템 변수의 이름은 대/소문자를 구분합니다.  
  
 사용자 정의 변수는 패키지, Foreach 루프 컨테이너, For 루프 컨테이너, 시퀀스 컨테이너, 태스크 및 이벤트 처리기와 같은 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 컨테이너 유형에 대해 만들 수 있습니다. 사용자 정의 변수는 해당 컨테이너에 대한 Variables 컬렉션의 멤버입니다.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 만드는 경우에는 **디자이너의** 패키지 탐색기 **탭에 있는** 변수 [!INCLUDE[ssIS](../includes/ssis-md.md)] 폴더에서 Variables 컬렉션의 멤버를 확인할 수 있습니다. 폴더에는 사용자 정의 변수와 시스템 변수가 나열됩니다.  
  
 사용자 정의 변수는 다음과 같은 방식으로 구성할 수 있습니다.  
  
-   변수에 대한 이름 및 설명을 제공합니다.  
  
-   변수에 대한 네임스페이스를 지정합니다.  
  
-   값이 변경될 때 변수가 이벤트를 발생시킬지 여부를 나타냅니다.  
  
-   변수가 읽기 전용 또는 읽기/쓰기인지 나타냅니다.  
  
-   식의 계산 결과를 사용하여 변수 값을 설정합니다.  
  
-   패키지 범위 또는 태스크와 같은 패키지 개체의 범위의 변수를 만듭니다.  
  
-   변수의 값과 데이터 형식을 지정합니다.  
  
 시스템 변수에서 구성할 수 있는 유일한 옵션은 값이 변경될 때 이벤트를 발생시키는지 여부를 지정하는 것입니다.  
  
 각 컨테이너 유형에 따라 서로 다른 시스템 변수를 사용할 수 있습니다. 패키지 및 해당 요소에서 사용되는 시스템 변수에 대한 자세한 내용은 [System Variables](system-variables.md)를 참조하십시오.  
  
 변수의 실제 사용 시나리오에 대한 자세한 내용은 [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)을 참조하세요.  
  
## <a name="variable-properties"></a>변수 속성  
 **변수** 창이나 **속성** 창에서 다음 속성을 설정하여 사용자 정의 변수를 구성할 수 있습니다. 일부 속성은 속성 창에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  시스템 변수에서 구성할 수 있는 유일한 옵션은 값이 변경될 때 이벤트를 발생시키는지 여부를 지정하는 것입니다.  
  
 Description  
 변수에 대한 설명을 지정합니다.  
  
 EvaluateAsExpression  
 속성이로 설정 된 경우 `True`, 제공 된 식이 변수 값을 설정 하는 데 사용 됩니다.  
  
 식  
 변수에 할당되는 식을 지정합니다.  
  
 이름  
 변수 이름을 지정합니다.  
  
 Namespace  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]은 **User** 및 **System**의 두 가지 네임스페이스를 제공합니다. 기본적으로 사용자 지정 변수는 **사용자** 네임스페이스에 속하고 시스템 변수는 **시스템** 네임스페이스에 속합니다. 사용자 정의 변수에 대한 추가 네임스페이스를 만들고 **User** 네임스페이스의 이름을 변경할 수 있지만 **System** 네임스페이스의 이름을 변경하거나, **System** 네임스페이스에 변수를 추가하거나, 시스템 변수를 다른 네임스페이스에 할당할 수 없습니다.  
  
 RaiseChangedEvent  
 이 속성을 `True`로 설정하면 변수에서 값을 변경할 때 `OnVariableValueChanged` 이벤트가 발생합니다.  
  
 읽기 전용  
 이 속성을 `False`로 설정하면 변수는 읽기/쓰기 변수입니다.  
  
 범위  
 > [!NOTE]  
>  이 속성 설정은 **변수** 창에서 **변수 이동** 을 클릭한 경우에만 변경할 수 있습니다.  
  
 변수는 패키지의 범위나 패키지에 들어 있는 컨테이너, 태스크 또는 이벤트 처리기의 범위 내에서 생성됩니다. 패키지 컨테이너는 컨테이너의 최상위 계층에 있으므로 패키지 범위의 변수는 전역 변수와 같은 기능을 수행하며 패키지의 모든 컨테이너에서 사용될 수 있습니다. 이와 비슷하게 For 루프 컨테이너와 같은 컨테이너의 범위 내에서 정의된 변수는 해당 For 루프 컨테이너 내의 모든 태스크 또는 컨테이너에서 사용될 수 있습니다.  
  
 패키지에서 패키지 실행 태스크를 사용하여 다른 패키지가 실행되는 경우 호출한 패키지 또는 실행 패키지 태스크의 범위 내에서 정의된 변수는 부모 패키지 변수 구성 유형을 통해 호출된 패키지에서 사용할 수 있도록 설정될 수 있습니다. 자세한 내용은 [Package Configurations](../../2014/integration-services/package-configurations.md)을 참조하세요.  
  
 IncludeInDebugDump  
 디버그 덤프 파일에 변수 값이 포함되는지 여부를 나타냅니다.  
  
 사용자 정의 변수 및 시스템 변수의 기본값에 대 한 값을 **InclueInDebugDump** 옵션은 `true`합니다.  
  
 그러나 사용자 정의 변수에 대 한 시스템을 다시 설정 합니다 **IncludeInDebugDump** 옵션을 `false` 다음 조건이 충족 될 때:  
  
-   경우는 **EvaluateAsExpression** 변수 속성이로 설정 되어 `true`, 시스템을 다시 설정 합니다 **IncludeInDebugDump** 옵션을 `false`합니다.  
  
     디버그 덤프 파일에 변수 값으로 식의 텍스트를 포함 하려면 설정 합니다 **IncludeInDebugDump** 옵션을 `true`입니다.  
  
-   변수 데이터 형식이 문자열로 변경 되 면 시스템이 다시 설정 합니다 **IncludeInDebugDump** 옵션을 `false`입니다.  
  
 시스템으로 다시 설정 합니다 **IncludeInDebugDump** 옵션을 `false`, 사용자가 선택한 값이 재정의 될 수 있습니다.  
  
 값  
 사용자 정의 변수의 값은 문자 또는 식일 수 있습니다. 변수에는 변수 값과 값의 데이터 형식을 설정하기 위한 옵션이 포함됩니다. 이 두 속성은 호환되어야 합니다. 예를 들어 정수 데이터 형식에는 문자열 값을 사용할 수 없습니다.  
  
 변수가 식으로 계산되도록 구성된 경우에는 식을 제공해야 합니다. 런타임에 식이 계산되고 변수에는 해당 계산의 결과가 설정됩니다. 예를 들어 변수에 `DATEPART("month", GETDATE())` 식이 사용된 경우 이 변수의 값은 현재 날짜의 월에 해당하는 숫자입니다. 식은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 식 문법 구문을 사용하는 유효한 식이어야 합니다. 변수에 식이 사용되는 경우 이 식에는 식 문법에서 제공하는 연산자와 함수 및 리터럴을 사용할 수 있지만 식에서 패키지의 데이터 흐름에 있는 열을 참조할 수는 없습니다. 식의 최대 길이는 4000자입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
 ValueType  
 > [!NOTE]  
>  이 속성 값은 **변수** 창의 **데이터 형식** 열에 표시됩니다.  
  
 변수 값의 데이터 형식을 지정합니다.  
  
## <a name="configuring-variables"></a>변수 구성  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [변수 창](../../2014/integration-services/variables-window.md)을 참조하세요.  
  
 변수 속성에 대한 자세한 내용과 이러한 변수를 프로그래밍 방식으로 설정하는 방법은 <xref:Microsoft.SqlServer.Dts.Runtime.Variable>을 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [사용자 정의 변수의 속성 설정](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [자식 패키지에서 변수 및 매개 변수의 값 사용](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
