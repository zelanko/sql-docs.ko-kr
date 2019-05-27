---
title: Transact-SQL 디버거 정보 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, Locals Window
- Transact-SQL debugger, Watch Window
- Transact-SQL debugger, Threads Window
- Transact-SQL debugger, Call Stack Window
- Transact-SQL debugger, QuickWatch
- Transact-SQL debugger, viewing information
ms.assetid: b99819cc-f388-41a1-b304-36e78ce24147
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fced8436279b5daa2751b0b4708a62b449d0bcd7
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821838"
---
# <a name="transact-sql-debugger---information"></a>Transact-SQL 디버거 - 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  디버거가 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 실행을 일시 중지할 때마다 여러 디버거 창을 사용하여 현재 실행 상태를 볼 수 있습니다.  
  
## <a name="debugger-windows"></a>디버거 창  
 디버거 모드에서 디버거가 주 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 창 아래쪽에 두 개의 창을 엽니다. 디버거는 이 두 창에 해당 정보를 모두 표시합니다. 각 디버거 창에는 창에 표시되는 정보 집합을 제어하기 위해 선택할 수 있는 탭이 있습니다. 왼쪽 디버거 창에는 **지역**, **조사식1**, **조사식2**, **조사식3**및 **조사식4** 탭이 있습니다. 오른쪽 디버거 창에는 **호출 스택**, **스레드**, **중단점**, **명령 창**및 **출력** 탭이 있습니다.  
  
> [!NOTE]  
>  앞의 설명은 디버거 창의 기본 위치에 적용됩니다. 탭을 끌어 창 사이를 이동하거나 탭의 도킹을 해제하여 원하는 위치에 배치할 수 있는 새 창을 만들 수 있습니다.  
  
 이러한 탭 또는 창의 일부는 기본적으로 활성화되어 있지 않습니다. 다음 방법 중 하나를 수행하여 특정 창을 열 수 있습니다.  
  
-   **디버그** 메뉴에서 **창**을 클릭한 다음 원하는 창을 선택합니다.  
  
-   **디버그** 도구 모음에서 **중단점**을 클릭한 다음 원하는 창을 선택합니다.  
  
## <a name="transact-sql-expressions"></a>Transact-SQL 식  
 식은 변수 또는 매개 변수와 같은 단일 스칼라 값으로 계산되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 절입니다. 왼쪽 디버거 창에서는 식에 현재 할당된 데이터 값을 최대 5개의 탭 또는 창인 **지역, 조사식1**, **조사식2**, **조사식3** 및 **조사식4**에 표시할 수 있습니다.  
  
 **지역** 창에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거의 현재 범위에 있는 지역 변수에 대한 정보가 표시됩니다. **지역** 창에 나열된 식 집합은 디버거가 코드의 서로 다른 부분에서 실행할 때 변경됩니다.  
  
 **간략한 조사식** 및 네 개의 **조사식** 창에 있는 식은 변수의 식별자만 나열합니다. 변수에 숫자를 추가하는 등 단일 값으로 계산되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식 또는 단일 값으로 계산되는 SELECT 문을 지정할 수 있습니다. 이러한 충돌이 발생합니다.  
  
-   @IntegerCounter와 같은 변수 이름입니다.  
  
-   @IntegerCounter + 1 등의 변수에 대한 산술 연산입니다.  
  
-   @FirstName + @LastName과 같은 두 문자 변수에 대한 문자열 연산입니다.  
  
