---
title: PDW 방화벽 구성-Analytics Platform System | Microsoft Docs
description: SQL Server PDW 구성 관리자의 방화벽 페이지를 허용 하거나 Analytics Platform System appliance에서 특정 포트에 대 한 액세스를 방지 하는 방화벽 규칙을 사용할지 수 있습니다.
aauthor: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3195007b4346c6010b416fae833643f3a80136fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639539"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Analytics Platform System의 병렬 데이터 웨어하우스 방화벽 구성
합니다 **방화벽** SQL Server PDW 구성 관리자의 페이지를 사용 하면 허용 하거나 Analytics Platform System appliance에서 특정 포트에 대 한 액세스를 방지 하는 방화벽 규칙을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>어플라이언스 노드에 대 한 규칙을 포트 및 방화벽을 관리 하려면  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  구성 관리자의 왼쪽된 창에서 확장 **병렬 데이터 웨어하우스 토폴로지**를 클릭 하 고 **방화벽**합니다.  
  
3.  구성 목록에서 업데이트 한 다음 선택 하거나 해당 항목 옆에 있는 확인란의 선택을 취소 하는 포트 또는 방화벽 규칙을 찾습니다. SQL Server PDW 구성 관리자 옵션만 열기 및 닫기 노드 외부에서 포트를 포함 하 여이 목록에 표시 됩니다.  
  
4.  클릭 **적용** 변경 내용을 저장 합니다.  
  
![DWConfig 어플라이언스 PDW 방화벽](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>외부 포트  
PDW 외부에서 들어오는 클라이언트 연결에 대해 다음 포트가 열립니다.  
  
|용도|포트 #|노드|  
|-----------|-----------|---------|  
|PDW (TDS)에 대 한 SQL 클라이언트 액세스|17001|CTL|  
|로더 클라이언트 액세스 (dwloader 및 SSIS)|8001|CTL|  
|원격 데스크톱 액세스|3389|CTL, CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 암호화 (관리자 콘솔에 액세스 하는 내부 통신)에 대 한 연결|443|모든 노드|  
|SQL Server PDW 부하 제어 흐름-Windows 자격 증명|8002|CTL|  
|_Kerberos|88|AD01 및 AD02,|  
|_ldap|389|AD01 및 AD02|  
  
## <a name="internal-ports"></a>내부 포트  
다음 포트를 내부 통신을 위한 PDW에서 사용 되지만 PDW 어플라이언스에 외부에서 들어오는 연결에 대 한 열리지 않습니다.  
  
|용도|포트 #|노드|  
|-----------|-----------|---------|  
|DMS 컨트롤 채널 트래픽|16450|CTL, CMP|  
|DMS 데이터 채널 트래픽|16550|CTL, CMP|  
|내부 진단|16650|CTL, CMP|  
|장애 조치 상태 (DMS)|15000|CTL, CMP|  
|장애 조치 상태 (엔진)|15001|CMP|  
|(임시) 동적 포트 범위|20000-65535|CTL, CMP|  
|SQL Server 포트 범위 (TDS)|1433, 1500-1508|CTL, CMP|  
  
> [!NOTE]  
> 외부 테이블 또는 외부 데이터 원본 만들기는 기본적으로 TCP 포트 8020을 사용 합니다. 이러한 문은 다른 포트를 대신 사용 하도록 구성할 수 있습니다. Hortonworks JOB_TRACKER_LOCATION 기본 포트가 50300입니다. 다른 시스템 및 도구와 통합 하면 포트를 추가로 필요할 수 있습니다.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
