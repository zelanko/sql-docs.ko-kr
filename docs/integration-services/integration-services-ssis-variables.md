---
title: "Integration Services(SSIS) 변수 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
caps.latest.revision: "60"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 47738020780bb8793c8cfa281815da5be26db222
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
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
  
 SQL 실행 태스크에서 SQL 문의 매개 변수에 변수를 매핑하는 데 사용하는 매개 변수 바인딩에 모든 변수, 즉 시스템 변수와 사용자 정의 변수를 사용할 수 있습니다. 자세한 내용은 [SQL 실행 태스크](../integration-services/control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)를 참조하세요.  
  
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
  
 각 컨테이너 유형에 따라 서로 다른 시스템 변수를 사용할 수 있습니다. 패키지 및 해당 요소에서 사용되는 시스템 변수에 대한 자세한 내용은 [System Variables](../integration-services/system-variables.md)를 참조하십시오.  
  
 변수의 실제 사용 시나리오에 대한 자세한 내용은 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
## <a name="properties-of-variables"></a>변수 속성  
 **변수** 창이나 **속성** 창에서 다음 속성을 설정하여 사용자 정의 변수를 구성할 수 있습니다. 일부 속성은 속성 창에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  시스템 변수에서 구성할 수 있는 유일한 옵션은 값이 변경될 때 이벤트를 발생시키는지 여부를 지정하는 것입니다.  
  
 **Description**    
 변수에 대한 설명을 지정합니다.  
  
 **EvaluateAsExpression**    
 이 속성을 **True**로 설정하면 제공된 식이 변수 값을 설정하는 데 사용됩니다.  
  
 **식**    
 변수에 할당되는 식을 지정합니다.  
  
 **이름**    
 변수 이름을 지정합니다.  
  
 **네임스페이스**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]은 **User** 및 **System**의 두 가지 네임스페이스를 제공합니다. 기본적으로 사용자 지정 변수는 **사용자** 네임스페이스에 속하고 시스템 변수는 **시스템** 네임스페이스에 속합니다. 사용자 정의 변수에 대한 추가 네임스페이스를 만들고 **User** 네임스페이스의 이름을 변경할 수 있지만 **System** 네임스페이스의 이름을 변경하거나, **System** 네임스페이스에 변수를 추가하거나, 시스템 변수를 다른 네임스페이스에 할당할 수 없습니다.  
  
**RaiseChangedEvent**  
 이 속성을 **True**로 설정하면 변수에서 값을 변경할 때 **OnVariableValueChanged** 이벤트가 발생합니다.  
  
 **읽기 전용**  
 이 속성을 **False**로 설정하면 변수는 읽기/쓰기 변수입니다.  
  
**범위**    
 > [!NOTE]  
>  이 속성 설정은 **변수** 창에서 **변수 이동** 을 클릭한 경우에만 변경할 수 있습니다.  
  
 변수는 패키지의 범위나 패키지에 들어 있는 컨테이너, 태스크 또는 이벤트 처리기의 범위 내에서 생성됩니다. 패키지 컨테이너는 컨테이너의 최상위 계층에 있으므로 패키지 범위의 변수는 전역 변수와 같은 기능을 수행하며 패키지의 모든 컨테이너에서 사용될 수 있습니다. 이와 비슷하게 For 루프 컨테이너와 같은 컨테이너의 범위 내에서 정의된 변수는 해당 For 루프 컨테이너 내의 모든 태스크 또는 컨테이너에서 사용될 수 있습니다.  
  
 패키지에서 패키지 실행 태스크를 사용하여 다른 패키지가 실행되는 경우 호출한 패키지 또는 실행 패키지 태스크의 범위 내에서 정의된 변수는 부모 패키지 변수 구성 유형을 통해 호출된 패키지에서 사용할 수 있도록 설정될 수 있습니다. 자세한 내용은 [Package Configurations](../integration-services/packages/package-configurations.md)을 참조하세요.  
  
