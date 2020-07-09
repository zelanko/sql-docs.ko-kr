---
title: 게시자 추가 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: bd972c1825deb947537473096653fc33e07a92fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726090"
---
# <a name="add-publisher"></a>게시자 추가
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **게시자 추가** 대화 상자를 사용하여 복제 모니터의 왼쪽 창에 하나 이상의 게시자를 추가할 수 있습니다. 게시자를 추가한 후 왼쪽 창에서 게시자를 선택하면 오른쪽 창에 해당 게시자에 대한 정보가 표시됩니다.  
  
## <a name="options"></a>옵션  
 **추가**  
 추가할 게시자 유형을 선택하려면 클릭합니다. **서버에 연결** 대화 상자가 시작됩니다. 옵션은 다음과 같습니다.  
  
-   **SQL Server 게시자 추가...**  
  
     **서버에 연결** 대화 상자를 사용하여 게시자에 연결합니다.  
  
-   **Oracle 게시자 추가...**  
  
     **서버에 연결** 대화 상자를 사용하여 Oracle 게시자에 연결된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에 연결합니다.  
  
-   **배포자를 지정한 후 해당 게시자 추가...**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 연결 **대화 상자를 사용하여 하나 이상의 게시자에 연결된** 배포자에 연결합니다.  
  
 게시자 또는 배포자에 성공적으로 연결하면 각 게시자 및 해당 배포자의 이름이 대화 상자 상단의 표에 표시됩니다.  
  
> [!NOTE]  
>  배포자 및 게시자가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 실행되는 경우가 많지만 배포자는 다른 인스턴스에서 실행될 수 있으며 이러한 구성을 원격 배포자라고 합니다.  
  
 **제거**  
 대화 상자 상단의 표에서 게시자를 선택하고 **제거** 를 클릭하여 추가할 게시자 목록에서 해당 게시자를 제거합니다.  
  
> [!NOTE]  
>  이 단추를 사용하여 이미 복제 모니터에 표시된 게시자를 제거할 수는 없습니다. 이미 표시된 게시자를 제거하려면 복제 모니터의 왼쪽 창에서 해당 게시자를 마우스 오른쪽 단추로 클릭한 다음 **제거**를 클릭합니다.  
  
 **복제 모니터가 시작될 때 자동으로 연결**  
 복제 모니터가 자동으로 배포자에 연결하여 대화 상자 상단의 표에 선택된 게시자의 상태 정보를 검색하도록 하려면 선택합니다. 이 확인란의 선택을 취소하면 복제 모니터를 시작한 후 복제 모니터의 왼쪽 창에서 게시자를 마우스 오른쪽 단추로 클릭한 다음 **연결**을 클릭하여 수동으로 연결해야 합니다.  
  
 **이 게시자 및 해당 게시의 상태를 자동으로 새로 고침**  
 복제 모니터가 대화 상자 상단의 표에 선택된 게시자의 상태를 자동으로 새로 고치도록 하려면 선택합니다. 이 옵션을 선택하면 복제 모니터가 배포자를 폴링하여 게시자 및 해당 게시에 대한 상태 정보를 얻습니다. 폴링 간격은 **새로 고침 빈도** 옵션으로 설정됩니다. 복제 모니터에서의 새로 고침에 대한 자세한 내용은 [캐싱, 새로 고침 및 복제 모니터 성능](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하세요.  
  
 **새로 고침 빈도**  
 복제 모니터가 상태를 얻기 위해 배포자를 폴링하는 빈도를 지정하는 값(초)을 입력합니다. 값이 낮을수록 폴링이 자주 수행되며 많은 게시자를 모니터링하는 경우 배포자에서의 성능에 영향을 줄 수 있습니다. 시스템을 테스트하여 적절한 값을 결정하는 것이 좋습니다. **새로 고침 빈도** 설정은 복제 모니터의 세부 정보 창에서 **자동 새로 고침** 을 선택한 경우에도 사용됩니다.  
  
 **이 게시자를 다음 그룹에 표시**  
 목록에서 게시자 그룹을 선택합니다. 게시자는 왼쪽 창에서 이 그룹 아래에 표시됩니다. 그룹을 사용하면 게시자를 구성할 수 있으며 이로 인해 복제 기능이 영향을 받지는 않습니다. 정의된 그룹이 없거나 새 그룹을 만들려면 **새 그룹**을 클릭합니다.  
  
 **새 그룹**  
 새 게시자 그룹을 만들려면 클릭합니다. 게시자 그룹을 사용하면 복제 모니터 내에서 게시자를 편리하게 구성할 수 있습니다. 그룹은 데이터 복제 또는 복제 토폴로지의 서버 간 관계에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
