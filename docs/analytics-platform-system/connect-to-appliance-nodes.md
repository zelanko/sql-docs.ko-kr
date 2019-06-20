---
title: Analytics Platform System appliance 노드에서 연결할 | Microsoft Docs
description: 이 문서는 분석 플랫폼 시스템 어플라이언스의 각 노드에 연결 하는 여러 가지를 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 873ce3cf5ad2707979d66068b3930d6f59f7057c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66186800"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 어플라이언스 노드에 연결
이 문서는 분석 플랫폼 시스템 어플라이언스의 각 노드에 연결 하는 여러 가지를 설명 합니다.  
  
## <a name="connecting-with-hadoop"></a>Hadoop을 사용 하 여 연결  
SQL Server PDW에서 Hadoop 사용 하기 전에 SQL Server PDW에 Java Runtime Environment를 설치 하려면 어플라이언스 관리자에 게 문의 합니다. 자세한 내용은 [외부 데이터에 PolyBase 연결 구성 &#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md) 어플라이언스 운영 가이드의 합니다.  
  
## <a name="ConnectingToIndividualNodes"></a>어플라이언스 노드에 연결  
각 어플라이언스 노드에 직접 액세스는 특정 사용자가 입력 하 고 특정 사용 시나리오에만 합니다. 다음 표에서 각 어플라이언스 노드 및 사용자가 해당 노드로 직접 연결 하는 시나리오를 나열 합니다.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 제품 팀 이나 AP 고객 지원 팀의 명시적 동의 없이 컨트롤 또는 계산 노드에 대 한 데이터베이스 또는 테이블 설정을 변경 하면 지원 되지 않는 APS 어플라이언스를 해석할 수 있습니다.
  
|||  
|-|-|  
|**Node**|**액세스 시나리오**|  
|제어 노드|웹 브라우저를 사용 하 여 제어 노드에서 실행 되는 관리 콘솔에 액세스 합니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다.<br /><br />모든 클라이언트 응용 프로그램 및 도구에는 이더넷 또는 InfiniBand 연결에서 사용 하는 여부에 관계 없이 제어 노드에 연결 합니다.<br /><br />제어 노드에 이더넷 연결을 구성 하려면 제어 노드 클러스터 IP 주소 및 포트를 사용할 **17001**합니다. 예를 들어, "192.168.0.1,17001"가 있습니다.<br /><br />제어 노드에 InfiniBand 연결을 구성 하려면 사용 하 여  <strong>*appliance_domain*-SQLCTL01</strong> 및 포트 **17001**합니다. 사용 하 여  <strong>*appliance_domain*-SQLCTL01</strong>, 어플라이언스 DNS 서버 active InfiniBand 네트워크에 서버를 연결 합니다. 이 사용 하 여 비 어플라이언스 서버를 구성 하려면 참조 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)합니다.<br /><br />어플라이언스 관리자 관리 작업을 수행 하는 제어 노드에 연결할 수 있습니다. 예를 들어, 어플라이언스 관리자는 제어 노드에서 다음 작업을 수행합니다.<br /><br />Analytics Platform System을 사용 하 여 구성 합니다 **dwconfig.exe** 구성 도구입니다.|  
|컴퓨팅 노드|계산 노드 연결 제어 노드에 의해 전달 됩니다. 계산 노드의 IP 주소 매개 변수로 응용 프로그램 명령으로 입력 되지 됩니다.<br /><br />를 로드 하기 위해 원격 테이블 복사 및 Hadoop, SQL Server PDW 백업 보내거나 병렬 계산 노드 및 비 어플라이언스 노드 또는 서버 사이 직접 데이터를 받고지 않습니다. 이러한 응용 프로그램에 제어 노드에 연결 하 여 SQL Server PDW를 사용 하 여 연결 및 그런 다음 제어 노드에 계산 노드 및 비 어플라이언스 서버 간의 통신을 설정 하려면 SQL Server PDW를 전달 합니다.<br /><br />예를 들어, 이러한 데이터 전송 작업이 계산 노드에 직접 연결을 사용 하 여 병렬로 수행 됩니다.<br /><br />SQL Server PDW 로드 서버에서 로드할 수 있습니다.<br /><br />백업 서버에 SQL Server PDW에서 데이터베이스를 백업 합니다.<br /><br />SQL Server PDW에 백업 서버에서 데이터베이스를 복원 합니다.<br /><br />SQL Server PDW에서 Hadoop 데이터를 쿼리 합니다.<br /><br />SQL Server PDW에서 외부 Hadoop 테이블에 데이터를 내보내는 중입니다.<br /><br />원격 SMP SQL Server 데이터베이스를 SQL Server PDW 테이블을 복사합니다.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>이더넷 및 InfiniBand 네트워크에 연결  
원격 서버에는 어플라이언스 InfiniBand 네트워크를 통해 또는 이더넷 네트워크를 통해 연결할 수 있습니다. 성능상의 이유로 서버 로드 서버를 백업 및 서버를 통해 데이터를 받는 **만들 REMOTE TABLE AS SELECT** 문, 일반적으로 어플라이언스 InfiniBand 네트워크를 통해 데이터를 전송 합니다.  
  
고유한 고객 작업 그룹 또는 도메인에 속한 비 어플라이언스 서버를 구성 하 고 고유한 고객 네트워크를 사용 하 여 해당 서버 및 전송 데이터에 연결할 수 있습니다. 또한 비 어플라이언스 서버 InfiniBand 기기에 연결 하는 옵션이 어플라이언스 InfiniBand 네트워크를 통해 서로 데이터를 전송 SQL Server PDW의 성능이 떨어질 수 있으므로 주의 해야 합니다.  
  
예를 들어이 문은 InfiniBand IP 주소가 192.168.0.1는 백업 서버로 InfiniBand 통해 백업을 수행 하는 것에 대 한 네트워크 자격 증명을 추가 합니다. 어플라이언스 도메인이 *mypdw*, 문은 백업 서버에서 수행 됩니다. 이 명령문을 실행 하기 전에 사용자 고유의 매개 변수를 입력 해야 합니다.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
예를 들어, 다음을 사용 하 여 로드 명령을 시작 됩니다.  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
