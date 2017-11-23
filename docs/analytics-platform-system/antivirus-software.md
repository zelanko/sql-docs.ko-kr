---
title: "바이러스 백신 소프트웨어 (분석 플랫폼 시스템)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60ab9a88-d339-4917-a38b-f9481aef38fd
caps.latest.revision: "29"
ms.openlocfilehash: f1d5c81381b486ec89198fed6aa22ccff22a544a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="antivirus-software"></a>바이러스 백신 소프트웨어
데이터 센터 바이러스 백신 소프트웨어를 필요한 경우 분석 플랫폼 시스템에 바이러스 백신 소프트웨어를 설치 하려면 다음이 지침을 사용 합니다. 데이터 센터의 절대적인 요구 하는 경우 바이러스 백신 소프트웨어를 설치 하지 않는 것이 좋습니다.  
  
> [!WARNING]  
> 개별적으로 각 컴퓨터에 대 한 고 전체적으로 분석 플랫폼 시스템에 대 한 보안 위험을 평가 하 고 있는 각 컴퓨터의 보안 위험 수준에 대 한 적절 한 도구를 선택 하는 것이 좋습니다. 또한, 바이러스 방지 프로젝트를 배포 하기 전에 변경 내용을 안정성과 성능을 측정 하는 전체 부하에서 전체 시스템을 테스트 하는 것이 좋습니다.  
>   
> 바이러스 백신 소프트웨어 실행 일부 시스템 리소스가 필요 합니다. 분석 플랫폼 시스템에 성능 영향 있는지 여부를 확인 하도록 바이러스 백신 소프트웨어를 설치한 후 및 하기 전에 테스트를 수행 해야 합니다.  
  
이 항목의 지침에 따라 [SQL Server를 실행 하는 컴퓨터에서 실행 하도록 바이러스 백신 소프트웨어를 선택 하는 방법](http://support.microsoft.com/kb/309422) 및 [KB 문서 961804](http://support.microsoft.com/kb/961804/en-us)합니다.  
  
## <a name="exclusion-list-for-physical-hosts"></a>물리적 호스트에 대 한 제외 목록  
실제 호스트에서 바이러스 백신 소프트웨어를 설치 하려면 다음과 같은 디렉터리 및 프로세스를 제외 합니다. 이러한 해야 바이러스 백신 소프트웨어에 의해 검색 되지 않습니다.  
  
**이러한 디렉터리를 제외 합니다.**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-가상 컴퓨터 구성 디렉터리  
  
-   기본 가상 하드 디스크 드라이브 디렉터리-C:\Users\Public\Documents\Hyper-V\Virtual 하드 디스크  
  
-   C:\clusterStorage-가상 하드 디스크 드라이브 디렉터리  
  
**이러한 프로세스를 제외 합니다.**  
  
-   가상 컴퓨터 관리 (Vmms.exe)  
  
-   가상 컴퓨터 작업 프로세스 (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>가상 컴퓨터 (Vm)에 대 한 제외 목록  
Vm에서 바이러스 백신 소프트웨어를 설치 하려면 다음과 같은 디렉터리 및 파일을 제외 합니다. 이러한 해야 바이러스 백신 소프트웨어에 의해 검색 되지 않습니다.  
  
***PDW_region*-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-AD01** 및  ***appliance_domain*-AD02**  
  
-   제한 없음  
  
**계산 노드 Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   제한 없음  
  
***appliance_domain*-WDS**  
  
-   제한 없음  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>관련 항목:  
[어플라이언스 관리 작업 &#40; 분석 플랫폼 시스템 &#41;](appliance-management-tasks.md)  
  
