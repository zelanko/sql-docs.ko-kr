---
title: PDW 방화벽 구성
description: SQL Server PDW Configuration Manager의 방화벽 페이지를 사용 하 여 분석 플랫폼 시스템 어플라이언스의 특정 포트에 대 한 액세스를 허용 하거나 차단 하는 방화벽 규칙을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400879"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>분석 플랫폼 시스템의 병렬 데이터 웨어하우스 방화벽 구성

SQL Server PDW Configuration Manager의 **방화벽** 페이지를 사용 하 여 분석 플랫폼 시스템 어플라이언스의 특정 포트에 대 한 액세스를 허용 하거나 차단 하는 방화벽 규칙을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>어플라이언스 노드에 대 한 포트 및 방화벽 규칙을 관리 하려면  
  
1.  Configuration Manager를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  Configuration Manager 왼쪽 창에서 **병렬 데이터 웨어하우스 토폴로지**를 확장 한 다음 **방화벽**을 클릭 합니다.  
  
3.  구성 목록에서 업데이트할 포트 또는 방화벽 규칙을 찾은 다음 해당 항목 옆에 있는 확인란을 선택 하거나 선택 취소 합니다. 외부에 연결 된 노드에 대 한 열기 및 닫기를 비롯 하 여이 목록에는 SQL Server PDW 관리자 구성 가능 옵션만 표시 됩니다.  
  
4.  **적용** 을 클릭 하 여 변경 내용을 저장 합니다.  
  
![DWConfig 어플라이언스 PDW 방화벽](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>외부 포트  
PDW 외부에서 들어오는 클라이언트 연결에 대해 다음 포트가 열립니다.  
  
|목적|포트인 #|노드|  
|-----------|-----------|---------|  
|PDW에 대 한 SQL 클라이언트 액세스 (TDS)|17001|CTL|  
|로더 클라이언트 액세스 (dwloader & SSIS)|8001|CTL|  
|원격 데스크톱 액세스|3389|CTL, .CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|.CMP|  
|SSL로 암호화 된 연결 (관리 콘솔에 액세스 하기 위한 내부 통신의 경우)|443|모든 노드|  
|SQL Server PDW 부하 제어 흐름-Windows 자격 증명|8002|CTL|  
|_Kerberos|88|AD01 및 AD02,|  
|_ldap|389|AD01 및 AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>내부 포트  
다음 포트는 PDW에서 내부 통신용으로 사용 되지만 PDW 어플라이언스 외부에서 들어오는 연결에 대해서는 열리지 않습니다.  
  
|목적|포트인 #|노드|  
|-----------|-----------|---------|  
|DMS 제어 채널 트래픽|16450|CTL, .CMP|  
|DMS 데이터 채널 트래픽|16550|CTL, .CMP|  
|내부 진단|16650|CTL, .CMP|  
|장애 조치 (Failover) 상태 (DMS)|15000|CTL, .CMP|  
|장애 조치 (Failover) 상태 (엔진)|15001|.CMP|  
|동적 (임시) 포트 범위|20000-65535|CTL, .CMP|  
|SQL Server 포트 범위 (TDS)|1433, 1500-1508|CTL, .CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> 외부 테이블 또는 외부 데이터 원본을 만드는 경우 기본적으로 TCP 포트 8020이 사용 됩니다. 이러한 문은 대신 다른 포트를 사용 하도록 구성할 수 있습니다. Hortonworks JOB_TRACKER_LOCATION 기본 포트는 50300입니다. 다른 시스템 및 도구와 통합 하려면 추가 포트가 필요할 수 있습니다.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
