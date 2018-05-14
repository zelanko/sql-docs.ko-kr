---
title: CLUSTER.LOG(Always On 가용성 그룹) (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 01a9e3c1-2a5f-4b98-a424-0ffc15d312cf
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6e2cc0bda94d980535c014c1f52cf83f9ee80910
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="clusterlog-always-on-availability-groups"></a>CLUSTER.LOG(Always On 가용성 그룹)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  장애 조치(failover) 클러스터 리소스로서 SQL Server, WSFC(Windows Server 장애 조치(Failover) 클러스터) 서비스 클러스터 및 SQL Server 리소스 DLL(hadrres.dll) 간에는 SQL Server 내에서 모니터링할 수 없는 외부 상호 작용이 있습니다. WSFC 로그 CLUSTER.LOG는 WSFC 클러스터 또는 SQL Server 리소스 DLL의 문제를 진단할 수 있습니다.  
  
 다음 다이어그램은 가용성 그룹 리소스 만들기, 파괴 또는 상태 변경을 시작하는 SQL Server 및 Windows 클러스터 관리자 같은 응용 프로그램 간의 관계를 보여 줍니다.  
  
## <a name="generate-cluster-log"></a>클러스터 로그 생성  
 클러스터 로그를 두 가지 방법으로 생성할 수 있습니다.  
  
1.  명령 프롬프트에서 `cluster /log /g` 명령을 사용합니다. 이 명령은 각 WSFC 노드의 \windows\cluster\reports 디렉터리에 클러스터 로그를 생성합니다. 이 방법의 장점은 `/level` 옵션을 사용하여 생성된 로그의 세부 수준을 지정할 수 있다는 것입니다. 단점은 생성된 클러스터 로그에 대한 대상 디렉터리를 지정할 수 없다는 것입니다. 자세한 내용은 [Windows Server 2008 장애 조치(failover) 클러스터링에서 cluster.log를 만드는 방법](http://blogs.msdn.com/b/clustering/archive/2008/09/24/8962934.aspx)을 참조하세요.  
  
2.  [Get-ClusterLog](http://technet.microsoft.com/library/ee461045.aspx) PowerShell cmdlet을 사용합니다. 이 방법의 장점은 cmdlet에서 실행하는 노드의 모든 노드에서 한 대상 디렉터리까지 클러스터 로그를 생성할 수 있다는 것입니다. 단점은 생성된 로그의 세부 수준을 지정할 수 없다는 것입니다.  
  
 다음 PowerShell 명령은 최근 15분의 모든 클러스터 노드에서 클러스터 로그를 생성하고 현재 디렉터리에 저장합니다. 관리자 권한으로 PowerShell 창에서 명령을 실행합니다.  
  
```powershell  
Import-Modeul FailoverClusters   
Get-ClusterLog –TimeSpan 15 –Destination .  
```  
  
## <a name="always-on-log-verbosity"></a>Always On 로그의 자세한 정도  
 가용성 그룹에 대한 CLUSTER.LOG에서 로그의 자세한 정도를 증가시킬 수 있습니다. 자세한 정도를 수정하려면 아래 단계를 따릅니다.  
  
1.  **시작** 메뉴에서 **장애 조치(failover) 클러스터 관리자**를 엽니다.  
  
2.  클러스터 및 **서비스 및 응용 프로그램** 노드를 확장한 다음, 가용성 그룹 이름을 클릭합니다.  
  
3.  세부 정보 창에서 가용성 그룹 리소스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **속성** 탭을 클릭합니다.  
  
5.  **VerboseLogging** 속성을 수정합니다. 기본적으로 **VerboseLogging**은 정보, 경고 및 오류를 보고하는 `0`으로 설정됩니다. **VerboseLogging**은 `0`에서 `2`까지 설정할 수 있습니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  가용성 그룹 리소스를 다시 마우스 오른쪽 단추로 클릭하고 **이 리소스를 오프라인으로 만들기**를 클릭합니다.  
  
8.  가용성 그룹 리소스를 다시 마우스 오른쪽 단추로 클릭하고 **이 리소스를 온라인으로 만들기**를 클릭합니다.  
  
## <a name="availability-group-resource-events"></a>가용성 그룹 리소스 이벤트  
 아래 표는 가용성 그룹 리소스에 속하는 CLUSTER.LOG에서 볼 수 있는 다양한 이벤트 유형을 보여 줍니다. WSFC의 RHS(Resource Hosting Subsystem) 및 RCM(Resource Control Monitor)에 대한 자세한 내용은 [Windows Server 2008 장애 조치 클러스터의 RHS(Resource Hosting Subsystem)](http://blogs.technet.com/b/askcore/archive/2009/11/23/resource-hosting-subsystem-rhs-in-windows-server-2008-failover-clusters.aspx)를 참조하세요.  
  
|ID|원본|CLUSTER.LOG의 예|  
|----------------|------------|------------------------------|  
|`[RES]` 및 `[hadrag]` 접두사를 포함하는 메시지|hadrres.dll(Always On 리소스 DLL)|00002cc4.00001264::2011/08/05-13:47:42.543 INFO  [RES] SQL Server 가용성 그룹 \<ag>: `[hadrag]` 오프라인 요청.<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.558 ERR   [RES] SQL Server 가용성 그룹 \<ag>: `[hadrag]` 임대 스레드 종료<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.605 INFO  [RES] SQL Server 가용성 그룹 \<ag>: `[hadrag]` 무료 SQL 명령문<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.902 INFO  [RES] SQL Server 가용성 그룹 \<ag>: `[hadrag]` SQL Server에서 연결 끊기|  
|`[RHS]` 접두사를 포함한 메시지|RHS.EXE(리소스 호스팅 하위 시스템, hadrres.dll의 호스트 프로세스)|00000c40.00000a34::2011/08/10-18:42:29.498 INFO  [RHS] 리소스 ag가 오프라인 상태가 되었습니다. RHS는 RCM에 대한 리소스 상태를 보고할 것입니다.|  
|`[RCM]` 접두사를 포함한 메시지|리소스 제어 메시지(클러스터 서비스)|000011d0.00000f80::2011/08/05-13:47:42.480 INFO  [RCM] rcm::RcmGroup::Move: 먼저 그룹 'ag'를 오프라인으로 만듭니다...<br /><br /> 000011d0.00000f80::2011/08/05-13:47:42.496 INFO  [RCM] TransitionToState(ag) Online-->OfflineCallIssued.|  
|RcmApi/ClusAPI|대부분의 경우 SQL Server를 의미하는 API 호출이 작업을 요청|000011d0.00000f80::2011/08/05-13:47:42.465 INFO  [RCM] rcm::RcmApi::MoveGroup: (ag, 2)|  
  
## <a name="debug-always-on-resource-dll-in-isolation"></a>분리 상태에서 Always On 리소스 DLL 디버그  
 Always On 리소스 DLL(hadrres.dll)을 다른 리소스 DLL과 분리된 상태에서 실행하도록 클러스터를 구성하는 것이 디버깅 모범 사례입니다. 기본적으로 WSFC 클러스터는 모든 리소스 DLL을 rhs.exe의 단일 인스턴스에서 실행합니다. 이렇게 하면 클러스터 내의 모든 리소스가 같은 rhs.exe 인스턴스를 공유합니다. 디버거를 사용하여 hadrres.dll의 디버그를 시도하는 경우, 중단점에서 일시 중지하면 rhs.exe 인스턴스를 공유하는 다른 리소스도 일시 중지할 수 있습니다. 또한 같은 클러스터에서 여러 가용성 그룹을 실행하면 같은 구성 때문에 한 가용성 그룹을 디버그하기 위해 중단점에서 일시 중지할 때 모든 가용성 그룹이 일시 중지할 수 있습니다.  
  
 가용성 그룹을 다른 클러스터 리소스 DLL(다른 가용성 그룹 포함)과 분리하려면 다음을 수행하여 별도의 rhs.exe 프로세스 내에서 hadrres.dll을 실행합니다.  
  
1.  **레지스트리 편집기**를 열고 다음 키를 탐색합니다. HKEY_LOCAL_MACHINE\Cluster\Resources. 이 키는 각각 서로 다른 GUID를 가진 모든 리소스에 대한 키를 포함합니다.  
  
2.  가용성 그룹 이름과 일치하는 **이름**을 포함한 리소스 키를 찾습니다.  
  
3.  **SeparateMonitor** 값을 **1**로 변경합니다.  
  
4.  WSFC 클러스터에서 가용성 그룹에 대한 클러스터형 서비스를 다시 시작합니다.  
  
  