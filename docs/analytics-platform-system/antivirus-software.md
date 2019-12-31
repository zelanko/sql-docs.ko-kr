---
title: 바이러스 백신 소프트웨어
description: 데이터 센터에 바이러스 백신 소프트웨어가 필요한 경우 다음 지침을 사용 하 여 AP (Analytics Platform System)에 바이러스 백신 소프트웨어를 설치 합니다. 데이터 센터의 기업 요구 사항이 아닌 경우에는 바이러스 백신 소프트웨어를 설치 하지 않는 것이 좋습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401469"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>Analytics Platform System (APS)의 바이러스 백신 소프트웨어
데이터 센터에 바이러스 백신 소프트웨어가 필요한 경우 다음 지침을 사용 하 여 분석 플랫폼 시스템에 바이러스 백신 소프트웨어를 설치 합니다. 데이터 센터의 기업 요구 사항이 아닌 경우에는 바이러스 백신 소프트웨어를 설치 하지 않는 것이 좋습니다.  
  
> [!WARNING]  
> 각 컴퓨터와 분석 플랫폼 시스템에 대해 개별적으로 보안 위험을 평가 하 고 각 컴퓨터의 보안 위험 수준에 적절 한 도구를 선택 하는 것이 좋습니다. 또한 바이러스 방지 프로젝트를 배포 하기 전에 전체 부하에서 전체 시스템을 테스트 하 여 안정성 및 성능의 변화를 측정 하는 것이 좋습니다.  
>   
> 바이러스 방지 소프트웨어를 실행 하려면 일부 시스템 리소스가 필요 합니다. 분석 플랫폼 시스템에 성능 영향이 있는지 확인 하려면 바이러스 백신 소프트웨어를 설치 하기 전후에 테스트를 수행 해야 합니다.  
  
이 항목은 SQL Server를 실행 하는 [컴퓨터에서 실행 하는 바이러스 백신 소프트웨어를 선택 하는 방법](https://support.microsoft.com/kb/309422) 에 대 한 지침과 [KB 문서 961804](https://support.microsoft.com/kb/961804/en-us)을 기반으로 합니다.  
  
## <a name="exclusion-list-for-physical-hosts"></a>실제 호스트의 제외 목록  
실제 호스트에 바이러스 백신 소프트웨어를 설치 하려면 다음 디렉터리 및 프로세스 목록을 제외 합니다. 이는 바이러스 백신 소프트웨어에서 검사 하면 안 됩니다.  
  
**다음 디렉터리를 제외 합니다.**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-가상 머신 구성 디렉터리  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual 하드 디스크-기본 가상 하드 디스크 드라이브 디렉터리  
  
-   C:\clusterStorage-가상 하드 디스크 드라이브 디렉터리  
  
**다음 프로세스를 제외 합니다.**  
  
-   가상 컴퓨터 관리 (Vmms)  
  
-   가상 컴퓨터 작업 프로세스 (Vmwp .exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Vm (Virtual Machines)에 대 한 제외 목록  
Vm에 바이러스 백신 소프트웨어를 설치 하려면 다음 디렉터리와 파일 목록을 제외 합니다. 이는 바이러스 백신 소프트웨어에서 검사 하면 안 됩니다.  
  
**_PDW_region_-CTL01**  
  
-   C:\a\  
  
-   G:\  
  
**_appliance_domain_-AD01** 및 ** _appliance_domain_-AD02**  
  
-   제한 없음  
  
**계산 노드 Vm**  
  
-   C:\a\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   제한 없음  
  
**_appliance_domain_-WDS**  
  
-   제한 없음  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>참고 항목  
[기기 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
