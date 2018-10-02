---
title: Transact-SQL 디버거 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, sysadmin requirement
- Transact-SQL debugger, supported versions
- Query Editor [Database Engine], right-click menu
- debugging [SQL Server], T-SQL debugger
- Transact-SQL debugger, Query Editor shortcut menu
- Transact-SQL debugger, stopping
- Transact-SQL debugger, Debug menu
- debugging [SQL Server]
- Transact-SQL debugger, Debug toolbar
- Transact-SQL debugger, keyboard shortcuts
- Transact-SQL debugger, starting
ms.assetid: 386f6d09-dbec-4dc7-9e8a-cd9a4a50168c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b90b3616e9641f21ae1345676e2262cf1cf424e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849451"
---
# <a name="run-the-transact-sql-debugger"></a>Transact-SQL 디버거 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기 창을 연 후에 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 디버거를 시작할 수 있습니다. 그러면 디버거를 중지할 때까지 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 디버그 모드에서 실행할 수 있습니다. 옵션을 설정하여 디버거 실행 방식을 사용자 지정할 수 있습니다.  
  
## <a name="starting-and-stopping-the-debugger"></a>디버거 시작 및 중지  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 시작하기 위한 요구 사항은 다음과 같습니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기가 다른 컴퓨터의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결된 경우 원격 디버깅을 사용하도록 디버거가 구성되어 있어야 합니다. 자세한 내용은 [TSQL 디버거를 실행하기 전에 방화벽 규칙 구성](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 sysadmin 고정 서버 역할의 멤버인 Windows 계정으로 실행해야 합니다.  
  
-   sysadmin 고정 서버 역할의 멤버인 Windows 인증 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인증 로그인을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 편집기 창을 연결해야 합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] SP2(서비스 팩 2) 이상의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에 연결해야 합니다. 쿼리 편집기 창이 단일 사용자 모드에 있는 인스턴스에 연결되어 있는 경우에는 디버거를 실행할 수 없습니다.  
  
 다음과 같은 이유로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드는 프로덕션 서버가 아니라 테스트 서버에서 디버깅하는 것이 좋습니다.  
  
-   디버깅은 높은 권한이 필요한 작업입니다. 따라서 sysadmin 고정 서버 역할의 멤버만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 디버깅할 수 있습니다.  
  
-   디버깅 세션은 사용자가 여러 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 작업을 조사하는 동안 장기간 실행되는 경우가 많습니다. 업데이트 잠금과 같이 세션에 의해 획득되는 잠금은 세션이 끝나거나 트랜잭션이 커밋 또는 롤백될 때까지 장기간 보유될 수 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 시작하면 쿼리 편집기 창이 디버그 모드로 설정됩니다. 쿼리 편집기 창이 디버그 모드로 설정되면 디버거가 코드의 첫 번째 줄에서 일시 중지됩니다. 그러면 코드를 단계별로 진행하고, 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 실행을 일시 중지하고, 디버거 창을 사용하여 현재 실행 상태를 볼 수 있습니다. **쿼리** 도구 모음에서 **디버그** 단추를 클릭하거나 **디버그** 메뉴에서 **디버깅 시작** 을 클릭하여 디버거를 시작할 수 있습니다.  
  
 쿼리 편집기 창은 쿼리 편집기 창의 마지막 문이 완료되거나 사용자가 디버그 모드를 중지할 때까지 디버그 모드로 유지됩니다. 다음 방법 중 하나를 사용하여 디버그 모드 및 문 실행을 중지할 수 있습니다.  
  
-   **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
-   **디버그** 도구 모음에서 **디버깅 중지** 단추를 클릭합니다.  
  
-   **쿼리** 메뉴에서 **쿼리 실행 취소**를 클릭합니다.  
  
-   **쿼리** 도구 모음에서 **쿼리 실행 취소** 단추를 클릭합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버그 **메뉴에서** 모두 분리 **를 클릭하여 디버그 모드를 중지하고 나머지** 문이 실행 완료되도록 할 수도 있습니다.  
  
## <a name="controlling-the-debugger"></a>디버거 제어  
 다음 메뉴 명령, 도구 모음 및 바로 가기를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거 작동 방식을 제어할 수 있습니다.  
  
-   **디버그** 메뉴 및 **디버그** 도구 모음. **디버그** 메뉴와 **디버그** 도구 모음 모두 열려 있는 쿼리 편집기 창에 포커스를 둘 때까지 비활성화되며 현재 프로젝트를 닫을 때까지 활성화된 상태로 유지됩니다.  
  
-   디버거 바로 가기 키  
  
-   쿼리 편집기 바로 가기 메뉴. 쿼리 편집기 창에서 쿼리 줄을 마우스 오른쪽 단추로 클릭하면 바로 가기 메뉴가 표시됩니다. 쿼리 편집기 창이 디버그 모드에 있으면 선택한 줄 또는 문자열에 적용되는 디버거 명령이 바로 가기 메뉴에 표시됩니다.  
  
-   **조사식** 또는 **중단점** 창과 같이 디버거에 의해 열리는 창에 있는 메뉴 항목 및 상황에 맞는 명령  
  
 다음 표에서는 디버거 메뉴 명령, 도구 모음 단추 및 바로 가기 키를 보여 줍니다.  
  
