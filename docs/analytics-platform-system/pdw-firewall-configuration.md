---
title: PDW 방화벽 구성 (분석 플랫폼 시스템)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 191f292d-16bc-4166-b855-158854ad062d
caps.latest.revision: 28
ms.openlocfilehash: 8795f2254160a4ba605643b89dc4b9df0cce4c7f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-firewall-configuration"></a>PDW 방화벽 구성
**방화벽** SQL Server PDW 구성 관리자의 페이지를 사용 하도록 설정 하거나 허용 하거나 분석 플랫폼 시스템 어플라이언스에서 특정 포트에 액세스할 수 없도록 하는 방화벽 규칙을 사용 하지 않도록 수 있습니다.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>어플라이언스 노드에 대 한 규칙 포트 및 방화벽을 관리 하려면  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 참조 [구성 관리자를 시작 &#40;분석 플랫폼 시스템&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  구성 관리자의 왼쪽된 창에서 확장 **병렬 데이터 웨어하우스 토폴로지**, 클릭 하 고 **방화벽**합니다.  
  
3.  구성 목록에서 업데이트 한 다음 선택 하거나 해당 항목 옆에 있는 확인란의 선택을 취소 하는 포트 또는 방화벽 규칙을 찾습니다. SQL Server PDW 관리 구성 가능한 옵션이 포함 하 여 포트 외부에 있는 노드를이 목록에 표시 됩니다.  
  
4.  클릭 **적용** 변경 내용을 저장 합니다.  
  
![DWConfig 어플라이언스 PDW 방화벽](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>외부 포트  
PDW 외부에서 들어오는 클라이언트 연결에 대해 다음 포트가 열려 있습니다.  
  
|용도|포트 #|노드|  
|-----------|-----------|---------|  
|SQL 클라이언트 액세스에 대 한 PDW TDS)|17001|CTL|  
|로더 클라이언트 액세스 (dwloader 및 SSIS)|8001|CTL|  
|원격 데스크톱 액세스|3389|CTL, CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 암호화 (내부 통신을 관리 콘솔에 액세스 하 고 HDInsight 클러스터 서비스에 액세스할 수)에 대 한 연결|443|모든 노드|  
|SQL Server PDW 부하 제어 흐름-Windows 자격 증명|8002|CTL|  
|_Kerberos|88|AD01 및 AD02,|  
|_ldap|389|AD01 및 AD02|  
  
## <a name="internal-ports"></a>내부 포트  
다음 포트가 내부 통신을 위한 PDW에서 사용 되지만 PDW 어플라이언스에 외부에서 들어오는 연결을 열 수 없습니다.  
  
|용도|포트 #|노드|  
|-----------|-----------|---------|  
|컨트롤 채널 DMS 트래픽|16450|CTL, CMP|  
|데이터 채널 DMS 트래픽|16550|CTL, CMP|  
|내부 진단|16650|CTL, CMP|  
|장애 조치 상태 (DMS)|15000|CTL, CMP|  
|장애 조치 상태 (엔진)|15001|CMP|  
|동적 (임시) 포트 범위|20000-65535|CTL, CMP|  
|SQL Server 포트 범위 (TDS)|1433, 1500-1508|CTL, CMP|  
  
> [!NOTE]  
> 외부 테이블 또는 외부 데이터 원본을 만드는 TCP 포트 8020 기본적으로 사용 합니다. 이러한 문은 다른 포트를 대신 사용 하도록 구성할 수 있습니다. Hortonworks JOB_TRACKER_LOCATION 기본 포트는 50300 합니다. 다른 시스템 및 도구와 통합 하면 포트를 추가로 필요할 수 있습니다.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
