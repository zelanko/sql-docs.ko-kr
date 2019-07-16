---
title: Analytics Platform System 바이러스 백신 소프트웨어 | Microsoft Docs
description: 데이터 센터에서 바이러스 백신 소프트웨어에 필요한 경우 분석 플랫폼 시스템에 바이러스 백신 소프트웨어를 설치 하려면 이러한 지침을 따르세요. 데이터 센터의 요구 사항 확실 하지 않은 바이러스 백신 소프트웨어를 설치 하지 않는 것이 좋습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1e52841ebe96d8aab84e4d09c91b590e8e4d7e2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961601"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Analytics Platform System에 대 한 바이러스 백신 소프트웨어
데이터 센터에서 바이러스 백신 소프트웨어에 필요한 경우 분석 플랫폼 시스템에 바이러스 백신 소프트웨어를 설치 하려면 이러한 지침을 따르세요. 데이터 센터의 요구 사항 확실 하지 않은 바이러스 백신 소프트웨어를 설치 하지 않는 것이 좋습니다.  
  
> [!WARNING]  
> 각 컴퓨터에 대 한 및 Analytics Platform System 전체에 대 한 보안 위험을 개별적으로 평가 하는 선택한 각 컴퓨터의 보안 위험 수준에 대 한 적합 한 도구는 것이 좋습니다. 또한 바이러스 프로젝트 롤아웃하기 전에 내용을 안정성 및 성능을 측정 하는 전체 부하 상태에서 전체 시스템을 테스트 하는 것이 좋습니다.  
>   
> 바이러스 백신 소프트웨어 실행 하려면 일부 시스템 리소스가 필요 합니다. Analytics Platform System에 성능 영향을 주지 되는지 확인 하려면 바이러스 백신 소프트웨어를 설치한 후 테스트를 수행 해야 합니다.  
  
이 항목의 지침에 따라 됩니다 [SQL Server를 실행 하는 컴퓨터에서 실행 하도록 바이러스 백신 소프트웨어를 선택 하는 방법](https://support.microsoft.com/kb/309422) 하 고 [KB 문서 961804](https://support.microsoft.com/kb/961804/en-us)합니다.  
  
## <a name="exclusion-list-for-physical-hosts"></a>실제 호스트에 대 한 제외 목록  
실제 호스트에서 바이러스 백신 소프트웨어를 설치 하려면 다음과 같은 디렉터리 및 프로세스를 제외 합니다. 이러한는 바이러스 백신 소프트웨어가 검색 되지 않습니다.  
  
**이러한 디렉터리를 제외 합니다.**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-가상 컴퓨터 구성 디렉터리  
  
-   기본 가상 하드 디스크 드라이브 디렉터리 C:\Users\Public\Documents\Hyper-V\Virtual 하드 디스크  
  
-   C:\clusterStorage-가상 하드 디스크 드라이브 디렉터리  
  
**이러한 프로세스를 제외 합니다.**  
  
-   가상 컴퓨터 관리 (Vmms.exe)  
  
-   가상 컴퓨터 작업 프로세스 (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Virtual Machines (Vm)에 대 한 제외 목록  
Vm에서 바이러스 백신 소프트웨어를 설치 하려면 다음 목록을 디렉터리 및 파일을 제외 합니다. 이러한는 바이러스 백신 소프트웨어가 검색 되지 않습니다.  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01** 하 고  **_appliance_domain_-AD02**  
  
-   제한 없음  
  
**계산 노드 Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   제한 없음  
  
**_appliance_domain_-WDS**  
  
-   제한 없음  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>관련 항목  
[어플라이언스 관리 작업 &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