**IncludeInDebugDump**  
 디버그 덤프 파일에 변수 값이 포함되는지 여부를 나타냅니다.  
  
 사용자 정의 변수 및 시스템 변수의 경우 **InclueInDebugDump** 옵션의 기본값은 **true**입니다.  
  
 그러나 사용자 정의 변수의 경우 다음과 같은 조건이 충족될 때 시스템에서 **IncludeInDebugDump** 옵션을 **false** 로 다시 설정합니다.  
  
-   **EvaluateAsExpression** 변수 속성이 **true**로 설정되면 시스템에서 **IncludeInDebugDump** 옵션을 **false**로 다시 설정합니다.  
  
     디버그 덤프 파일에 식의 텍스트를 변수 값으로 포함하려면 **IncludeInDebugDump** 옵션을 **true**로 설정합니다.  
  
-   변수 데이터 형식이 문자열로 변경되면 시스템에서 **IncludeInDebugDump** 옵션을 **false**로 다시 설정합니다.  
  
 시스템에서 **IncludeInDebugDump** 옵션을 **false**로 다시 설정하면 사용자가 선택한 값이 재정의될 수 있습니다.  
  
**Value**    
 사용자 정의 변수의 값은 문자 또는 식일 수 있습니다. 변수에는 변수 값과 값의 데이터 형식을 설정하기 위한 옵션이 포함됩니다. 이 두 속성은 호환되어야 합니다. 예를 들어 정수 데이터 형식에는 문자열 값을 사용할 수 없습니다.  
  
 변수가 식으로 계산되도록 구성된 경우에는 식을 제공해야 합니다. 런타임에 식이 계산되고 변수에는 해당 계산의 결과가 설정됩니다. 예를 들어 변수에 `DATEPART("month", GETDATE())` 식이 사용된 경우 이 변수의 값은 현재 날짜의 월에 해당하는 숫자입니다. 식은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 식 문법 구문을 사용하는 유효한 식이어야 합니다. 변수에 식이 사용되는 경우 이 식에는 식 문법에서 제공하는 연산자와 함수 및 리터럴을 사용할 수 있지만 식에서 패키지의 데이터 흐름에 있는 열을 참조할 수는 없습니다. 식의 최대 길이는 4000자입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
**ValueType**    
 > [!NOTE]  
>  이 속성 값은 **변수** 창의 **데이터 형식** 열에 표시됩니다.  
  
 변수 값의 데이터 형식을 지정합니다.  