|디버그 메뉴 명령|편집기 바로 가기 명령|도구 모음 단추|바로 가기 키|작업|  
|------------------------|-----------------------------|--------------------|-----------------------|------------|  
|**창/중단점**|사용할 수 없음|**중단점**|Ctrl+Alt+B|중단점을 보고 관리할 수 있는 **중단점** 창을 표시합니다.|  
|**창/조사식/조사식1**|사용할 수 없음|**중단점/조사식/조사식1**|CTRL+ALT+W, 1|**조사식1** 창을 표시합니다.|  
|**창/조사식/조사식2**|사용할 수 없음|**중단점/조사식/조사식2**|CTRL+ALT+W, 2|**조사식2** 창을 표시합니다.|  
|**창/조사식/조사식3**|사용할 수 없음|**중단점/조사식/조사식3**|CTRL+ALT+W, 3|**조사식3** 창을 표시합니다.|  
|**창/조사식/조사식4**|사용할 수 없음|**중단점/조사식/조사식4**|Ctrl+Alt+W, 4|**조사식4** 창을 표시합니다.|  
|**창/지역**|사용할 수 없음|**중단점/지역**|Ctrl+Alt+V, L|**지역** 창을 표시합니다.|  
|**창/호출 스택**|사용할 수 없음|**중단점/호출 스택**|Ctrl+Alt+C|**호출 스택** 창을 표시합니다.|  
|**창/스레드**|사용할 수 없음|**중단점/스레드**|Ctrl+Alt+H|**스레드** 창을 표시합니다.|  
|**계속**|사용할 수 없음|**계속**|Alt+F5|다음 중단점까지 실행합니다. **계속** 은 디버그 모드에 있는 쿼리 편집기 창에 포커스를 둘 때까지 활성화되지 않습니다.|  
|**디버그**|사용할 수 없음|**디버그**|Alt+F5|쿼리 편집기 창을 디버그 모드로 설정하고 첫 번째 중단점까지 실행합니다. 디버그 모드에 있는 쿼리 편집기 창에 포커스가 있는 경우 **디버깅 시작** 은 **계속**으로 대체됩니다.|  
|**모두 중단**|사용할 수 없음|**모두 중단**|Ctrl+Alt+Break|이 기능은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에 사용되지 않습니다.|  
|**디버깅 중지**|사용할 수 없음|**디버깅 중지**|Shift+F5|쿼리 편집기 창에서 디버그 모드를 중지하고 일반 모드로 되돌립니다.|  
|**메뉴에서**|사용할 수 없음|사용할 수 없음|사용할 수 없음|쿼리 편집기 창에서 디버그 모드를 중지하지만 나머지 문은 실행합니다.|  
|**한 단계씩 코드 실행**|사용할 수 없음|**한 단계씩 코드 실행**|F11|다음 문을 실행하고 다음 문이 저장 프로시저, 트리거 또는 함수를 실행하는 경우 디버그 모드에서 새 쿼리 편집기 창을 엽니다.|  
|**프로시저 단위 실행**|사용할 수 없음|**프로시저 단위 실행**|F10|함수, 저장 프로시저 또는 트리거가 디버깅되지 않는다는 점을 제외하고 **한 단계씩 코드 실행**과 같습니다.|  
|**프로시저 나가기**|사용할 수 없음|**프로시저 나가기**|Shift+F11|중단점에서 일시 중지하지 않고 트리거, 함수 또는 저장 프로시저의 나머지 코드를 실행합니다. 일반 디버그 모드는 모듈을 호출한 코드로 컨트롤이 반환되면 재개됩니다.|  
|사용할 수 없음|**커서까지 실행**|사용할 수 없음|Ctrl+F10|중단점에서 중지하지 않고 마지막 중지 위치에서 현재 커서 위치까지 모든 코드를 실행합니다.|  
|**간략한 조사식**|**간략한 조사식**|사용할 수 없음|Ctrl+Alt+Q|**간략한 조사식** 창을 표시합니다.|  
|**중단점 설정/해제**|**중단점/중단점 삽입**|사용할 수 없음|F9|현재 또는 선택한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 중단점을 배치합니다.|  
|사용할 수 없음|**중단점/중단점 삭제**|사용할 수 없음|사용할 수 없음|선택한 줄에서 중단점을 삭제합니다.|  
|사용할 수 없음|**중단점/중단점 해제**|사용할 수 없음|사용할 수 없음|선택한 줄에서 중단점을 해제합니다. 중단점이 코드 줄에 유지되지만 중단점을 다시 설정할 때까지 실행이 중지되지 않습니다.|  
|사용할 수 없음|**중단점/중단점 설정**|사용할 수 없음|사용할 수 없음|선택한 줄에서 중단점을 설정합니다.|  
|**모든 중단점 삭제**|사용할 수 없음|사용할 수 없음|Ctrl+Shift+F9|모든 중단점을 삭제합니다.|  
|**모든 중단점 해제**|사용할 수 없음|사용할 수 없음|사용할 수 없음|모든 중단점을 해제합니다.|  
|사용할 수 없음|**조사식 추가**|사용할 수 없음|사용할 수 없음|**조사식** 창에 선택한 식을 추가합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 코드 단계별 실행](../../relational-databases/scripting/step-through-transact-sql-code.md)   
 [Transact-SQL 디버거 정보](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [데이터베이스 엔진 쿼리 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md)  
  
  
