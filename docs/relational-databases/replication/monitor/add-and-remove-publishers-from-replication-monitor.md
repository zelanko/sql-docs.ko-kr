---
title: "복제 모니터에서 게시자 추가 및 제거 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fd06f71bd65e1731ab53924e03e756044e505ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>복제 모니터에서 게시자 추가 및 제거
  복제 모니터를 실행하는 서버가 게시자인 경우 자동으로 모니터에 추가됩니다. **게시자 추가** 대화 상자를 통해 게시자를 추가할 수 있습니다. 게시자를 추가하면 게시자는 모니터의 왼쪽 창에 있는 그룹에 표시됩니다. **내 게시자** 그룹이 기본적으로 포함되지만 새 그룹을 만들어 하나 이상의 복제 토폴로지를 관리할 수 있습니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-add-a-sql-server-publisher"></a>SQL Server 게시자를 추가하려면  
  
1.  왼쪽 창에서 **복제 모니터** 노드 또는 게시자 그룹 노드를 마우스 오른쪽 단추로 클릭한 다음 **게시자 추가**를 클릭합니다.  
  
2.  **게시자 추가** 대화 상자에서 **추가**를 클릭한 다음 **SQL Server 게시자 추가**를 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 게시자의 이름을 입력한 다음 인증 유형을 선택합니다. **SQL Server 인증**을 선택한 경우 로그인 및 암호를 입력합니다. 지정한 자격 증명은 나중에 이 서버에 연결할 때 사용하기 위해 복제 모니터에 의해 저장됩니다. 지정한 Windows 계정 또는 SQL Server 로그인은 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에 있는 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
4.  **연결**을 클릭합니다. 게시자가 원격 배포자를 사용할 경우 **서버에 연결** 대화 상자에 배포자로 연결하라는 메시지가 표시됩니다. 지정한 자격 증명은 나중에 이 서버에 연결할 때 사용하기 위해 복제 모니터에 의해 저장됩니다. 지정한 Windows 계정 또는 SQL Server 로그인은 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에 있는 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
5.  게시자 또는 배포자의 이름이 **다음 게시자의 모니터링 시작** 표에 표시됩니다.  
  
6.  게시자에 대해 새로 고침 및 연결 옵션을 지정하려면 표에서 게시자를 선택한 다음 필요에 맞게 옵션을 수정합니다. 새로 고침 옵션에 대한 자세한 내용은 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하십시오.  
  
7.  복제 모니터에서 게시자가 표시되는 그룹을 선택합니다. 새 그룹을 만들려면 **새 그룹**을 클릭한 다음 그룹 이름을 입력합니다. **이 게시자를 다음 그룹에 표시** 목록에서 해당 그룹을 선택합니다.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>Oracle 게시자를 추가하려면  
  
1.  왼쪽 창에서 **복제 모니터** 노드 또는 게시자 그룹 노드를 마우스 오른쪽 단추로 클릭한 다음 **게시자 추가**를 클릭합니다.  
  
2.  **게시자 추가** 대화 상자에서 **추가**를 클릭한 다음 **Oracle 게시자 추가**를 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 Oracle 게시자와 관련된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자의 이름을 입력한 다음 인증 유형을 선택합니다. **SQL Server 인증**을 선택한 경우 로그인 및 암호를 입력합니다. 지정한 자격 증명은 나중에 이 서버에 연결할 때 사용하기 위해 복제 모니터에 의해 저장됩니다. 지정한 Windows 계정 또는 SQL Server 로그인은 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에 있는 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
4.  **연결**을 클릭합니다.  
  
5.  게시자 또는 배포자의 이름이 **다음 게시자의 모니터링 시작** 표에 표시됩니다.  
  
6.  게시자에 대해 새로 고침 및 연결 옵션을 지정하려면 표에서 게시자를 선택한 다음 필요에 맞게 옵션을 수정합니다. 새로 고침 옵션에 대한 자세한 내용은 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하십시오.  
  
7.  복제 모니터에서 게시자가 표시되는 그룹을 선택합니다. 새 그룹을 만들려면 **새 그룹**을 클릭한 다음 그룹 이름을 입력합니다. **이 게시자를 다음 그룹에 표시** 목록에서 해당 그룹을 선택합니다.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>같은 배포자를 사용하는 하나 이상의 게시자를 추가하려면  
  
1.  왼쪽 창에서 **복제 모니터** 노드 또는 게시자 그룹 노드를 마우스 오른쪽 단추로 클릭한 다음 **게시자 추가**를 클릭합니다.  
  
2.  **게시자 추가** 대화 상자에서 **추가**를 클릭한 다음 **배포자를 지정한 후 해당 게시자 추가**를 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 배포자의 이름을 입력한 다음 인증 유형을 선택합니다. **SQL Server 인증**을 선택한 경우 로그인 및 암호를 입력합니다. 지정한 자격 증명은 나중에 이 서버에 연결할 때 사용하기 위해 복제 모니터에 의해 저장됩니다. 지정한 Windows 계정 또는 SQL Server 로그인은 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에 있는 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
4.  **연결**을 클릭합니다.  
  
5.  배포자와 각 게시자의 이름이 **다음 게시자의 모니터링 시작** 표에 표시됩니다. 게시자가 복제 모니터에 이미 추가된 경우에는 표에 게시자가 표시되지 않습니다.  
  
6.  게시자에 대해 새로 고침 및 연결 옵션을 지정하려면 표에서 게시자를 선택한 다음 필요에 맞게 옵션을 수정합니다. 새로 고침 옵션에 대한 자세한 내용은 [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하십시오.  
  
7.  복제 모니터에서 게시자가 표시되는 그룹을 선택합니다. 새 그룹을 만들려면 **새 그룹**을 클릭한 다음 그룹 이름을 입력합니다. **이 게시자를 다음 그룹에 표시** 목록에서 해당 그룹을 선택합니다.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>게시자 및 게시자 그룹에 대한 설정을 수정하려면  
  
1.  왼쪽 창에서 게시자를 마우스 오른쪽 단추로 클릭한 다음 **게시자 설정**을 클릭합니다.  
  
2.  **게시자 설정** 대화 상자에서 변경을 수행합니다.  
  
    -   복제 모니터가 서버에 연결할 때 사용하는 자격 증명을 변경하려면 **게시자 연결** 또는 **배포자 연결**을 클릭한 다음 **서버에 연결** 입력란에 자격 증명을 입력합니다.  
  
    -   한 그룹에서 다른 그룹으로 게시자를 이동하려면 **다음 게시자의 모니터링 시작** 표에서 게시자를 선택한 다음 **이 게시자를 다음 그룹에 표시** 목록에서 새 그룹을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>복제 모니터에서 게시자를 제거하려면  
  
1.  왼쪽 창에서 게시자를 마우스 오른쪽 단추로 클릭합니다.  
  
2.  **제거**를 클릭합니다.  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>게시자 그룹을 복제 모니터에 추가하려면  
  
1.  게시자 그룹은 게시자를 추가하거나 게시자에 대한 설정을 수정하는 경우에만 만들 수 있습니다. 자세한 내용은 게시자 추가 방법을 참조하십시오.  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>복제 모니터에서 게시자 그룹을 제거하려면  
  
1.  모든 게시자를 다른 그룹으로 이동하거나 복제 모니터에서 제거합니다. 자세한 내용은 이 항목의 앞부분에 나오는 절차를 참조하십시오.  
  
2.  게시자 그룹을 마우스 오른쪽 단추로 클릭한 다음 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../../relational-databases/replication/configure-distribution.md)   
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
