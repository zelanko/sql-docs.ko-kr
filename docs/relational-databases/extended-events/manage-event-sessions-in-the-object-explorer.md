---
title: 개체 탐색기에서 이벤트 세션 관리
description: '개체 탐색기에서 확장 이벤트에 영향을 주는 작업(예: 확장 이벤트 만들기, 시작, 중지, 내보내기, 가져오기, 편집 또는 삭제)을 수행할 수 있습니다.'
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3b7295d803770d37940480606ce038129e62a01d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465514"
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>개체 탐색기에서 이벤트 세션 관리

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 항목에서는 **개체 탐색기** 에서 수행할 수 있는 확장 이벤트에 영향을 주는 동작에 대해 설명합니다.  
  
-   확장 이벤트 세션 만들기  
  
-   확장 이벤트 세션 시작 또는 중지  
  
-   확장 이벤트 세션 내보내기  
  
-   확장 이벤트 세션 템플릿 가져오기  
  
-   확장 이벤트 세션 편집  
  
-   확장 이벤트 세션 삭제  
  
## <a name="create-an-extended-events-session"></a>확장 이벤트 세션 만들기  
 확장 이벤트 세션을 만드는 방법은 [Create an Extended Events Session](/previous-versions/sql/sql-server-2016/hh213147(v=sql.130))를 참조하십시오.  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>확장 이벤트 세션 시작 또는 중지  
 **쿼리 편집기** 에서 **ALTER EVENT SESSION** 문을 사용하거나 **개체 탐색기** 의 **확장 이벤트** 노드를 사용하여 확장 이벤트 세션을 시작하거나 중지할 수 있습니다.  
  
 이벤트 세션을 중지하면 해당 세션은 sys.dm_xe_sessions DMV(동적 관리 뷰)에서 더 이상 활성 세션으로 표시되지 않습니다. 그러나 세션 정의는 그대로 유지되므로 세션을 다시 시작할 수 있습니다. 세션 정의를 완전히 제거하려면 세션을 삭제해야 합니다.  
  
 확장 이벤트 세션을 시작하거나 중지하려면 ALTER ANY EVENT SESSION 권한이 있어야 합니다.  
  
 링 버퍼, 버킷팅, 이벤트 쌍 또는 동기 이벤트 카운터 대상 등의 메모리 내 대상을 사용하는 세션을 중지하면 해당 세션의 버퍼(sys.dm_xe_session_targets DMV의 target_data 열)에 저장된 모든 정보가 손실됩니다. 세션을 중지한 후 이벤트 데이터에 액세스하려면 세션을 중지하기 전에 데이터를 저장하거나 파일 대상을 사용하도록 세션을 구성해야 합니다.  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>쿼리 편집기를 사용하여 확장 이벤트 세션 시작 또는 중지  
 세션을 시작하려면 다음 문을 실행합니다. *session_name* 을 확장 이벤트 세션의 이름으로 바꿉니다.  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 세션을 중지하려면 다음 문을 실행합니다. *session_name* 을 확장 이벤트 세션의 이름으로 바꿉니다.  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>개체 탐색기에서 확장 이벤트 세션 시작 또는 중지  
 **개체 탐색기** 에서 확장 이벤트 세션을 시작하거나 중지하려면 **관리**, **확장 이벤트** 및 **세션** 노드를 차례로 확장한 다음 세션을 마우스 오른쪽 단추로 클릭하고 **세션 시작** 또는 **세션 중지** 를 클릭합니다.  
  
## <a name="export-an-extended-events-session-template"></a>확장 이벤트 세션 템플릿 내보내기  
 **개체 탐색기** 를 사용하여 확장 이벤트 세션을 내보내고 이 세션을 .xml 템플릿 파일로 저장할 수 있습니다. 예를 들어 세션을 내보낸 다음 **새 세션 마법사** 또는 **새 세션** 마법사를 사용하여 새 이벤트 세션에 템플릿을 적용할 수 있습니다.  
  
 세션을 내보내는 경우 NTFS 파일 시스템을 사용하는 위치에 템플릿 파일을 저장하고, 인증된 사용자만 해당 정보를 볼 수 있도록 액세스를 제한해야 합니다.  
  
 **개체 탐색기** 에서 확장 이벤트 세션을 내보내려면  
  
1.  **관리**, **확장 이벤트** 및 **세션** 노드를 차례로 확장합니다.  
  
2.  내보낼 세션을 마우스 오른쪽 단추로 클릭하고 **세션 내보내기** 를 선택합니다.  
  
