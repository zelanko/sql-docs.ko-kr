---
title: 어플라이언스 노드에 연결
description: 이 문서에서는 분석 플랫폼 시스템 어플라이언스의 각 노드에 연결 하는 다양 한 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401242"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 어플라이언스 노드에 연결
이 문서에서는 분석 플랫폼 시스템 어플라이언스의 각 노드에 연결 하는 다양 한 방법을 설명 합니다.  
  
## <a name="connecting-with-hadoop"></a>Hadoop과 연결  
SQL Server PDW에서 Hadoop을 사용 하려면 먼저 장치 관리자에 게 SQL Server PDW에 Java Runtime Environment를 설치 하도록 요청 하세요. 자세한 내용은 어플라이언스 작업 가이드에서 [외부 데이터에 대 한 PolyBase 연결 &#40;분석 플랫폼 시스템&#41;을](configure-polybase-connectivity-to-external-data.md) 참조 하세요.  
  
## <a name="connecting-to-appliance-nodes"></a><a name="ConnectingToIndividualNodes"></a>어플라이언스 노드에 연결  
각 어플라이언스 노드는 특정 사용 시나리오 및 특정 사용자 형식 에서만 직접 액세스 됩니다. 다음 표에서는 각 어플라이언스 노드 및 사용자가 해당 노드에 직접 연결 하는 시나리오를 보여 줍니다.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 제품 팀 또는 AP 고객 지원 팀에 게 명시적으로 동의 하지 않고 제어 또는 계산 노드의 데이터베이스 또는 테이블 설정을 변경 하면 AP 기기가 지원 되지 않을 수 있습니다.
  
|||  
|-|-|  
|**노드**|**액세스 시나리오**|  
|제어 노드|웹 브라우저를 사용 하 여 제어 노드에서 실행 되는 관리 콘솔에 액세스 합니다. 자세한 내용은 [관리 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)을 참조 하세요.<br /><br />모든 클라이언트 응용 프로그램 및 도구는 연결에서 이더넷 또는 InfiniBand를 사용 하는지 여부에 관계 없이 제어 노드에 연결 합니다.<br /><br />제어 노드에 대 한 이더넷 연결을 구성 하려면 제어 노드 클러스터 IP 주소와 포트 **17001**을 사용 합니다. 예를 들면 "192.168.0.1, 17001"입니다.<br /><br />Control 노드에 대 한 InfiniBand 연결을 구성 하려면 <strong> *appliance_domain*-SQLCTL01</strong> 및 포트 **17001**을 사용 합니다. SQLCTL01를 사용 <strong> *appliance_domain*</strong>하 여 어플라이언스 DNS 서버가 활성 InfiniBand 네트워크에 서버를 연결 합니다. 이를 사용 하도록 어플라이언스 서버가 아닌 서버를 구성 하려면 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)을 참조 하세요.<br /><br />어플라이언스 관리자는 제어 노드에 연결 하 여 관리 작업을 수행 합니다. 예를 들어 어플라이언스 관리자는 제어 노드에서 다음 작업을 수행 합니다.<br /><br />**Dwconfig .exe** 구성 도구를 사용 하 여 분석 플랫폼 시스템을 구성 합니다.|  
|컴퓨팅 노드|계산 노드 연결은 제어 노드에 의해 전달 됩니다. 계산 노드의 IP 주소는 매개 변수로 응용 프로그램 명령에 입력 되지 않습니다.<br /><br />로드, 백업, 원격 테이블 복사 및 Hadoop의 경우, SQL Server PDW는 계산 노드와 비 어플라이언스 노드 또는 서버 간에 데이터를 직접 병렬로 보내고 받습니다. 이러한 응용 프로그램은 제어 노드에 연결 하 여 SQL Server PDW에 연결 하 고, 컨트롤 노드는 계산 노드와 비 어플라이언스 서버 간의 통신을 설정 하도록 SQL Server PDW를 지시 합니다.<br /><br />예를 들어 이러한 데이터 전송 작업은 계산 노드에 대 한 직접 연결을 통해 병렬로 수행 됩니다.<br /><br />로드 서버에서 SQL Server PDW 로드 하는 중입니다.<br /><br />SQL Server PDW에서 백업 서버로 데이터베이스를 백업 합니다.<br /><br />백업 서버에서 SQL Server PDW로 데이터베이스 복원<br /><br />SQL Server PDW에서 Hadoop 데이터를 쿼리 합니다.<br /><br />SQL Server PDW에서 외부 Hadoop 테이블로 데이터를 내보냅니다.<br /><br />SQL Server PDW 테이블을 원격 SMP SQL Server 데이터베이스로 복사|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>이더넷 및 InfiniBand 네트워크에 연결  
원격 서버는 어플라이언스 InfiniBand 네트워크 또는 이더넷 네트워크를 통해 연결할 수 있습니다. 성능상의 이유로, **CREATE REMOTE TABLE AS SELECT** 문을 통해 데이터를 수신 하는 서버, 백업 서버 및 서버를 로드 하는 것은 일반적으로 어플라이언스 InfiniBand 네트워크를 통해 데이터를 전송 합니다.  
  
자신의 고객 작업 그룹 또는 도메인에 포함 하도록 비 어플라이언스 서버를 구성한 다음 해당 서버에 연결 하 여 데이터를 전송 하는 데 고유한 고객 네트워크를 사용할 수 있습니다. 또한 어플라이언스 InfiniBand에 연결 된 비 어플라이언스 서버는 어플라이언스 InfiniBand 네트워크를 통해 서로 데이터를 전송 하는 옵션을 사용할 수 있습니다. 이는 SQL Server PDW의 성능을 저하 시킬 수 있기 때문에 주의 해야 합니다.  
  
예를 들어,이 문은 InfiniBand IP 주소가 192.168.0.1 인 백업 서버에 InfiniBand를 통해 백업을 수행 하기 위한 네트워크 자격 증명을 추가 합니다. 어플라이언스 도메인은 *mypdw*백업 서버에서 수행 됩니다. 이 문을 실행 하기 전에 매개 변수를 직접 입력 해야 합니다.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
예를 들어 로드 명령은 다음과 같이 시작 됩니다.  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
