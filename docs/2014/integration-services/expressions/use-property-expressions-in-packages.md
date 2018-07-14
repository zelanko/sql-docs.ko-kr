---
title: 패키지에서 속성 식 사용 | Microsoft Docs
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
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- dynamic properties
- updating package properties
- SSIS packages, expressions
- expressions [Integration Services], property expressions
- property expressions [Integration Services]
ms.assetid: a4bfc925-3ef6-431e-b1dd-7e0023d3a92d
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b4d8718e8a30fdc55da6601ad24e54923d9ae526
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289379"
---
# <a name="use-property-expressions-in-packages"></a>패키지에서 속성 식 사용
  속성 식은 런타임에 동적으로 속성을 업데이트하기 위해 속성에 할당한 식입니다. 예를 들어 속성 식을 사용하면 메일 보내기 태스크에서 사용하는 받는 사람 줄에 변수에 저장된 전자 메일 주소를 삽입할 수 있습니다.  
  
 식은 패키지, 태스크, Foreach 루프, For 루프, 시퀀스, Foreach 열거자, 이벤트 처리기, 패키지 또는 프로젝트 수준의 연결 관리자 또는 로그 공급자에 추가할 수 있습니다. 이러한 개체의 읽기/쓰기가 가능한 속성으로 속성 식을 구현할 수 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 또한 데이터 흐름 구성 요소의 일부 사용자 지정 속성에 속성 식을 사용할 수 있습니다. 변수 및 선행 제약 조건은 속성 식을 지원하지 않지만 식을 사용할 수 있는 특수 속성을 포함합니다.  
  
 속성 식은 여러 다른 방법으로 업데이트됩니다.  
  
-   사용자 정의 변수는 패키지 구성에 포함시키고 패키지를 배포할 때 업데이트할 수 있습니다. 속성 식은 런타임에 업데이트된 변수 값을 사용해 계산됩니다.  
  
-   식에 포함된 시스템 변수는 런타임에 업데이트되어 속성 계산 결과를 변경합니다.  
  
-   날짜 및 시간 함수는 런타임에 계산되어 속성 식에 업데이트된 값을 제공합니다.  
  
-   식 내의 변수는 스크립트 태스크 및 스크립트 구성 요소가 실행하는 스크립트에서 업데이트할 수 있습니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 식 언어를 사용하여 식을 작성할 수 있습니다. 식에서는 시스템 변수 또는 사용자 정의 변수를 식 언어에서 제공하는 연산자, 함수 및 형식 변환과 함께 사용할 수 있습니다.  
  
> [!NOTE]  
>  사용자 정의 변수 및 시스템 변수의 이름은 대/소문자를 구분합니다.  
  
 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](integration-services-ssis-expressions.md)을 참조하세요.  
  
 속성 식의 중요한 용도는 배포된 패키지의 각 인스턴스 구성을 사용자 지정하는 것입니다. 이렇게 하면 다른 환경의 패키지 속성을 동적으로 업데이트할 수 있습니다. 예를 들어 연결 관리자의 연결 문자열에 변수를 할당하는 속성 식을 만든 다음 패키지를 배포할 때 런타임에 연결 문자열이 정확한지 확인하고 변수를 업데이트할 수 있습니다. 패키지 구성은 속성 식을 계산하기 전에 로드됩니다.  
  
 속성은 하나의 속성 식만 사용할 수 있고 속성 식은 하나의 속성에만 적용할 수 있습니다. 그러나 여러 동일한 속성 식을 작성하고 다른 속성에 할당할 수 있습니다.  
  
 일부 속성은 열거자의 값을 사용하여 설정됩니다. 속성 식의 열거자 멤버를 참조할 경우 열거자 멤버의 이름에 해당하는 숫자 값을 사용해야 합니다. 예를 들어 속성 식을 설정 하는 경우는 `LoggingMode` 속성의 값을 사용 하는 `DTSLoggingMode` 열거형 속성 식 이름 대신 0, 1 또는 2를 사용 해야 합니다 `Enabled`, `Disabled`, 또는 `UseParentSetting`. 자세한 내용은 [속성 식의 열거 상수](enumerated-constants-in-property-expressions.md)를 참조하세요.  
  
## <a name="property-expression-user-interface"></a>속성 식 사용자 인터페이스  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 빌드하고 관리 하는 속성 식에 대 한 도구 집합을 제공 합니다.  
  
-   **식** 페이지는 태스크용 사용자 지정 편집기, For 루프 컨테이너 및 Foreach 컨테이너에 있습니다. **식** 페이지를 사용하여 식을 편집하고 태스크, Foreach 루프 또는 For 루프에서 사용하는 속성 식의 목록을 볼 수 있습니다.  
  
