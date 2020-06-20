---
title: 패키지에서 변수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ddf6086306d24c4f92dfef2b9f4522dc2002733f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972593"
---
# <a name="use-variables-in-packages"></a>패키지에서 변수 사용
  변수는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에 추가된 유용하고 융통성 있는 기능입니다. 변수는 패키지 개체 간 및 부모 패키지와 자식 패키지 간 통신을 제공합니다. 식과 스크립트에도 변수를 사용할 수 있습니다.  
  
## <a name="user-defined-variables-and-system-variables"></a>사용자 정의 변수 및 시스템 변수  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 시스템 변수를 제공하고 사용자 정의 변수를 지원합니다. 새 패키지를 만들거나 패키지에 컨테이너 또는 태스크를 추가하거나 이벤트 처리기를 만들면 컨테이너를 위한 시스템 변수 집합이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에 포함됩니다. 시스템 변수는 패키지, 컨테이너, 태스크 또는 이벤트 처리기에 대한 유용한 정보를 포함합니다. 예를 들어 런타임에 **MachineName** 시스템 변수는 패키지가 실행되는 컴퓨터의 이름을 포함하며 **StartTime** 은 패키지 실행이 시작된 시각을 포함합니다. 시스템 변수는 읽기 전용입니다. 자세한 내용은 [System Variables](system-variables.md)을 참조하세요.  
  
 사용자 정의 변수를 만들고 이를 패키지에서 사용할 수 있습니다. [!INCLUDE[ssIS](../includes/ssis-md.md)]에서 사용자 정의 변수는 스크립트, 선행 제약 조건에 사용되는 식, For 루프 컨테이너, 파생 열 변환 및 조건부 분할 변환에 사용되는 식, 속성 값을 업데이트하는 속성 식 등의 다양한 용도에 사용됩니다.  
  
 예를 들어 For 루프 컨테이너의 평가 조건에 사용자 정의 변수를 사용할 수 있습니다. Foreach 루프 컨테이너의 열거자 컬렉션 값을 변수로 매핑할 수 있으며 SQL 실행 태스크가 매개 변수가 있는 SQL 문을 사용하는 경우 해당 문의 매개 변수를 변수로 매핑할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)을 참조하세요.  
  
## <a name="variables-usage-scenarios"></a>변수 사용 시나리오  
 변수는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에서 다양한 방법으로 사용됩니다. 패키지 개발이 본격적으로 진행되면 솔루션에서 요구하는 유연성과 관리 효율성을 구현하기 위해 사용자 정의 변수를 패키지에 추가하는 작업이 필요할 것입니다. 시나리오에서 따라서는 시스템 변수도 일반적으로 사용됩니다.  
  
 **속성 식** 변수를 사용하여 패키지 및 패키지 개체의 속성을 설정하는 속성 식에 값을 제공할 수 있습니다. 예를 들어 `SELECT * FROM @varTableName` 식에는 SQL 실행 태스크가 실행하는 SQL 문을 업데이트하는 `varTableName` 변수가 포함되어 있습니다. `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" 식은 해당 월의 첫 번째 날에는 `varPackageFirst` 변수에 지정된 패키지를 실행하고 다른 날에는 `varPackageOther` 변수에 지정된 패키지를 실행하여 패키지 실행 태스크에서 실행하는 패키지를 업데이트합니다. 자세한 내용은 [패키지에서 속성 식 사용](expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 **데이터 흐름 식** 변수를 사용하여 파생 열 및 조건부 분할 변환에서 열을 채우기 위해 사용하는 식에 값을 제공하거나 데이터 행을 다른 변환 출력에 전송할 수 있습니다. 예를 들어 `@varSalutation + LastName`식은 `VarSalutation` 변수와 `LastName` 열의 값을 연결합니다. `Income < @HighIncome`식은 `Income` 열의 값이 `HighIncome` 변수의 값보다 작은 데이터 행을 출력에 전송합니다. 자세한 내용은 [파생 열 변환](data-flow/transformations/derived-column-transformation.md), [조건부 분할 변환](data-flow/transformations/conditional-split-transformation.md) 및 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
 **선행 제약 조건 식** 제약 조건이 지정된 실행 개체가 실행되는지 여부를 결정하기 위해 선행 제약 조건에서 사용할 값을 제공합니다. 식을 실행 결과(성공, 실패, 완료)와 함께 사용하거나 실행 결과 대신에 사용할 수 있습니다. 예를 들어 `@varMax > @varMin` 식이 `true`로 계산될 경우 실행 개체가 실행됩니다. 자세한 내용은 [선행 제약 조건에 식 추가](control-flow/precedence-constraints.md)를 참조하세요.  
  
 **매개 변수 및 반환 코드** 입력 매개 변수에 대한 값을 제공하거나 출력 매개 변수 및 반환 코드의 값을 저장합니다. 변수를 매개 변수 및 반환 값에 매핑하여 이 작업을 수행합니다. 예를 들어 `varProductId` 변수를 23으로 설정하고 SQL 문 `SELECT * from Production.Product WHERE ProductID = ?`를 실행할 경우 쿼리는 `ProductID` 가 23인 제품을 검색합니다. 자세한 내용은 [SQL 실행 태스크](control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하세요.  
  
 **For 루프 식** For 루프의 초기화, 계산 및 대입 식에서 사용할 값을 제공합니다. 예를 들어 `varCount` 변수가 2, `varMaxCount` 변수가 10, 초기화 식이 `@varCount`, 계산 식이  `@varCount < @varMaxCount`, 대입 식이 `@varCount =@varCount +1`인 경우 루프는 8번 반복됩니다. 자세한 내용은 [For 루프 컨테이너](control-flow/for-loop-container.md)가 될 때까지 워크플로를 반복합니다.  
  
 **부모 패키지 변수 구성** 부모 패키지에서 자식 패키지로 값을 전달합니다. 자식 패키지는 부모 패키지 변수 구성을 사용하여 부모 패키지의 변수에 액세스할 수 있습니다. 예를 들어 자식 패키지가 부모 패키지와 동일한 데이터를 사용해야 할 경우 자식 패키지는 부모 패키지의 GETDATE 함수에서 설정한 변수를 지정하는 부모 패키지 변수 구성을 정의할 수 있습니다. 자세한 내용은 [Execute Package Task](control-flow/execute-package-task.md) 및 [Package Configurations](../../2014/integration-services/package-configurations.md)를 참조하세요.  
  
 **스크립트 태스크 및 스크립트 구성 요소** 스크립트 태스크 또는 스크립트 구성 요소에 대한 읽기 전용 및 읽기/쓰기 변수 목록을 제공하고 스크립트 내에서 읽기/쓰기 변수를 업데이트한 다음 스크립트 내부 또는 외부에서 업데이트된 값을 사용합니다. 예를 들어 `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`코드에서 스크립트 변수 `numberOfCars` 는 `NumberOfCars`변수의 값에 의해 업데이트됩니다. 자세한 내용은 [Using Variables in the Script Task](control-flow/script-task.md)을 참조하세요.  
  
## <a name="configurations-and-variables"></a>구성 및 변수  
 변수를 동적으로 업데이트하려면 변수에 대한 구성을 만들고 패키지와 함께 구성을 배포한 다음 패키지를 배포할 때 구성 파일 내의 변수 값을 업데이트하십시오. 패키지는 런타임에 업데이트된 변수 값을 사용합니다. 자세한 내용은 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)를 참조하세요.  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>사용자 정의 변수를 추가, 수정 및 삭제하려면  
  
-   [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [사용자 정의 변수의 속성 설정](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