## <a name="scenarios-for-using-variables"></a>변수 사용 시나리오  
 변수는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 다양한 방법으로 사용됩니다. 패키지 개발이 본격적으로 진행되면 솔루션에서 요구하는 유연성과 관리 효율성을 구현하기 위해 사용자 정의 변수를 패키지에 추가하는 작업이 필요할 것입니다. 시나리오에서 따라서는 시스템 변수도 일반적으로 사용됩니다.  
  
 **속성 식** 변수를 사용하여 패키지 및 패키지 개체의 속성을 설정하는 속성 식에 값을 제공할 수 있습니다. 예를 들어 `SELECT * FROM @varTableName` 식에는 SQL 실행 태스크가 실행하는 SQL 문을 업데이트하는 `varTableName` 변수가 포함되어 있습니다. `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" 식은 해당 월의 첫 번째 날에는 `varPackageFirst` 변수에 지정된 패키지를 실행하고 다른 날에는 `varPackageOther` 변수에 지정된 패키지를 실행하여 패키지 실행 태스크에서 실행하는 패키지를 업데이트합니다. 자세한 내용은 [패키지에서 속성 식 사용](../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 **데이터 흐름 식** 변수를 사용하여 파생 열 및 조건부 분할 변환에서 열을 채우기 위해 사용하는 식에 값을 제공하거나 데이터 행을 다른 변환 출력에 전송할 수 있습니다. 예를 들어 `@varSalutation + LastName`식은 `VarSalutation` 변수와 `LastName` 열의 값을 연결합니다. `Income < @HighIncome`식은 `Income` 열의 값이 `HighIncome` 변수의 값보다 작은 데이터 행을 출력에 전송합니다. 자세한 내용은 [파생 열 변환](../integration-services/data-flow/transformations/derived-column-transformation.md), [조건부 분할 변환](../integration-services/data-flow/transformations/conditional-split-transformation.md) 및 [Integration Services&#40;SSIS&#41; 식](../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
 **선행 제약 조건 식** 제약 조건이 지정된 실행 개체가 실행되는지 여부를 결정하기 위해 선행 제약 조건에서 사용할 값을 제공합니다. 식을 실행 결과(성공, 실패, 완료)와 함께 사용하거나 실행 결과 대신에 사용할 수 있습니다. 예를 들어 `@varMax > @varMin`식이 **true**로 계산될 경우 실행 개체가 실행됩니다. 자세한 내용은 [선행 제약 조건에 식 추가](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)를 참조하세요.  
  
 **매개 변수 및 반환 코드** 입력 매개 변수에 대한 값을 제공하거나 출력 매개 변수 및 반환 코드의 값을 저장합니다. 변수를 매개 변수 및 반환 값에 매핑하여 이 작업을 수행합니다. 예를 들어 `varProductId` 변수를 23으로 설정하고 SQL 문 `SELECT * from Production.Product WHERE ProductID = ?`를 실행할 경우 쿼리는 `ProductID` 가 23인 제품을 검색합니다. 자세한 내용은 [SQL 실행 태스크](../integration-services/control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)를 참조하세요.  
  
 **For 루프 식** For 루프의 초기화, 계산 및 대입 식에서 사용할 값을 제공합니다. 예를 들어 `varCount` 변수가 2, `varMaxCount` 변수가 10, 초기화 식이 `@varCount`, 계산 식이  `@varCount < @varMaxCount`, 대입 식이 `@varCount =@varCount +1`인 경우 루프는 8번 반복됩니다. 자세한 내용은 [For Loop Container](../integration-services/control-flow/for-loop-container.md)을 참조하세요.  
  
 **부모 패키지 변수 구성** 부모 패키지에서 자식 패키지로 값을 전달합니다. 자식 패키지는 부모 패키지 변수 구성을 사용하여 부모 패키지의 변수에 액세스할 수 있습니다. 예를 들어 자식 패키지가 부모 패키지와 동일한 데이터를 사용해야 할 경우 자식 패키지는 부모 패키지의 GETDATE 함수에서 설정한 변수를 지정하는 부모 패키지 변수 구성을 정의할 수 있습니다. 자세한 내용은 [Execute Package Task](../integration-services/control-flow/execute-package-task.md) 및 [Package Configurations](../integration-services/packages/package-configurations.md)를 참조하세요.  
  
 **스크립트 태스크 및 스크립트 구성 요소** 스크립트 태스크 또는 스크립트 구성 요소에 대한 읽기 전용 및 읽기/쓰기 변수 목록을 제공하고 스크립트 내에서 읽기/쓰기 변수를 업데이트한 다음 스크립트 내부 또는 외부에서 업데이트된 값을 사용합니다. 예를 들어 `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`코드에서 스크립트 변수 `numberOfCars` 는 `NumberOfCars`변수의 값에 의해 업데이트됩니다. 자세한 내용은 [Using Variables in the Script Task](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)을 참조하세요.  

## <a name="add-a-variable"></a>변수 추가  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 작업하려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  다음 중 하나를 수행하여 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 변수 범위를 정의하십시오.  
  
    -   패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
    -   이벤트 처리기의 범위를 설정하려면 **이벤트 처리기** 탭의 디자인 화면에서 실행 파일 및 이벤트 처리기를 선택합니다.  
  
    -   태스크 또는 컨테이너의 범위를 설정하려면 **제어 흐름** 탭 또는 **이벤트 처리기** 탭의 디자인 화면에서 태스크 또는 컨테이너를 클릭합니다.  
  
4.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
5.  **변수** 창에서 **변수 추가** 아이콘을 클릭합니다. 새 변수가 목록에 추가됩니다.  
  
6.  필요에 따라 **표 옵션** 아이콘을 클릭하고 **가변 눈금 옵션** 대화 상자에 표시할 추가 열을 선택한 다음 **확인**을 클릭합니다.  
  
7.  필요에 따라 변수 속성을 설정합니다. 자세한 내용은 [사용자 정의 변수의 속성 설정](http://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f)을 참조하세요.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

### <a name="add-variable-dialog-box"></a>변수 추가 대화 상자
**변수 추가** 대화 상자를 사용하여 새 변수의 속성을 지정할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **컨테이너**  
 목록에서 컨테이너를 선택합니다. 컨테이너는 변수의 범위를 정의합니다. 컨테이너는 패키지 또는 패키지의 실행 파일일 수 있습니다.  
  
 **이름**  
 변수 이름을 입력합니다.  
  
 **네임스페이스**  
 변수의 네임스페이스를 지정합니다. 기본적으로 사용자 정의 변수는 **User** 네임스페이스에 있습니다.  
  
 **값 유형**  
 데이터 형식을 선택합니다.  
  
 **Value**  
 값을 입력합니다. 이 값은 **값 유형** 옵션에 지정한 데이터 형식과 호환되어야 합니다.  
  
 **읽기 전용**  
 변수를 읽기 전용으로 만들려면 선택합니다.  
   
## <a name="delete-a-variable"></a>변수 삭제  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
4.  삭제할 변수를 선택한 다음 **변수 삭제**를 클릭합니다.  
  
     변수 창에 변수가 표시되지 않는 경우 **표 옵션** 을 클릭하고 **모든 범위의 변수 표시**를 선택합니다.  
  
5.  **변수 삭제 확인** 대화 상자에서 **예** 를 클릭하여 삭제를 확인합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="change-the-scope-of-a-variable"></a>변수의 범위 변경  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
4.  변수를 선택한 다음 **변수 이동**을 클릭합니다.  
  
     변수 창에 변수가 표시되지 않는 경우 **표 옵션** 을 클릭하고 **모든 범위의 변수 표시**를 선택합니다.  
  
5.  **새 범위 선택** 대화 상자에서 변수 범위를 변경할 패키지나 패키지에 들어 있는 컨테이너, 태스크 또는 이벤트 처리기를 선택합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="set-the-properties-of-a-user-defined-variable"></a>사용자 정의 변수의 속성 설정
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 사용자 정의 변수의 속성을 설정하려면 다음 기능 중 하나를 사용합니다.  
  
-   변수 창.  
  
-   속성 창. **속성** 창에는 **변수** 창에서 사용할 수 없는 변수를 구성하기 위한 Description, EvaluateAsExpression, Expression, ReadOnly, ValueType 및 IncludeInDebugDump 속성이 나열됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 속성을 업데이트할 수 없는 시스템 변수 집합도 제공합니다(RaiseChangedEvent 속성은 제외).  
  
### <a name="set-expressions-on-variables"></a>변수의 식 설정  
  
 **속성** 창을 사용하여 사용자 정의 변수의 식을 설정하는 경우 다음을 참조하세요.  
  
-   변수 값은 Value 또는 Expression 속성에서 설정할 수 있습니다. 기본적으로 EvaluateAsExpression 속성은 **False** 로 설정되고 변수 값은 Value 속성에서 설정합니다. 식을 사용하여 값을 설정하려면 먼저 EvaluateAsExpression을 **True**로 설정한 다음 Expression 속성에서 식을 제공합니다. Value 속성은 이 식의 계산 결과로 자동으로 설정됩니다.  
  
-   ValueType 속성에는 Value 속성에 있는 값의 데이터 형식이 포함됩니다. Value가 식에서 설정된 경우 ValueType은 해당 식의 계산 결과와 호환되는 데이터 형식으로 자동으로 업데이트됩니다. 예를 들어 Value에 0이 포함되어 있고 ValueType 속성에 **Int32** 가 포함되어 있으며 Expression을 GETDATE()로 설정할 경우 Value에는 현재 날짜와 시간이 포함되며 ValueType은 **DateTime**으로 설정됩니다.  
  
-   변수에 대한 **속성** 창에서 **식 작성기** 대화 상자에 액세스할 수 있습니다. 이 도구를 사용하여 식 작성, 유효성 검사 및 계산을 수행할 수 있습니다. 자세한 내용은 [식 작성기](../integration-services/expressions/expression-builder.md) 및 [Integration Services&#40;SSIS&#41; 식](../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
 **변수** 창을 사용하여 사용자 정의 변수의 식을 설정하는 경우 다음을 참조하세요.  
  
-   식을 사용하여 변수 값을 설정하려면 먼저 변수 데이터 형식이 식의 계산 결과와 호환되는지 확인한 다음 **변수** 창의 **식** 열에 식을 제공합니다. **속성** 창의 EvaluateAsExpression 속성이 자동으로 **True**로 설정됩니다.  
  
-   변수에 식을 할당할 경우 해당 변수 옆에 특수 아이콘 표식이 표시됩니다. 이 특수 아이콘 표식은 식이 설정되어 있는 연결 관리자 및 태스크 옆에도 표시됩니다.  
  
-   변수에 대한 **변수** 창에서 **식 작성기** 대화 상자에 액세스할 수 있습니다. 이 도구를 사용하여 식 작성, 유효성 검사 및 계산을 수행할 수 있습니다. 자세한 내용은 [식 작성기](../integration-services/expressions/expression-builder.md) 및 [Integration Services&#40;SSIS&#41; 식](../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
 변수에 식을 할당하고 **EvaluateAsExpression** 이 **True** 로 설정된 경우 **변수** 창과 **속성**창 모두에서 변수 데이터 형식을 변경할 수 없습니다.  
  
### <a name="set-the-namespace-and-name-properties"></a>네임스페이스 및 이름 속성 설정
  
 **Name** 및 **Namespace** 속성 값은 Unicode Standard 2.0에 정의된 대로 영문자 또는 밑줄(_)로 시작해야 합니다. 후속 문자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(\_)일 수 있습니다.  
  
### <a name="set-variable-properties-in-the-variables-window"></a>변수 창에서 변수 속성 설정   
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **SSIS** 메뉴에서 **변수**를 클릭합니다.  
  
     **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
4.  필요에 따라 **변수** 창에서 **표 옵션**을 클릭하고 **변수** 창에 표시할 열을 선택한 다음 변수 목록에 적용할 필터를 선택합니다.  
  
5.  목록에서 변수를 선택한 다음 **이름**, **데이터 형식**, **값**, **네임스페이스**, **변경 이벤트 발생**, **설명** 및 **식** 열의 값을 업데이트합니다.  
  
6.  목록에서 변수를 선택하고 **변수 이동** 을 클릭하여 범위를 변경합니다.  
  
7.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
### <a name="set-variable-properties-in-the-properties-window"></a>속성 창에서 변수 속성 설정  

1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **보기** 메뉴에서 **속성 창**을 클릭합니다.  
  
4.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **패키지 탐색기** 탭을 클릭하고 패키지 노드를 확장합니다.  
  
5.  패키지 범위의 변수를 수정하려면 변수 노드를 확장합니다. 그렇지 않으면 수정할 변수가 있는 변수 노드를 찾을 때까지 이벤트 처리기 또는 실행 파일 노드를 확장합니다.  
  
6.  속성을 수정할 변수를 클릭합니다.  
  
7.  **속성** 창에서 읽기/쓰기 변수 속성을 업데이트합니다. 일부 속성은 사용자 정의 변수에 대해 읽기/읽기 전용입니다.  
  
     속성에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  

## <a name="update-a-variable-dynamically-with-configurations"></a>구성에서 변수를 동적으로 업데이트  
 변수를 동적으로 업데이트하려면 변수에 대한 구성을 만들고 패키지와 함께 구성을 배포한 다음 패키지를 배포할 때 구성 파일 내의 변수 값을 업데이트하십시오. 패키지는 런타임에 업데이트된 변수 값을 사용합니다. 자세한 내용은 [패키지 구성 만들기](../integration-services/packages/create-package-configurations.md)를 참조하세요.  

## <a name="related-tasks"></a>관련 태스크  
 [자식 패키지에서 변수 및 매개 변수의 값 사용](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