-   **속성** 창을 사용하여 식을 편집하고 패키지 또는 패키지 개체가 사용하는 속성 식의 목록을 볼 수 있습니다.  
  
-   **속성 식 편집기** 대화 상자를 사용하여 속성 식을 생성, 업데이트 및 삭제할 수 있습니다.  
  
-   **식 작성기** 대화 상자의 그래픽 도구를 사용하여 식을 작성할 수 있습니다. **식 작성기** 대화 상자에서는 검토를 위해 계산 결과를 속성에 할당하지 않고 식을 계산할 수 있습니다.  
  
 다음 다이어그램에서는 속성 식을 추가, 변경 및 제거하는 데 사용하는 사용자 인터페이스를 보여 줍니다.  
  
 ![속성 식에 대한 사용자 인터페이스](../media/ssis-propertyexpressionui.gif "속성 식에 대한 사용자 인터페이스")  
  
 **속성** 창과 **식** 페이지에서 **식** 컬렉션 수준의 찾아보기 단추 **(…)** 를 클릭하여 **속성 식 편집기** 대화 상자를 엽니다. 속성 식 편집기를 사용하여 속성을 식에 매핑하거나 속성 식을 입력할 수 있습니다. 그래픽 식 도구를 사용하여 식을 만든 다음 식의 유효성을 검사하려면 식 수준의 찾아보기 단추 **(...)** 를 클릭하여 **식 작성기** 대화 상자를 연 다음 식을 만들거나 수정하고 필요에 따라 식의 유효성을 검사합니다.  
  
 **속성 식 편집기** 대화 상자에서 **식 작성기** 를 열 수도 있습니다.  
  
#### <a name="to-work-with-property-expressions"></a>속성 식을 사용하려면  
  
-   [속성 식 추가 또는 변경](add-or-change-a-property-expression.md)  
  
### <a name="setting-property-expressions-of-data-flow-components"></a>데이터 흐름 구성 요소의 속성 식 설정  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 생성하면 속성 식을 지원하는 데이터 흐름 구성 요소의 속성이 해당 속성이 속한 데이터 흐름 태스크에 표시됩니다. 데이터 흐름 구성 요소의 속성 식을 추가, 변경 및 제거하려면 데이터 흐름 구성 요소가 속한 데이터 흐름의 데이터 흐름 태스크를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. 속성 창에 속성 식을 사용할 수 있는 데이터 흐름 구성 요소의 속성이 나열됩니다. 예를 들어 SampleCustomer라는 데이터 흐름에서 행 샘플링 변환의 SamplingValue 속성에 대한 속성 식을 만들거나 수정하려면 행 샘플링 변환이 속한 데이터 흐름의 데이터 흐름 태스크를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. [SampleCustomer].[SamplingValue] 형식의 SamplingValue 속성이 속성 창에 나열됩니다.  
  
 속성 창에서 데이터 흐름 구성 요소에 대한 속성 식을 다른 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 개체 유형에 대한 속성 식과 같은 방식으로 추가, 변경 및 제거합니다. 또한 속성 창에서 데이터 흐름 구성 요소에 대한 속성 식을 추가, 변경 또는 제거할 때 사용하는 다양한 대화 상자 및 작성기에 액세스할 수 있습니다. 속성 식으로 업데이트할 수 있는 데이터 흐름 구성 요소의 속성에 대한 자세한 내용은 [Transformation Custom Properties](../data-flow/transformations/transformation-custom-properties.md)을 참조하십시오.  
  
## <a name="loading-property-expressions"></a>속성 식 로드  
 속성 식이 로드되는 시기를 지정하거나 제어할 수 없습니다. 패키지와 패키지 개체의 유효성이 검사되면 속성 식이 평가되고 로드됩니다. 패키지를 저장하고 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 연 다음 실행하면 유효성 검사가 수행됩니다.  
  
 따라서 속성 식을 추가한 후에 패키지를 저장, 실행 또는 다시 열 때까지 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 속성 식을 사용하는 패키지 개체의 업데이트된 속성 값이 표시되지 않습니다.  
  
 연결 관리자, 로그 공급자, 열거자 등의 다른 유형의 개체와 관련된 속성 식도 해당 개체 유형과 연관된 메서드가 호출되면 로드됩니다. 예를 들어 연결 관리자의 속성은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에서 연결 인스턴스를 만들기 전에 로드됩니다.  
  
 속성 식은 패키지 구성이 로드된 후에 로드됩니다. 예를 들어 변수가 해당 구성에 의해 먼저 업데이트된 다음 변수를 사용하는 속성 식이 평가되고 로드됩니다. 즉, 속성 식은 항상 구성에 의해 설정된 변수 값을 사용합니다.  
  
