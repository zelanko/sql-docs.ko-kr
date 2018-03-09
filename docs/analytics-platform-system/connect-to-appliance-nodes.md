---
title: "어플라이언스 노드 (분석 플랫폼 시스템)에 연결"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f975aa91-c816-4b29-89bf-923ab5b4abb4
caps.latest.revision: "19"
ms.openlocfilehash: 8d7a6f0def6b7cedb5bf7a7306fd10a3f167335e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-appliance-nodes"></a>어플라이언스 노드에 연결
이 항목에서는 분석 플랫폼 시스템 어플라이언스의 각 노드에 연결 하는 다양 한 방법에 설명 합니다.  
  
## <a name="connecting-with-hadoop"></a>Hadoop을 사용 하 여 연결  
Hadoop SQL Server PDW를 사용 하기 전에 SQL Server PDW에 Java Runtime Environment를 설치 하려면 기기 관리자에 게 문의 합니다. 자세한 내용은 [외부 데이터 &#40; PolyBase 연결 구성 분석 플랫폼 시스템 &#41; ](configure-polybase-connectivity-to-external-data.md) 기기 작업에서 가이드입니다.  
  
## <a name="ConnectingToIndividualNodes"></a>어플라이언스 노드에 연결  
각 기기 노드의 직접 액세스할 인 경우에 특정 사용 시나리오 및 특정 사용자 형식입니다. 다음 표에서 각 어플라이언스 노드 및 사용자가 해당 노드로 직접 연결 하는 시나리오를 나열 합니다.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Node**|**액세스 시나리오**|  
|제어 노드|웹 브라우저를 사용 하는 제어 노드에에서 실행 되는 관리 콘솔에 액세스 합니다. 자세한 내용은 참조 [관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41; ](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />모든 클라이언트 응용 프로그램 및 도구에는 이더넷 또는 InfiniBand 연결을 사용 하는지 여부에 관계 없이 제어 노드에 연결 합니다.<br /><br />컨트롤 노드 클러스터 IP 주소와 포트 사용 하는 제어 노드에 이더넷 연결을 구성 하려면 **17001**합니다. 예를 들어 "192.168.0.1,17001"가 있습니다.<br /><br />사용 하는 제어 노드에 InfiniBand 연결을 구성 하려면  ***appliance_domain*-SQLCTL01** 및 포트 **17001**합니다. 사용 하 여  ***appliance_domain*-SQLCTL01**, 기기 DNS 서버는 활성 InfiniBand 네트워크에 서버를 연결 합니다. 이 사용 하 여 비 어플라이언스 서버의 구성 하려면 참조 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)합니다.<br /><br />어플라이언스 관리자 하 관리 작업을 수행 하는 제어 노드에 연결 됩니다. 예를 들어 기기 관리자는 제어 노드에에서 다음 작업을 수행 합니다.<br /><br />분석 플랫폼 시스템으로 구성 된 **dwconfig.exe** 구성 도구입니다.|  
|계산 노드|제어 노드에 의해 방식 노드 연결을 계산 합니다. 계산 노드의 IP 주소가 매개 변수로 응용 프로그램 명령으로 입력 되지 됩니다.<br /><br />로드에 대 한 원격 테이블 복사본 및 Hadoop, SQL Server PDW 백업 보내거나 계산 노드 및 비 어플라이언스 노드 또는 서버 간의 직접 병렬로 데이터를 받을지 않습니다. 이러한 응용 프로그램에는 제어 노드에 연결 하 여 SQL Server PDW와 연결 하 고는 제어 노드에 계산 노드 및 비 어플라이언스 서버의 간의 통신을 설정 하려면 SQL Server PDW 보냅니다 하는 다음 키를 누릅니다.<br /><br />예를 들어 계산 노드에 직접 연결을 통해 동시에 이러한 데이터 전송 작업이 수행 됩니다.<br /><br />SQL Server PDW 로드 서버에서 로드할 수 있습니다.<br /><br />백업 서버에 SQL Server PDW에서 데이터베이스를 백업 합니다.<br /><br />SQL Server PDW에 백업 서버에서 데이터베이스를 복원 합니다.<br /><br />SQL Server PDW에서 Hadoop 데이터를 쿼리 합니다.<br /><br />SQL Server PDW에서 외부 Hadoop 테이블 데이터 내보내기.<br /><br />SMP SQL Server 데이터베이스를 원격으로 SQL Server PDW 테이블을 복사 합니다.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>이더넷 및 InfiniBand 네트워크에 연결  
원격 서버 기기 InfiniBand 네트워크를 통해 또는 이더넷 네트워크를 통해 연결할 수 있습니다. 성능상의 이유로, 서버, 로드, 서버 백업에 대 한 및 서버를 통해 데이터를 받는 **CREATE 원격 TABLE AS SELECT** 문, 일반적으로 어플라이언스에 InfiniBand 네트워크를 통해 데이터를 전송 합니다.  
  
고유한 고객 작업 그룹 또는 도메인에 속해야 하도록 비 어플라이언스 서버를 구성할 수 있으며 다음 자신의 고객 네트워크를 사용 하 여 해당 서버 및 데이터를 전송에 연결 하는 데 있습니다. 또한 비 어플라이언스 서버의 기기 InfiniBand에 연결 하는 옵션이; 기기 InfiniBand 네트워크를 통해 서로 데이터를 전송 이 때문에 기해야 SQL Server PDW의 성능이 느려질 수 있습니다.  
  
예를 들어이 문은 InfiniBand IP 주소가 192.168.0.1 백업 서버로 InfiniBand 통해 백업을 수행 하기 위한 네트워크 자격 증명을 추가 합니다. 어플라이언스 도메인은 *mypdw*, 문이 백업 서버에서 수행 됩니다. 이 명령문을 실행 하기 전에 고유한 매개 변수를 입력 해야 합니다.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
예를 들어 로드 명령을 다음으로 시작 됩니다.  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
