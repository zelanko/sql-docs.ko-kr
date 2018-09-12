---
title: 차트, 경고, 로그 및 보고서 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4f29d36ab5e1664b73bc95d96f7255a1c8abf358
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818939"
---
# <a name="create-charts-alerts-logs-and-reports"></a>차트, 경고, 로그 및 보고서 만들기
  시스템 모니터를 사용하면 차트, 경고, 로그 및 보고서를 만들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 모니터링할 수 있습니다.  
  
## <a name="charts"></a>차트  
 차트를 사용하면 선택된 개체 및 카운터의 현재 성능(CPU 사용량 또는 디스크 I/O)을 모니터링할 수 있습니다. 차트에 여러 가지 시스템 모니터 개체 및 카운터 조합을 추가할 수 있습니다. 또한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 개체 및 카운터도 차트에 추가할 수 있습니다.  
  
 각 차트는 모니터링하려는 정보의 하위 집합을 나타냅니다. 예를 들어 어떤 차트는 메모리 사용량 통계를, 다른 차트는 디스크 I/O 통계를 추적하도록 할 수 있습니다.  
  
 차트 사용은 다음 태스크에 유용합니다.  
  
-   컴퓨터 혹은 응용 프로그램의 속도가 느려지는 원인 조사  
  
-   작동이 중단되는 성능 문제를 찾아내기 위해 시스템을 지속적으로 모니터링  
  
-   용량을 늘려야 하는 이유 확인  
  
-   선형 차트로 추세 표시  
  
-   히스토그램 차트로 비교 표시  
  
 차트는 이벤트가 발생할 때 모니터링하는 것과 같이 로컬 또는 원격 컴퓨터를 단기에 걸쳐 실시간으로 모니터링할 때 유용합니다.  
  
## <a name="alerts"></a>,  
 경고를 사용하면 시스템 모니터는 특정 이벤트를 추적해 이 이벤트에 대해 사용자가 요청한 대로 알려 줍니다. 경고 로그를 사용하면 선택된 카운터의 현재 성능 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]개체의 인스턴스를 모니터링할 수 있습니다. 카운터가 지정된 값을 넘어 가면 로그에 이벤트가 발생한 날짜와 시간이 기록됩니다. 이벤트는 네트워크 경고도 생성할 수 있습니다. 특정 프로그램을 이벤트가 처음 발생할 때 실행되도록 하거나 이벤트가 발생할 때마다 실행되도록 할 수도 있습니다. 예를 들어 경고 기능을 사용하면 모든 시스템 관리자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 디스크 공간이 부족하다는 네트워크 메시지를 보낼 수 있습니다.  
  
## <a name="logs"></a>로그  
 로그를 사용하면 선택된 개체 및 컴퓨터의 현재 동작에 대한 정보를 기록해 나중에 검색하고 분석할 수 있습니다. 여러 시스템의 데이터를 모아 하나의 로그 파일에 저장할 수도 있습니다. 예를 들어 여러 컴퓨터에 있는 선택된 개체의 성능에 대한 정보를 축적하도록 로그를 여러 개 만들어 나중에 분석할 때 사용할 수 있습니다. 이렇게 모은 로그 파일에 이름을 지정해 저장하면 비슷한 정보의 다른 로그를 만들어 비교할 때 다시 사용할 수 있습니다.  
  
 로그 파일을 활용하면 문제 해결이나 계획 수립 단계에서 풍부한 정보를 확보할 수 있습니다. 차트, 경고 및 보고서는 현재 작업에 대한 즉각적인 피드백을 제공하는 반면, 로그 파일을 사용하면 장기간에 걸쳐 카운터를 추적할 수 있습니다. 따라서 정보를 완벽하게 검사해 시스템 성능을 문서화할 수 있습니다.  
  
## <a name="reports"></a>보고서  
 보고서를 사용하면 계속 변경되는 선택된 개체의 카운터 및 인스턴스 값을 표시할 수 있습니다. 각 인스턴스의 값은 열에 표시됩니다. 보고 간격, 인쇄 스냅숏 및 데이터 내보내기를 조정할 수도 있습니다. 숫자를 그대로 표시하려면 보고서를 사용하십시오.  
  
 차트, 경고, 로그, 보고서 작성 또는 Windows 개체 및 카운터에 대한 자세한 내용은 Windows 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