> [!NOTE]  
>  사용할 수 없습니다는 `Set` 옵션을 **dtexec** 속성 식을 채울 수 있는 유틸리티.  
  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 의 속성 식이 평가되고 로드되는 시기를 요약합니다.  
  
|개체 유형|로드 및 평가|  
|-----------------|-----------------------|  
|패키지, Foreach 루프, For 루프, 시퀀스, 태스크 및 데이터 흐름 구성 요소|구성 로드 후<br /><br /> 유효성 검사 전<br /><br /> 실행 전|  
|연결 관리자|구성 로드 후<br /><br /> 유효성 검사 전<br /><br /> 실행 전<br /><br /> 연결 인스턴스 만들기 전|  
|로그 공급자|구성 로드 후<br /><br /> 유효성 검사 전<br /><br /> 실행 전<br /><br /> 로그 열기 전|  
|Foreach 열거자|구성 로드 후<br /><br /> 유효성 검사 전<br /><br /> 실행 전<br /><br /> 각 루프 열거 전|  
  
## <a name="using-property-expressions-in-the-foreach-loop"></a>Foreach 루프에 속성 식 사용  
 Foreach 루프 컨테이너 내에서 사용되는 연결 관리자의 `ConnectionString` 속성 값을 설정하도록 속성 식을 구현하는 것이 유용한 경우가 종종 있습니다. 열거자의 현재 값 루프의 각 반복을 변수에 매핑한, 후 속성 식의 값을 업데이트 하려면이 변수의 값을 사용 수를 `ConnectionString` 속성 동적으로 합니다.  
  
 Foreach 루프에서 사용하는 파일, 다중 파일, 플랫 파일 및 다중 플랫 파일 연결 관리자의 `ConnectionString` 속성과 함께 속성 식을 사용하려는 경우 몇 가지 사항을 고려해야 합니다. `MaxConcurrentExecutables` 속성을 1보다 큰 값이나 -1 값으로 설정하여 여러 실행 파일을 동시에 실행하도록 패키지를 구성할 수 있습니다. 값 -1은 동시에 실행되는 최대 실행 파일 수가 프로세서 수 +2가 되도록 합니다. 실행 파일의 병렬 실행에서 부정적인 결과가 발생하지 않도록 하려면 `MaxConcurrentExecutables` 값을 1로 설정해야 합니다. 하는 경우 `MaxConcurrentExecutables` 의 값을 1로 설정 되지 않은 `ConnectionString` 속성을 보장할 수 없으므로 결과 예측할 수 없습니다.  
  
 예를 들어 Foreach 루프가 폴더에 있는 파일을 열거하고 파일 이름을 검색한 다음 SQL 실행 태스크를 사용하여 각 파일 이름을 테이블에 삽입한다고 가정합니다. `MaxConcurrentExecutables`가 1로 설정되지 않은 경우 SQL 실행 태스크의 인스턴스 두 개가 동시에 테이블에 쓰기를 시도하면 쓰기 충돌이 발생할 수 있습니다.  
  
## <a name="sample-property-expressions"></a>예제 속성 식  
 다음 예제 식에서는 속성 식에서 시스템 변수, 연산자, 함수 및 문자열 리터럴을 사용하는 방법을 보여 줍니다.  
  
### <a name="property-expression-for-the-loggingmode-property-of-a-package"></a>패키지의 LoggingMode 속성에 대한 속성 식  
 다음 속성 식을 사용하여 패키지의 LoggingMode 속성을 설정할 수 있습니다. 이 식은 DAY 및 GETDATE 함수를 사용하여 날짜의 일 부분을 나타내는 정수를 가져옵니다. 일이 1이거나 15이면 로깅이 설정되고 그렇지 않으면 로깅 설정이 해제됩니다. 1 값은 정수 LoggingMode 열거자 멤버와 동등한 `Enabled`, 값 2는 정수 이며 멤버에 해당 `Disabled`합니다. 식에는 열거자 멤버 이름 대신 숫자 값을 사용해야 합니다.  
  
 `DAY((DT_DBTIMESTAMP)GETDATE())==1||DAY((DT_DBTIMESTAMP)GETDATE())==15?1:2`  
  
### <a name="property-expression-for-the-subject-of-an-e-mail-message"></a>전자 메일 메시지의 제목에 속성 식 사용  
 다음 속성 식을 사용하여 메일 보내기 태스크의 Subject 속성을 설정하여 전자 메일 제목을 지정할 수 있습니다. 식에는 문자열 리터럴, 시스템 변수, 연결(+) 및 캐스트 연산자, DATEDIFF 및 GETDATE 함수의 조합을 사용할 수 있습니다. 시스템 변수로는 `PackageName` 및 `StartTime` 변수가 있습니다.  
  
 `"PExpression-->Package: (" + @[System::PackageName] + ") Started:"+  (DT_WSTR, 30) @[System::StartTime] + " Duration:"  +  (DT_WSTR,10) (DATEDIFF( "ss", @[System::StartTime] , GETDATE()  )) + " seconds"`  
  
 패키지 이름이 EmailRowCountPP이고 2005/3/4에 9초 동안 실행된 경우 식이 다음 문자열로 계산됩니다.  
  
 PExpression-->Package: (EmailRowCountPP) Started:3/4/2005 11:06:18 AM Duration:9 seconds.  
  