3.  **다른 이름으로 저장** 대화 상자에서 파일을 저장할 위치를 선택하고 **파일 이름** 상자에 파일 이름을 입력한 다음 **저장** 을 클릭합니다.  
  
     파일을 기본 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 템플릿 위치에 저장하면 **새 세션 마법사** 및 **새 세션** 대화 상자의 미리 정의된 템플릿 드롭다운 목록에 해당 템플릿이 표시됩니다.  
  
## <a name="import-an-extended-events-session-template"></a>확장 이벤트 세션 템플릿 가져오기  
 **개체 탐색기** 를 사용하여 확장 이벤트 세션 템플릿을 가져올 수 있습니다. 예를 들어 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 내보낸 템플릿을 사용하여 세션을 만들려는 경우 템플릿을 가져옵니다.  
  
 확장 이벤트 세션을 가져오려면 **ALTER ANY EVENT SESSION** 권한이 있어야 합니다.  
  
 템플릿 파일을 가져오기 전에 파일 원본을 신뢰할 수 있는지 확인합니다. NTFS 파일 시스템을 사용하며 인증된 사용자만 해당 정보를 볼 수 있도록 액세스가 제한된 위치에 템플릿 파일을 저장해야 합니다.  
  
 확장 이벤트 세션을 가져오려면  
  
1.  **개체 탐색기** 에서 **관리** 및 **확장 이벤트** 노드를 차례로 확장합니다.  
  
2.  **세션** 을 마우스 오른쪽 단추로 클릭하고 **새 세션** 을 선택합니다.  
  
3.  세션의 이름을 지정합니다.  
  
4.  **템플릿** 드롭다운 상자를 확장합니다.  
  
5.  **\<File From ...>열기** 를 클릭하고 가져올 세션(XML 파일)을 찾습니다.  
  
 해당 세션이 **세션** 노드에 표시됩니다. 기본적으로 세션은 시작되지 않습니다.  
  
## <a name="edit-an-extended-events-session"></a>확장 이벤트 세션 편집  
 개체 탐색기에서 확장 이벤트 세션을 편집할 수 있습니다.  
  
 확장 이벤트 세션을 편집하려면  
  
1.  **개체 탐색기** 에서 **관리**, **확장 이벤트**, **세션** 노드를 차례로 확장합니다.  
  
2.  세션을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
3.  **페이지 선택** 섹션에서 편집할 페이지를 선택합니다.  
  
4.  이벤트 세션을 수정한 후 **확인** 을 클릭합니다.  
  
## <a name="script-an-event-session-definition-using-tsql"></a>다음을 사용하여 확장 이벤트 세션 스크립팅: [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 새 세션 마법사와 새 세션 대화 상자에는 확장 이벤트 세션을 정의하는, [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 생성하는 스크립트 옵션이 있습니다.  
  
 세션 이름을 마우스 오른쪽 단추로 클릭하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 세션 스크립팅 **을 선택한 다음** Create **를 선택하여 기존 확장 이벤트 세션의** 에 액세스할 수 있습니다.  
  
## <a name="delete-an-extended-events-session"></a>확장 이벤트 세션 삭제  
 다음과 같은 방법으로 확장 이벤트 세션을 삭제할 수 있습니다.  
  
-   쿼리 편집기에서 **DROP EVENT SESSION** 사용  
  
-   **개체 탐색기** 에서  
  
 이벤트 세션을 삭제하면 모든 구성 정보도 제거되므로 해당 세션 정의가 더 이상 sys.server_event_sessions 카탈로그 뷰에 나타나지 않습니다.  
  
> [!NOTE]  
>  system_health와 Always On_health는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되어 있으므로 삭제하지 마세요. system_health는 기본적으로 사용됩니다. 자세한 내용은 [system_health 세션 사용](../../relational-databases/extended-events/use-the-system-health-session.md)을 참조하세요. Always On_health는 기본적으로 해제되어 있습니다. 이러한 세션은 성능 문제를 진단하는 데 유용한 데이터를 수집합니다.  
  
 확장 이벤트 세션을 삭제하려면 ALTER ANY EVENT SESSION 권한이 있어야 합니다.  
  
 **개체 탐색기** 에서 확장 이벤트 세션을 삭제하려면  
  
1.  **관리**, **확장 이벤트** 및 **세션** 노드를 차례로 확장합니다.  
  
2.  세션을 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.  
  
3.  **개체 삭제** 대화 상자에서 **확인** 을 클릭합니다.  
  
4.  이벤트 세션을 수정한 후 **확인** 을 클릭합니다.  
  
 **쿼리 편집기** 에서 확장 이벤트 세션을 삭제하려면 다음 문을 실행합니다. *session_name* 을 삭제할 확장 이벤트 세션의 이름으로 바꿉니다.  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
