---
title: "중단점 동작 지정 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.action
helpviewer_keywords:
- Transact-SQL debugger, breakpoint action
- Transact-SQL debugger, breakpoint when hit action
ms.assetid: f97f0097-6f51-40c1-b2e0-294a93ce1e1b
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1594f724e5020c1678812ff74c55bb1fefe5bf5e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="specify-a-breakpoint-action"></a>중단점 동작 지정
  중단점 **적중될 때** 동작은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 중단점에 대해 수행하는 사용자 지정 태스크를 지정합니다. 지정한 적중 횟수에 도달하고 지정한 중단 조건을 만족하면 디버거는 해당 중단점에 대해 지정된 동작을 수행합니다.  
  
##  <a name="BKMK_ActionConsiderations"></a> 동작 고려 사항  
 중단점의 기본 동작은 적중 횟수와 중단점 조건을 모두 만족하면 실행을 중단하는 것입니다. **디버거에서** 적중될 때 [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작은 주로 출력 메시지를 지정하여 대신 디버거 **출력** 창에 정보를 출력하는 데 사용됩니다.  
  
 출력 메시지는 디버깅 중인 **의 정보가 포함된 식을 포함하는 텍스트 문자열로** 메시지 표시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 옵션에 지정합니다. 식은 다음과 같습니다.  
  
-   중괄호({})에 포함된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식. 식은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변수, 매개 변수 및 기본 제공 함수를 포함할 수 있습니다. 예제에는 {@MyVariable}, {@NameParameter}, {@@SPID} 또는 {SERVERPROPERTY('ProcessID')}가 포함됩니다.  
  
-   다음 키워드 중 하나:  
  
    1.  $ADDRESS는 중단점이 설정된 저장 프로시저 또는 사용자 정의 함수의 이름을 반환합니다. 중단점이 편집기 창에 설정되어 있으면 $ADDRESS는 편집 중인 스크립트 파일의 이름을 반환합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 $ADDRESS와 $FUNCTION은 동일한 정보를 반환합니다.  
  
    2.  $CALLER는 저장 프로시저 또는 함수를 호출한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 단위의 이름을 반환합니다. 중단점이 편집기 창에 있으면 $CALLER는 \<No caller available>을 반환합니다. 중단점이 편집기 창의 코드에서 호출되는 저장 프로시저 또는 사용자 정의 함수에 있으면 $CALLER는 편집 중인 파일의 이름을 반환합니다. 중단점이 다른 저장 프로시저 또는 함수에서 호출되는 저장 프로시저 또는 사용자 정의 함수에 있으면 $CALLER는 호출하는 프로시저 또는 함수의 이름을 반환합니다.  
  
    3.  $CALLSTACK은 체인에서 현재 저장 프로시저 또는 사용자 정의 함수를 호출한 함수 호출 스택을 반환합니다. 중단점이 편집기 창에 있으면 $CALLSTACK은 편집 중인 스크립트 파일의 이름을 반환합니다.  
  
    4.  $FUNCTION은 중단점이 설정된 저장 프로시저 또는 사용자 정의 함수의 이름을 반환합니다. 중단점이 편집기 창에 설정되어 있으면 $FUNCTION은 편집 중인 스크립트 파일의 이름을 반환합니다.  
  
    5.  $PID 및 $PNAME은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이 실행되고 있는 데이터베이스 엔진 인스턴스를 실행하는 운영 체제 프로세스의 ID 및 이름을 반환합니다. $PID는 SERVERPROPERTY('ProcessID')와 동일한 ID를 반환합니다. 다른 점은 $PID는 16진수 값이고 SERVERPROPERTY('ProcessID')는 10진수 값이라는 것입니다.  
  
    6.  $TID 및 $TNAME은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리를 실행하는 운영 체제 스레드의 ID 및 이름을 반환합니다. 이 스레드는 데이터베이스 엔진 인스턴스를 실행하는 프로세스에 연결되어 있는 스레드입니다. $TID는 SELECT kpid FROM sys.sysprocesses WHERE spid = @@SPID와 동일한 값을 반환합니다. 다른 점은 $TID는 16진수 값이고 kpid는 10진수 값이라는 것입니다.  
  
-   백슬래시(\\) 문자를 이스케이프 문자로 사용하여 \\{, \\}, \\\\등의 중괄호 및 백슬래시를 메시지에 허용할 수 있습니다.  
  
#### <a name="to-specify-a-when-hit-action"></a>적중될 때 동작을 지정하려면  
  
1.  편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중될 때** 를 클릭합니다.  
  
     -또는-  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **적중될 때** 를 클릭합니다.  
  
2.  **중단점이 적중될 때** 대화 상자에서 원하는 동작을 선택합니다.  
  
    1.  중단점이 적중될 때 디버거 출력 창에 메시지를 출력하려면 **메시지 표시** 를 선택합니다.  
  
    2.  **매크로 실행** 옵션은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 사용할 수 없으므로 회색으로 나타납니다.  
  
    3.  중단점이 실행을 일시 중지하지 않도록 하려면 **계속 실행** 을 선택합니다. 이 옵션은 **메시지 표시** 옵션을 선택한 경우에만 활성화됩니다.  
  
3.  **확인** 을 클릭하여 변경 내용을 구현하거나 **취소** 를 클릭하여 변경 내용을 적용하지 않고 종료합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중단점 조건 지정](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [적중 횟수 지정](../../relational-databases/scripting/specify-a-hit-count.md)  
  
  
