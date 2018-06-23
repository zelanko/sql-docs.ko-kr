---
title: 배포자 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a5644adcf6037789429de47ee69a3e6c91991e4f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180806"
---
# <a name="distributor-settings"></a>배포자 설정
  **배포자 설정** 대화 상자에서는 복제 모니터의 왼쪽 창에 추가된 배포자에 대한 설정을 변경할 수 있습니다.  
  
## <a name="options"></a>변수  
 **복제 모니터가 시작될 때 자동으로 연결**  
 복제 모니터에서 배포자에 연결하고 상태 정보를 검색하도록 하려면 선택합니다.  
  
 **대량 삽입 태스크 편집기**  
 **서버에 연결** 대화 상자를 표시하려면 클릭합니다. 이 대화 상자를 통해 복제 모니터에서 배포자에 연결하기 위해 사용하는 연결 속성 및 자격 증명을 보고 변경할 수 있습니다.  
  
 **이 배포자 및 해당 게시의 상태를 자동으로 새로 고침**  
 복제 모니터에서 배포자의 상태를 자동으로 새로 고치도록 하려면 선택합니다. 이 옵션을 선택하면 복제 모니터가 **새로 고침 빈도** 옵션에 설정된 폴링 간격에 따라 배포자를 폴링하여 상태 정보를 얻습니다. 복제 모니터에서의 새로 고침에 대한 자세한 내용은 [Caching, Refresh, and Replication Monitor Performance](monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하십시오.  
  
 **새로 고침 빈도**  
 복제 모니터가 상태를 얻기 위해 배포자를 폴링하는 빈도를 지정하는 값(초)을 입력합니다. 값이 낮을수록 폴링이 자주 수행되며 많은 게시자를 모니터링하는 경우 배포자에서의 성능에 영향을 줄 수 있습니다. 시스템을 테스트하여 적절한 값을 결정하는 것이 좋습니다. **새로 고침 빈도** 설정은 복제 모니터의 세부 정보 창에서 **자동 새로 고침** 을 선택한 경우에도 사용됩니다.  
  
 **다음 그룹에 있는 이 배포자의 모든 게시자 표시**  
 목록에서 게시자 그룹을 선택합니다. 게시자는 왼쪽 창에서 이 그룹 아래에 표시됩니다. 그룹을 사용하면 게시자를 구성할 수 있으며 이로 인해 복제 기능이 영향을 받지는 않습니다.  
  
 **새 그룹**  
 새 게시자 그룹을 만들려면 클릭합니다. 게시자 그룹을 사용하면 복제 모니터 내에서 게시자를 편리하게 구성할 수 있습니다. 그룹은 데이터 복제 또는 복제 토폴로지의 서버 간 관계에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  