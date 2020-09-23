---
title: 장애 조치(failover) 클러스터 인스턴스 이름 바꾸기
description: 이 문서에서는 장애 조치(failover) 클러스터의 일부인 SQL Server 인스턴스의 이름을 바꾸는 방법을 설명합니다. 이는 독립 실행형 인스턴스의 이름을 바꾸는 방법과는 다릅니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- clusters [SQL Server], virtual servers
- renaming virtual servers
- virtual servers [SQL Server], failover clustering
- failover clustering [SQL Server], virtual servers
ms.assetid: 2a49d417-25fb-4760-8ae5-5871bfb1e6f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6144c7ef647f9108f9ac6619d971696b643e7648
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115747"
---
# <a name="rename-a-sql-server-failover-cluster-instance"></a>SQL Server 장애 조치(Failover) 클러스터 인스턴스 이름 변경
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 장애 조치 클러스터의 일부인 경우 가상 서버의 이름을 바꾸는 방법은 독립 실행형 인스턴스의 이름을 바꾸는 방법과 다릅니다. 자세한 내용은 [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)를 참조하세요.  
  
 가상 서버의 이름은 항상 SQL 네트워크 이름(SQL 가상 서버 네트워크 이름)과 동일합니다. 가상 서버의 이름은 바꿀 수 있지만 인스턴스 이름은 바꿀 수 없습니다. 예를 들어 VS1\instance1이라는 가상 서버 이름을 SQL35\instance1과 같은 다른 이름으로 바꿀 수 있지만 이름 중 인스턴스 부분인 instance1은 바뀌지 않습니다.  
  
 이름 바꾸기 프로세스를 시작하기 전에 아래 항목을 검토하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 복제와 함께 로그 전달을 사용하는 경우를 제외하고 복제 시 서버 이름 바꾸기를 지원하지 않습니다. 주 서버가 영구적으로 손실되면 로그 전달의 보조 서버 이름을 바꿀 수 있습니다. 자세한 내용은 [로그 전달 및 복제&#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)를 참조하세요.  
  
-   데이터베이스 미러링을 사용하도록 구성된 가상 서버 이름을 바꿀 때는 이름 바꾸기 작업을 수행하기 전에 데이터베이스 미러링을 해제한 다음 새로운 가상 서버 이름으로 데이터베이스 미러링을 다시 구성해야 합니다. 데이터베이스 미러링의 메타데이터는 새로운 가상 서버 이름을 반영하도록 자동으로 업데이트되지 않습니다.  
  
### <a name="to-rename-a-virtual-server"></a>가상 서버 이름을 바꾸려면  
  
1.  클러스터 관리자를 사용하여 SQL 네트워크 이름을 새 이름으로 바꿉니다.  
  
2.  네트워크 이름 리소스를 오프라인으로 만듭니다. 이 작업을 수행하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스와 다른 종속된 리소스도 오프라인이 됩니다.  
  
3.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 다시 온라인으로 만듭니다.  
  
## <a name="verify-the-renaming-operation"></a>이름 바꾸기 작업 확인  
 가상 서버 이름을 바꾼 후 이전 이름을 사용하던 연결은 새 이름을 사용하여 연결해야 합니다.  
  
 이러한 남은 작업이 완료되었는지 확인하기 위해 **@@servername** 또는 **sys.servers**에서 정보를 선택합니다. **@@servername** 함수는 새로운 가상 서버 이름을 반환하며 **sys.servers** 테이블은 새로운 가상 서버 이름을 표시합니다. 또한 장애 조치 프로세스가 새 이름으로 제대로 작동하는지 확인하기 위해 다른 노드에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스에 오류를 발생시켜 봐야 합니다.  
  
 클러스터 노드로부터의 연결에서는 새 이름을 거의 즉시 사용할 수 있습니다. 하지만 클라이언트 컴퓨터의 새 이름을 사용하는 연결에서는 새 이름이 클라이언트 컴퓨터에 표시되기 전까지 새 이름을 사용하여 서버에 연결할 수 없습니다. 새 이름이 네트워크를 통해 전파되는 데 필요한 시간은 몇 초 정도 걸릴 수 있으며 네트워크 구성에 따라 3-5분까지 걸릴 수도 있습니다. 이전 가상 서버 이름이 네트워크에서 사라지는 데에도 추가 시간이 걸릴 수 있습니다.  
  
 가상 서버 이름 바꾸기 작업에 따른 네트워크 전파 지연을 최소화하려면 다음과 같은 단계를 수행하십시오.  
  
#### <a name="to-minimize-network-propagation-delay"></a>네트워크 전파 지연을 최소화하려면  
  
1.  서버 노드의 명령 프롬프트에서 다음 명령을 실행합니다.  
  
    ```  
    ipconfig /flushdns  
    ipconfig /registerdns  
    nbtstat -RR  
    ```  
  
## <a name="additional-considerations-after-the-renaming-operation"></a>이름 바꾸기 작업 후 추가 고려 사항  
 장애 조치(Failover) 클러스터의 네트워크 이름을 바꾼 후에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 모든 시나리오를 지원하기 위해 다음 지침을 확인하고 수행해야 합니다.  
  
 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 서비스에 대한 아래의 추가 작업을 확인 및 수행합니다.  
  
-   SQL 에이전트가 이벤트를 전달하도록 구성된 경우 레지스트리 설정을 수정합니다. 자세한 내용은 [이벤트 전달 서버 지정&#40;SQL Server Management Studio&#41;](https://msdn.microsoft.com/library/81dfcbe4-3000-4e77-99de-bf85fef63a12)을 참조하세요.  
  
-   컴퓨터/클러스터 네트워크 이름을 바꿀 때 마스터 서버(MSX) 및 대상 서버(TSX) 인스턴스 이름을 수정합니다. 자세한 내용은 아래 항목을 참조하세요.  
  
    -   [마스터 서버에서 여러 대상 서버 제거](../../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
    -   [다중 서버 환경 만들기](../../../ssms/agent/create-a-multiserver-environment.md)  
  
-   업데이트된 서버 이름을 사용하여 로그를 백업 및 복원할 수 있도록 로그 전달을 다시 구성합니다. 자세한 내용은 아래 항목을 참조하세요.  
  
    -   [로그 전달 구성&#40;SQL Server&#41;](../../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
    -   [로그 전달 제거&#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   서버 이름을 기반으로 하는 작업 단계를 업데이트합니다. 자세한 내용은 [Manage Job Steps](../../../ssms/agent/manage-job-steps.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server의 독립 실행형 인스턴스를 호스트하는 컴퓨터 이름 바꾸기](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)  
  
  
