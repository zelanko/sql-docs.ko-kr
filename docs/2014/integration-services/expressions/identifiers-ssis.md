---
title: 식별자(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 84a20b15390463d19577ab6ae800bcb7f0579bb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295053"
---
# <a name="identifiers-ssis"></a>식별자(SSIS)
  식에서 식별자는 연산에 사용할 수 있는 열과 변수입니다. 식은 일반 식별자와 정규화된 식별자를 사용할 수 있습니다.  
  
## <a name="regular-identifiers"></a>일반 식별자  
 일반 식별자는 추가 한정자가 필요 없는 식별자입니다. 예를 들어 **AdventureWorks**데이터베이스의 **Contacts** 테이블에 있는 **MiddleName** 열은 일반 식별자입니다.  
  
 일반 식별자 이름은 다음 규칙을 따라야 합니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에서 정의한 문자나 숫자이거나 밑줄(_), @, $ 및 # 문자일 수 있습니다.  
  
> [!IMPORTANT]  
>  공백과 목록에 없는 특수 문자는 일반 식별자에 유효하지 않습니다. 공백과 특수 문자를 사용하려면 일반 식별자 대신 정규화된 식별자를 사용해야 합니다.  
  
## <a name="qualified-identifiers"></a>정규화된 식별자  
 정규화된 식별자는 대괄호로 구분된 식별자입니다. 식별자 이름에 공백이 포함되어 있거나 식별자 이름이 문자나 밑줄로 시작하지 않기 때문에 식별자에 구분 기호가 필요할 수 있습니다. 예를 들어 열 이름이 **Middle Name** 인 경우 대괄호로 묶어서 식에 [Middle Name] 형식으로 써야 합니다.  
  
 식별자 이름에 공백이 있거나 올바른 일반 식별자 이름이 아니면 식별자를 정규화해야 합니다. 식 계산기는 여는 대괄호와 닫는 대괄호([])를 사용하여 식별자를 정규화합니다. 대괄호는 문자열의 시작 위치와 끝 위치에 있습니다. 예를 들어 식별자 5$>는 [5$>]가 됩니다. 대괄호는 열 이름, 변수 이름 및 함수 이름에 사용할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너 대화 상자를 사용하여 식을 작성하면 자동으로 일반 식별자가 대괄호로 묶입니다. 그러나 이름에 잘못된 문자가 포함된 경우에만 대괄호가 필요합니다. 예를 들어 이름이 **MiddleName** 인 열은 대괄호가 없어도 유효합니다.  
  
 대괄호가 포함된 열 이름은 식에서 참조할 수 없습니다. 예를 들어 열 이름 **Column[1]** 은 식에 사용할 수 없습니다. 식에 이 열을 사용하려면 대괄호가 없는 이름으로 바꾸어야 합니다.  
  
## <a name="lineage-identifiers"></a>계보 식별자  
 식은 계보 식별자를 사용하여 열을 참조할 수 있습니다. 계보 식별자는 처음 패키지를 만들 때 자동으로 할당됩니다. **디자이너의** 고급 편집기 **대화 상자에 있는** 열 속성 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 열의 계보 식별자를 볼 수 있습니다.  
  
 계보 식별자를 사용하여 열을 참조하는 경우 해당 식별자에 파운드(#) 문자 접두사를 포함해야 합니다. 예를 들어 계보 식별자가 147인 열은 #147로 참조해야 합니다.  
  
 식이 성공적으로 구문 분석되면 식 계산기는 계보 식별자를 대화 상자에 표시된 열 이름으로 바꿉니다.  
  
## <a name="unique-column-names"></a>고유 열 이름  
 패키지에 사용된 여러 개의 구성 요소가 동일한 이름을 가진 열을 표시할 수 있습니다. 이러한 열을 식에 사용하는 경우 열을 명확히 구분해야만 식이 성공적으로 구문 분석될 수 있습니다. 식 계산기는 열 원본을 식별하기 위한 점 표기법을 지원합니다. 예를 들어 **Age** 라는 이름의 두 개 열은 각각 **FlatFileSource.Age** 와 **OLEDBSource.Age**가 되어 해당 원본이 FlatFileSource 또는 OLEDBSource임을 나타냅니다. 구문 분석기는 정규화된 이름을 단일 열 이름으로 처리합니다.  
  
 원본 구성 요소 이름과 열 이름은 별도로 정규화됩니다. 다음 예에서는 점 표기법에서 대괄호의 올바른 사용을 보여 줍니다.  
  
-   원본 구성 요소 이름에 공백이 포함되어 있습니다.  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   열 이름의 첫 문자가 유효하지 않습니다.  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   원본 구성 요소와 열 이름에 유효하지 않은 문자가 포함되어 있습니다.  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  점 표기법에서 두 요소가 한 쌍의 대괄호로 묶여 있으면 식 계산기는 이 쌍을 원본-열 조합이 아닌 단일 식별자로 해석합니다.  
  
## <a name="variables-in-expressions"></a>식의 변수  
 식에서 참조된 변수는 @ 접두사를 포함해야 합니다. 예를 들어 **Counter** 변수는 @Counter를 사용하여 참조합니다. @ 문자는 변수 이름의 일부가 아니라 식 계산기에 해당 변수를 식별하는 역할만 합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 제공하는 대화 상자를 사용하여 식을 작성하면 변수 이름에 @ 문자가 자동으로 추가됩니다. @ 문자와 변수 이름 사이에는 공백을 넣을 수 없습니다.  
  
 변수 이름은 다른 일반 식별자의 이름과 동일한 규칙을 따라야 합니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에서 정의한 문자나 숫자이거나 밑줄(_), @, $ 및 # 문자일 수 있습니다.  
  
 목록에 없는 문자가 변수 이름에 포함되어 있으면 해당 변수를 대괄호로 묶어야 합니다. 예를 들어 공백이 포함된 변수 이름은 대괄호로 묶어야 합니다. 여는 대괄호는 @ 문자 뒤에 옵니다. 예를 들어 **My Name** 변수는 @[My Name]으로 참조됩니다. 변수 이름과 대괄호 사이에는 공백을 넣을 수 없습니다.  
  
> [!NOTE]  
>  사용자 정의 변수 및 시스템 변수의 이름은 대/소문자를 구분합니다.  
  
## <a name="unique-variable-names"></a>고유 변수 이름  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 사용자 지정 변수를 지원하며 시스템 변수 집합을 제공합니다. 기본적으로 사용자 지정 변수는 **User** 네임스페이스에 속하고 시스템 변수는 **System** 네임스페이스에 속합니다. 사용자 지정 변수용 네임스페이스를 추가로 만들고 응용 프로그램의 요구에 맞게 기존 네임스페이스 이름을 업데이트할 수 있습니다. 식 작성기는 모든 네임스페이스의 범위 내 변수 목록을 표시합니다.  
  
 모든 변수는 범위를 가지고 있고 하나의 네임스페이스에 속합니다. 변수 범위는 패키지 범위이거나 패키지의 컨테이너 또는 태스크 범위입니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 식 작성기는 범위 내 변수 목록만 표시합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
 식에 사용된 변수의 이름이 고유해야 식 계산기에서 식을 올바로 계산할 수 있습니다. 패키지에서 이름이 같은 변수를 여러 개 사용할 경우 해당 네임스페이스가 서로 달라야 합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 두 개의 콜론으로 구성된(::) 네임스페이스 확인 연산자를 사용하여 네임스페이스로 변수를 정규화합니다. 예를 들어 다음 식에서는 **Count**라는 이름을 가진 변수 두 개를 사용합니다. 하나는 **User** 네임스페이스에 속하고 다른 하나는 **MyNamespace** 네임스페이스에 속합니다.  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  식 계산기에서 변수를 인식할 수 있도록 네임스페이스와 정규화된 변수 이름 조합을 대괄호로 묶어야 합니다.  
  
 경우 값 **개수** 에 **사용자** 네임 스페이스가 10이 고 값 **개수** 에서 **MyNamespace** 가 2 이면 식의 결과가 `true` 식 계산기에서 두 개의 다른 변수를 인식 하므로 합니다.  
  
 고유한 변수 이름을 사용하지 않아도 오류가 발생하지는 않습니다. 대신 식 계산기가 해당 변수의 한 개 인스턴스만 사용하여 식을 계산하고 잘못된 결과를 반환합니다. 예를 들어 다음 식은 하려던 별개의 두 값 (10과 2)을 비교 **개수** 변수 이지만 식 `false` 식 계산기 합니다 의동일한인스턴스를사용하기때문에 **개수** 변수에 두 번입니다.  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>관련 내용  
 pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](http://go.microsoft.com/fwlink/?LinkId=217683)  
  
  