### <a name="property-expression-for-the-message-of-an-e-mail-message"></a>전자 메일 메시지의 메시지에 속성 식 사용  
 다음 속성 식을 사용하여 메일 보내기 태스크의 MessageSource 속성을 설정할 수 있습니다. 식에는 문자열 리터럴 조합, 사용자 정의 변수 및 연결 (+) 연산자를 사용합니다. 사용자 정의 변수의 이름은 `nasdaqrawrows`, `nyserawrows`및 `amexrawrows`입니다. 문자열 "\n"은 캐리지 리턴을 나타냅니다.  
  
 `"Rows Processed: "  +   "\n" +"   NASDAQ: "  +   (dt_wstr,9)@[nasdaqrawrows]   + "\n" + "   NYSE: "  +  (dt_wstr,9)@[nyserawrows]  + "\n" + "   Amex: "  +  (dt_wstr,9)@[amexrawrows]`  
  
 `nasdaqrawrows` 가 7058이고 `nyserawrows` 가 3528이며 `amexrawrows` 가 1102인 경우 이 식은 다음 문자열로 계산됩니다.  
  
 처리된 행:  
  
 NASDAQ: 7058  
  
 NYSE: 3528  
  
 AMEX: 1102  
  
### <a name="property-expression-for-the-executable-property-of-an-execute-process-task"></a>프로세스 실행 태스크의 Executable 속성용 속성 식  
 다음 속성 식을 사용하여 프로세스 실행 태스크의 Executable 속성을 설정할 수 있습니다. 식에는 문자열 리터럴 조합, 연산자 및 함수를 사용합니다. 다음 식에는 DATEPART와 GETDATE 함수 및 조건부 연산자가 사용되었습니다.  
  
 `DATEPART("weekday", GETDATE()) ==2?"notepad.exe":"mspaint.exe"`  
  
 프로세스 실행 태스크는 오늘이 한 주의 두 번째 날인 경우 notepad.exe를 실행하고 그렇지 않으면 mspaint.exe를 실행합니다.  
  
### <a name="property-expression-for-the-connectionstring-property-of-a-flat-file-connection-manager"></a>플랫 파일 연결 관리자의 ConnectionString 속성용 속성 식  
 다음 속성 식을 사용하여 플랫 파일 연결 관리자의 ConnectionString 속성을 설정할 수 있습니다. 다음 식은 텍스트 파일의 경로를 포함하는 한 개의 사용자 정의 변수 `myfilenamefull`을 사용합니다.  
  
 `@[User::myfilenamefull]`  
  
> [!NOTE]  
>  연결 관리자용 속성 식은 속성 창을 통해서만 액세스할 수 있습니다. 연결 관리자의 속성을 보려면 속성 창이 열려 있을 때 **디자이너의** 연결 관리자 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 영역에서 연결 관리자를 선택하거나 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택해야 합니다.  
  
### <a name="property-expression-for-the-configstring-property-of-a-text-file-log-provider"></a>텍스트 파일 로그 공급자의 ConfigString 속성에 대한 속성 식  
 다음 속성 식을 사용하여 텍스트 파일 로그 공급자의 ConfigString 속성을 설정할 수 있습니다. 이 식에서는 사용할 파일 연결 관리자의 이름이 포함된 단일 사용자 정의 변수 `varConfigString`을 사용합니다. 파일 연결 관리자는 로그 항목이 작성된 텍스트 파일의 경로를 지정합니다.  
  
 `@[User::varConfigString]`  
  
> [!NOTE]  
>  로그 공급자용 속성 식은 속성 창을 통해서만 액세스할 수 있습니다. 로그 공급자의 속성을 보려면 속성 창이 열려 있을 때 **디자이너의** 패키지 탐색기 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 탭에서 로그 공급자를 선택하거나 패키지 탐색기에서 로그 공급자를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭해야 합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   [식 및 구성 강조 표시자(CodePlex 프로젝트)](http://go.microsoft.com/fwlink/?LinkId=146625)  
  
-   social.technet.microsoft.com의 기술 문서 - [SSIS 식 예](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>관련 항목  
 [패키지에서 변수 사용](../use-variables-in-packages.md)  
  
  
