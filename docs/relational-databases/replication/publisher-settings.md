---
title: "게시자 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8fcc0c12988b1daf5ffa6cfc7f45a5c2e2ff9d88
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="publisher-settings"></a>게시자 설정
  **게시자 설정** 대화 상자에서 복제 모니터의 왼쪽 창에 추가된 게시자에 대한 설정을 변경할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **게시자 연결**  
 복제 모니터에서 게시자에 연결하기 위해 사용하는 연결 속성 및 자격 증명을 보고 변경할 수 있는 **서버에 연결** 대화 상자를 시작하려면 클릭합니다.  
  
 **배포자 연결**  
 게시자가 원격 배포자를 사용하는 경우에만 표시됩니다. 복제 모니터에서 원격 배포자에 연결하기 위해 사용하는 연결 속성 및 자격 증명을 보고 변경할 수 있는 **서버에 연결** 대화 상자를 시작하려면 클릭합니다.  
  
 **복제 모니터가 시작될 때 자동으로 연결**  
 복제 모니터가 자동으로 배포자에 연결하여 대화 상자 상단의 표에 선택된 게시자의 상태 정보를 검색하도록 하려면 선택합니다. 이 확인란의 선택을 취소하면 복제 모니터를 시작한 후 복제 모니터의 왼쪽 창에서 게시자를 마우스 오른쪽 단추로 클릭한 다음 **연결**을 클릭하여 수동으로 연결해야 합니다.  
  
 **이 게시자 및 해당 게시의 상태를 자동으로 새로 고침**  
 복제 모니터가 대화 상자 상단의 표에 선택된 게시자의 상태를 자동으로 새로 고치도록 하려면 선택합니다. 이 옵션을 선택하면 복제 모니터가 배포자를 폴링하여 게시자 및 해당 게시에 대한 상태 정보를 얻습니다. 폴링 간격은 **새로 고침 빈도** 옵션으로 설정됩니다. 복제 모니터에서의 새로 고침에 대한 자세한 내용은 [캐싱, 새로 고침 및 복제 모니터 성능](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하세요.  
  
 **새로 고침 빈도**  
 복제 모니터가 상태를 얻기 위해 배포자를 폴링하는 빈도를 지정하는 값(초)을 입력합니다. 값이 낮을수록 폴링이 자주 수행되며 많은 게시자를 모니터링하는 경우 배포자에서의 성능에 영향을 줄 수 있습니다. 시스템을 테스트하여 적절한 값을 결정하는 것이 좋습니다. **새로 고침 빈도** 설정은 복제 모니터의 세부 정보 창에서 **자동 새로 고침** 을 선택한 경우에도 사용됩니다.  
  
 **이 게시자를 다음 그룹에 표시**  
 목록에서 게시자 그룹을 선택합니다. 게시자는 왼쪽 창에서 이 그룹 아래에 표시됩니다. 그룹을 사용하면 게시자를 구성할 수 있으며 이로 인해 복제 기능이 영향을 받지는 않습니다.  
  
 **새 그룹**  
 새 게시자 그룹을 만들려면 클릭합니다. 게시자 그룹을 사용하면 복제 모니터 내에서 게시자를 편리하게 구성할 수 있습니다. 그룹은 데이터 복제 또는 복제 토폴로지의 서버 간 관계에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
