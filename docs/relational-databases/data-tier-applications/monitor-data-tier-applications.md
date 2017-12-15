---
title: "데이터 계층 응용 프로그램 모니터링 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cb93f6f2644966696f7d7c48f2dac7f72cde06b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-data-tier-applications"></a>데이터 계층 응용 프로그램 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] SSMS([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])의 **유틸리티 탐색기** 및 **개체 탐색기**에서 시스템 뷰 및 테이블과 함께 DAC(데이터 계층 응용 프로그램)를 모니터링할 수 있습니다. 또한 DAC에 포함된 데이터베이스의 모든 개체를 표준 데이터베이스 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 모니터링 기술을 사용하여 모니터링할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
 DAC를 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 관리되는 인스턴스로 배포하는 경우 배포된 DAC에 대한 정보는 유틸리티 컬렉션 집합이 인스턴스에서 유틸리티 제어 지점으로 다음에 전송될 때 SQL Server 유틸리티에 통합됩니다. 그런 다음 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **유틸리티 탐색기**를 사용하여 DAC에 대한 기본 상태 정보를 볼 수 있습니다.  
  
 인스턴스가 SQL Server 유틸리티에서 관리되는지 여부에 상관없이 SSMS **개체 탐색기** 에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 배포된 각 DAC에 대한 기본 구성 정보가 표시됩니다. 또한 데이터베이스를 모니터링할 때와 동일한 절차를 사용하여 배포된 DAC와 연결된 데이터베이스를 모니터링할 수 있습니다.  
  
## <a name="using-the-sql-server-utility"></a>SQL Server 유틸리티 사용  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **유틸리티 탐색기**의 **배포된 데이터 계층 응용 프로그램** 세부 정보 페이지에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 관리되는 인스턴스에 배포된 모든 DAC의 리소스 사용률을 보고하는 대시보드가 표시됩니다. 이 세부 정보 페이지의 위쪽 창에는 배포된 각 DAC가 해당 CPU 및 파일 리소스의 사용률이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 정의된 정책을 벗어나는지 여부를 나타내는 시각적 표시기와 함께 나열됩니다. 목록 뷰에서 DAC를 선택할 경우 페이지 아래쪽 창의 탭에 추가 세부 정보가 표시됩니다. 세부 정보 페이지에 제공되는 정보에 대한 자세한 내용은 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)를 참조하세요.  
  
 **배포된 데이터 계층 응용 프로그램** 세부 정보 페이지를 사용하여 사용률이 낮거나 하드웨어 리소스를 과도하게 사용하는 DAC를 신속하게 식별한 후 문제를 해결하기 위한 계획을 수립할 수 있습니다. 현재 하드웨어 리소스를 충분히 활용하지 않는 여러 DAC를 단일 서버로 통합하여 일부 서버를 다른 곳에 사용하도록 해제할 수 있습니다. DAC가 현재 서버의 리소스를 과도하게 사용하는 경우 DAC를 더 큰 서버로 이동하거나 현재 서버에 리소스를 추가할 수 있습니다.  
  
 리소스 사용의 최소 및 최대 한도는 **유틸리티 관리** 세부 정보 페이지에 정의된 응용 프로그램 모니터링 정책에 의해 정의됩니다. 데이터베이스 관리자는 조직에서 설정한 한도와 일치하도록 이러한 정책을 조정할 수 있습니다. 예를 들어 한 회사는 DAC의 최대 CPU 사용률을 75%로 설정하고 다른 회사는 80%로 설정할 수 있습니다. 응용 프로그램 모니터링 정책을 설정하는 방법은 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)를 참조하세요.  
  
 **배포된 데이터 계층 응용 프로그램** 세부 정보 페이지를 보려면  
  
1.  **보기/유틸리티 탐색기** 메뉴를 선택합니다.  
  
2.  **유틸리티 탐색기** 를 UCP(유틸리티 제어 지점)에 연결합니다.  
  
3.  **보기/유틸리티 탐색기 정보** 메뉴를 선택합니다.  
  
4.  **유틸리티 탐색기** 에서 **배포된 데이터 계층 응용 프로그램**노드를 선택합니다.  
  
 **배포된 데이터 계층 응용 프로그램** 세부 정보 페이지의 정보는 기본적으로 15분마다 데이터를 수집하도록 되어 있는 유틸리티 관리 데이터 웨어하우스의 데이터에서 제공됩니다. **유틸리티 관리** 세부 정보 페이지를 사용하여 이 간격을 조정할 수도 있습니다.  
  
## <a name="using-object-explorer"></a>개체 탐색기 사용  
 SSMS **개체 탐색기** 에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 배포된 각 DAC에 대한 기본 구성 정보가 표시됩니다. 여기에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록된 관리되는 인스턴스 및 **유틸리티 탐색기**에서 볼 수 없는 독립 실행형 인스턴스가 둘 다 포함됩니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 배포된 DAC의 세부 정보를 보려면  
  
1.  **보기/개체 탐색기** 메뉴를 선택합니다.  
  
2.  개체 탐색기 창에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
3.  **보기/개체 탐색기 정보** 메뉴를 선택합니다.  
  
4.  **개체 탐색기** 에서 이 인스턴스에 매핑되는 서버 노드를 선택한 다음 **관리\데이터 계층 응용 프로그램** 노드로 이동합니다.  
  
5.  세부 정보 페이지의 위쪽 창에 있는 목록 뷰에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 배포된 각 DAC가 나열됩니다. DAC를 선택하여 페이지 아래쪽의 세부 정보 창에 정보를 표시할 수 있습니다.  
  
 **데이터 계층 응용 프로그램** 노드를 마우스 오른쪽 단추로 클릭하면 나타나는 메뉴에서 새 DAC를 배포하거나 기존 DAC를 삭제할 수도 있습니다.  
  
## <a name="using-the-dac-system-views-and-tables"></a>DAC 시스템 뷰 및 테이블 사용  
 msdb.dbo.sysdac_history_internal 시스템 테이블은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에서 수행된 모든 DAC 관리 동작의 성공이나 실패를 기록합니다. 이 테이블은 각 동작이 발생한 시간 및 동작을 시작한 로그인을 기록합니다. 자세한 내용은 [sysdac_history_internal&#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal.md)을 참조하세요.  
  
 DAC 시스템 뷰는 기본 카탈로그 정보를 보고합니다. 자세한 내용은 [데이터 계층 응용 프로그램 뷰&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)를 참조하세요.  
  
## <a name="monitoring-dac-databases"></a>DAC 데이터베이스 모니터링  
 DAC가 성공적으로 배포된 후 DAC에 포함된 데이터베이스는 다른 데이터베이스와 동일하게 작동합니다. 표준 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 기술 및 도구를 사용하여 데이터베이스의 성능, 로그, 이벤트 및 리소스 사용률을 모니터링할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 응용 프로그램 배포](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  