-   SELECT CharCol FROM MyTable WHERE PrimaryKey = 1 등의 단일 값을 반환하는 SELECT 문입니다.  
  
 **간략한 조사식** 창을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식 값을 본 다음 해당 식을 **조사식** 창에 저장할 수 있습니다. **간략한 조사식**에서 식을 선택하려면 **식** 상자에서 식 이름을 선택하거나 입력합니다.  
  
 4개의 **조사식** 창에는 선택한 변수 및 식에 대한 정보가 표시됩니다. **조사식** 창에 나열된 식 집합은 목록에서 식을 추가하거나 삭제할 때까지 변경되지 않습니다.  
  
 **조사식** 창에 식을 추가하려면 **간략한 조사식** 대화 상자에서 **조사식 추가** 를 선택하거나 **조사식** 창에서 빈 행의 **이름** 열에 식 이름을 입력합니다.  
  
 행을 마우스 오른쪽 단추로 클릭한 다음 **값 편집**을 선택하여 **지역**, **조사식** 또는 **간략한 조사식**창에서 변수에 대한 데이터 값을 설정할 수 있습니다. **지역** 창, **조사식** 창 및 **간략한 조사식** 대화 상자의 **값** 열은 모두 텍스트, XML 및 HTML 데이터 시각화 도우미를 지원합니다. 시각화 도우미는 **값** 열의 오른쪽 끝에 있는 돋보기 모양의 데이터 팁으로 표시됩니다. 시각화 도우미를 사용하면 브라우저 창에서 XML 파일을 보는 경우와 같이 데이터 형식과 일치하는 표시 형식으로 텍스트, XML 또는 HTML 데이터 값을 볼 수 있습니다.  
  
 디버그 모드에서 마우스 포인터를 식별자 위로 이동하면 식 이름 및 식의 현재 값이 포함된 **요약 정보** 팝업 창이 표시됩니다. 자세한 내용은 [요약 정보&#40;IntelliSense&#41;](../../relational-databases/scripting/quick-info-intellisense.md)를 참조하세요.  
  
## <a name="breakpoints"></a>중단점  
 **중단점** 창을 사용하여 현재 설정된 중단점을 보고 관리할 수 있습니다. 자세한 내용은 [Transact-SQL 코드 단계별 실행](../../relational-databases/scripting/step-through-transact-sql-code.md)을 참조하세요.  
  
## <a name="call-stacks"></a>호출 스택  
 **호출 스택** 창에는 현재 실행 위치와 원래 쿼리 편집기 창에서 전달된 실행이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈(함수, 저장 프로시저 또는 트리거)을 통해 현재 실행 위치에 도달하는 방법에 대한 정보가 표시됩니다. **호출 스택** 창의 각 행은 스택 프레임이라고 하며 다음 항목 중 하나를 나타냅니다.  
  
-   현재 실행 위치  
  
-   한 모듈에서 다른 모듈로의 호출  
  
-   편집기 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈로의 호출  
  
 스택 순서는 모듈이 호출되는 순서와 반대입니다. 현재 실행 위치는 스택의 맨 위이며 원래 호출 위치는 맨 아래입니다. 스택 프레임의 왼쪽 여백에 있는 노란색 화살표는 디버거가 실행을 일시 중지한 프레임을 식별합니다.  
  
 **이름** 열은 다음 정보를 기록합니다.  
  
-   다음 수준까지 호출한 코드 줄을 포함하는 원본 모듈  
  
-   스택의 다음 모듈을 호출한 코드 줄  
  
-   매개 변수를 가져온 저장 프로시저 또는 함수까지 호출한 경우 모든 매개 변수의 이름, 데이터 형식 및 값도 나열됩니다.  
  
 **지역**, **조사식**및 **간략한 조사식** 창의 식은 현재 스택 프레임에 대해 계산됩니다. 기본적으로 현재 스택 프레임은 디버거가 실행을 일시 중지한 스택의 맨 위 프레임입니다. 다른 스택 프레임을 현재 프레임으로 지정한 경우 **지역**, **조사식**및 **간략한 조사식** 창의 식은 새 스택 프레임에 대해 다시 계산됩니다. 프레임을 두 번 클릭하거나 프레임을 클릭하고 **프레임으로 전환**을 선택하여 현재 스택 프레임을 변경할 수 있습니다. 이 경우 **지역**, **조사식**및 **간략한 조사식** 창의 식은 새 프레임에 대해 다시 계산됩니다. 현재 스택 프레임이 스택의 맨 위 프레임이 아닌 경우 스택 프레임 왼쪽 여백에 있는 녹색 화살표가 현재 스택 프레임을 식별합니다.  
  
 스택 프레임을 마우스 오른쪽 단추로 클릭하고 **원본 코드로 이동**을 선택하면 해당 프레임에 대한 코드가 쿼리 편집기 창에 표시됩니다. 그러나 해당 프레임이 현재 프레임으로 생성되지 않고 **지역**, **조사식**및 **간략한 조사식** 창의 내용이 변경되지 않습니다.  
  
## <a name="system-information-and-transact-sql-results"></a>시스템 정보 및 Transact-SQL 결과  
 디버거는 **출력** 창에 해당 상태 및 이벤트 메시지를 나열합니다. 여기에는 디버거에서 다른 프로세스에 연결하는 경우 또는 디버거 스레드가 종료되는 경우와 같은 정보가 포함되어 있습니다.  
  
 디버그 모드에서는 **결과** 및 **메시지** 탭이 쿼리 편집기에 계속 활성화되어 있습니다. **결과** 탭은 디버깅 세션 동안 실행되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과 집합을 계속 표시합니다. **메시지** 탭은 *xx* 개 행 적용됨, PRINT 및 RAISERROR 문의 출력과 같은 시스템 메시지를 계속 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [지역 창](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [조사식 창](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [간략한 조사식 대화 상자](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [중단점 창](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md)   
 [호출 스택 창](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [스레드 창](../../relational-databases/scripting/transact-sql-debugger-threads-window.md)   
 [출력 창](../../relational-databases/scripting/transact-sql-debugger-output-window.md)   
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
