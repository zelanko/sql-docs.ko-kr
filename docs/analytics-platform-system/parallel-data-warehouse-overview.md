---
title: "병렬 데이터 웨어하우스 개요"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "이 항목에서는 원격 클라이언트 컴퓨터 및 분석 플랫폼 시스템의 비 어플라이언스 소프트웨어 구성 요소를 설명 합니다."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: db0c4a43-a66d-4c44-ab91-791c5785f71c
caps.latest.revision: "20"
ms.openlocfilehash: 587b1ce6720fc07d9ac24edde2c5b8cc2b30c89f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="parallel-data-warehouse-overview"></a>병렬 데이터 웨어하우스 개요
이 항목에서는 원격 클라이언트 컴퓨터 및 분석 플랫폼 시스템의 비 어플라이언스 소프트웨어 구성 요소를 설명 합니다.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![병렬 데이터 웨어하우스 소프트웨어](media/parallel-data-warehouse-software.png "병렬 데이터 웨어하우스 소프트웨어")  
  
## <a name="sec1"></a>원격 클라이언트 컴퓨터 – 쿼리 처리 및 사용자 데이터 저장  
  
### <a name="control-node"></a>제어 노드  
MPP 엔진  
MPP 엔진에는 방대한 병렬 처리 (MPP) 시스템의 브레인입니다. 메서드는 다음 작업을 수행합니다.  
  
-   병렬 쿼리 계획을 작성 하 고 계산 노드에 대 한 병렬 쿼리 실행을 조정 합니다.  
  
-   저장 하 고 모든 데이터베이스에 대 한 메타 데이터 및 구성 데이터를 조정 합니다.  
  
-   SQL Server PDW 데이터베이스 인증 및 권한 부여를 관리합니다.  
  
-   하드웨어 및 소프트웨어 상태를 추적합니다.  
  
### <a name="data-movement-service-dms"></a>데이터 이동 서비스 (DMS)  
데이터 이동 서비스 (DMS)의 "방법" PDW의 일부입니다. 메서드는 다음 작업을 수행합니다.  
  
-   SQL Server PDW 노드 간에 데이터를 전송합니다.  
  
-   프로세스 노드 사이 데이터를 전송 해야 하는 작업을 쿼리 합니다.  
  
-   데이터 전송 속도 최적화 하 여 쿼리 성능을 향상 시킵니다.  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 웹 응용 프로그램은 합니다.  
  
### <a name="configuration-manager"></a>구성 관리자  
Configuration Manager (dwconfig.exe)는 분석 플랫폼 시스템을 구성 하려면 기기 관리자를 사용 하는 도구입니다.  
  
### <a name="control-node-databases"></a>컨트롤 노드 데이터베이스  
SQL Server에는 제어 노드에 있는 데이터베이스의 모든 관리 합니다.  
  
-   셸 데이터베이스는 분산된 된 사용자는 모든 데이터베이스에 대 한 메타 데이터를 관리 합니다.  
  
-   TempDB 기기에서 모든 사용자의 임시 테이블에 대 한 메타 데이터를 포함 합니다.  
  
-   마스터는 제어 노드에 SQL Server에 대 한 마스터 테이블입니다.  
  
### <a name="compute-node"></a>계산 노드  
계산 노드는 병렬 데이터 처리 및 저장소 단위입니다. SQL Server를 사용 하 여 사용자 데이터를 관리 및 직접 연결된 저장소는 합니다.  
  
### <a name="data-movement-service-dms"></a>데이터 이동 서비스 (DMS)  
데이터 이동 서비스 (DMS) 다음을 수행 하려면 각 계산 노드에서 실행 됩니다.  
  
-   병렬 쿼리 처리의 일부로 DMS 제어 노드 및 다른 컴퓨터 노드 간에 데이터를 전송 합니다.  
  
-   각 계산 노드에서 실행 DMS 동시에 데이터 로드를 받습니다. 데이터는 계산 노드 로드 서버에서 직접 병렬로 로드 됩니다.  
  
-   DMS 각 계산 노드에서 백업 서버에 직접 데이터를 전송합니다.  
  
-   PolyBase를 사용 하 여 DMS 어플라이언스에서 하 고는 외부 Hadoop 클러스터 또는 HDInsight 영역에서 데이터를 전송 합니다.  
  
### <a name="compute-node-databases"></a>계산 노드 데이터베이스 
각 계산 노드에 쿼리를 처리 하 고 사용자 데이터를 관리 하도록 SQL server 인스턴스를 실행 합니다.  
  
## <a name="appliance-fabric"></a>어플라이언스 패브릭  
어플라이언스 패브릭 어플라이언스에 대 한 운영 체제, 서비스 및 네트워크 인프라를 제공합니다.  
  
### <a name="domain-controller"></a>도메인 컨트롤러  
Active Directory (AD) 도메인 서비스 (DS)  
분석 플랫폼 시스템 분석 플랫폼 시스템 노드 간에 인증을 수행 하 고 SQL Server PDW Windows 인증 로그인의 인증을 관리 합니다.  
  
DNS 서비스  
분석 플랫폼 시스템 어플라이언스에 대 한 IP 주소에 도메인 이름을 확인 하는 Windows 서비스 DNS (Domain Name) 합니다.  
  
### <a name="windows-deployment-service"></a>Windows 배포 서비스  
Windows 배포 서비스 (WDS) 어플라이언스에 Windows Server 운영 체제를 배포합니다. 어플라이언스를 통해 모든 호스트 및 가상 컴퓨터에 배포 합니다.  
  
DHCP 서비스 기기 도메인 내에서 호스트 미리 구성 된 IP 주소를 사용 하지 않고도 기기 네트워크에 참가할 수 있도록 IP 주소를 만듭니다.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
분석 플랫폼 시스템 가상화를 사용 하 여 가용성을 높이기 위해. Virtual Machine Manager는 물리적 호스트에 운영 체제를 배포 하기 위해 System Center를 호스팅합니다.  
  
WSUS Windows Server Update Services ()을 적용 하거나 모든 호스트 및 가상 컴퓨터에서 Windows 업데이트를 제거 합니다.  
  
### <a name="windows-server"></a>Windows Server  
모든 호스트 및 가상 컴퓨터 기기에서 Windows Server 운영 체제를 실행합니다.  
  
### <a name="failover-clustering"></a>장애 조치(Failover) 클러스터링  
Windows 장애 조치 클러스터링에 호스트 오류가 수동 호스트에는 프로세스를 다시 시작 하는 기능을 제공 합니다.  
  
### <a name="storage-spaces"></a>저장소 공간  
Windows 저장소 공간 계산 노드의 작은 그룹에 대 한 저장소 풀으로 사용자 데이터를 관리합니다. 계산 노드에 오류가 발생 하는 경우 해당 데이터를 그룹에 다른 계산 노드를 통해 액세스할 수 있습니다.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-v Server는 간단 하 고 신뢰할 수 있는 가상화 솔루션을 제공합니다. 분석 플랫폼 시스템 가상화를 사용 하 여 CPU 리소스를 분산 하 고 패브릭 구성 요소 기기 고 PDW 노드에 대 한 고가용성을 제공 합니다.  
  
## <a name="sec2"></a>비관계형 데이터
SQL Server PDW 데이터 외부 Hadoop 데이터와 통합 하려면 PolyBase 기술입니다. Hadoop 데이터의 이러한 Hadoop 데이터 원본에 저장할 수 있습니다.  
  
-   Linux 또는 Windows Server 용 Hortonworks  
  
-   Linux에서 Cloudera  
  
-   APS에서 실행 되는 HDInsight  
  
-   Azure 저장소 Blob에 저장 된 HDInsight 데이터  
  
## <a name="query-tools"></a>쿼리 도구   
  
Transact를 사용 하 여 쿼리 작성\-SQL는 쿼리의 MPP 특성에 맞게 수정 합니다. 모든 쿼리는 계산 노드에서 쿼리를 실행 하는 병렬 쿼리 계획을 생성 하는 제어 노드에로 전송 됩니다.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL  Server  Data  Tools(SSDT)  
SQL Server Data Tools Visual Studio 내에서 실행 되며 SQL Server PDW에 대 한 쿼리를 제출 하기 위한 우리의 권장 되는 GUI 도구입니다. 이 개체 탐색기를 탐색할 수 있도록 하 여 SQL Server Management Studio와 비슷합니다.  
  
Visual Studio를 아직 없는 경우 무료로 필요한 도구를 다운로드할 수 있습니다. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 명령줄 쿼리 도구  
sqlcmd는 Transact 실행 하기 위한 SQL Server 명령줄 도구\-SQL 문 및 시스템 명령입니다. SQL Server PDW 쿼리 하기 위한 권장 되는 명령줄 도구 및 SQL Server PDW와 작동 합니다. Sqlcmd Transact 실행할 수 있습니다\-대화형으로 배치 파일로 명령줄에서 또는 Windows PowerShell에서 SQL 문입니다.  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
SQL Server PDW 쿼리를 Integration Services를 사용할 수 있습니다. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>연결된 서버  
SQL Server 연결 된 서버 연결을 사용 하 여 Transact 제출 하려면 SQL Server를 사용할 수\-SQL Server PDW에 대 한 SQL 문입니다. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>비즈니스 인텔리전스 도구
  
Analysis Services  
SQL Server PDW는 Analysis Services 데이터베이스 및 Excel PowerPivot 모델에 대 한 유효한 데이터 원본. OLE DB 공급자를 사용 하 여 다차원 온라인 분석 처리 (MOLAP) 또는 관계형 온라인 분석 처리 (ROLAP) 저장소를 사용 하도록 Analysis Services 큐브를 구성할 수 있습니다.  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>보고서 작성기  
Reporting Services에 대 한 SQL Server 보고서 작성기를 사용 하 여 개발 하는 보고서에 대 한 SQL Server PDW SQL Server 데이터 원본으로 사용할 수 있습니다. 보고서 모델에 대 한 SQL Server 원본으로 SQL Server PDW를 사용할 수 있습니다. 보고서 관리자 또는 보고서 서버 API 사용 하 여 SQL Server PDW 데이터베이스에서 모델을 생성할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
Excel의 경우 크게 Excel의 데이터 분석 기능을 확장 하는 무료 다운로드 PowerPivot과 SQL Server PDW에 연결할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>도구를 로드합니다. 
  
### <a name="integration-services"></a>Integration Services  
SQL Server PDW에 데이터를 로드 SQL ServerIntegration 서비스를 사용할 수 있도록 하는 PDW 특정 대상 어댑터를 설치 합니다.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 명령줄 로더  
dwloader는 SQL Server PDW 계산 노드에 로드 서버에서 데이터를 병렬로 로드 하는 명령줄 로드 도구입니다. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 통합  
PolyBase 기술을 사용 하면 SQL Server PDW의 관계형 테이블에는 Hadoop 클러스터에서 비관계형 데이터를 로드할 수 있습니다. Hadoop 데이터는 Azure 저장소 Blob 또는 Hadoop 클러스터 AP에 HDI 영역 외부에 있을 수 있습니다.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>데이터베이스 백업 및 복원  
SQL Server PDW Transact 사용 하 여\-SQL 데이터베이스 백업 및 복원 명령을 백업 하 고 백업 서버에서 병렬로 사용자 데이터베이스를 복원 합니다. SQL Server PDW 백업 디렉터리는 Windows 파일 공유에 쓰고 후 Windows 파일 공유에서 마찬가지로 데이터를 복원 합니다.  
  
자세한 내용은 참조 [백업 및 로드 하드웨어 계획](backup-and-loading-hardware.md) 및 [백업 및 복원 개요](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>원격 테이블 복사  
원격 테이블 복사 기능을 사용 하면 원격 (비 어플라이언스) SMP SQL Server 데이터베이스에 SQL Server PDW 데이터베이스에서 테이블을 복사할 수 있습니다. 이 SQL Server PDW에 대 한 허브 및 스포크 시나리오를 지원 합니다.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>모니터링  
분석 플랫폼 시스템에 어플라이언스 활동을 모니터링 하는 여러 가지 방법으로  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔을 사용 하면 어플라이언스 상태에 대 한 현재 상태를 볼 수 있습니다. 이 컨트롤 노드에서 웹 응용 프로그램으로 실행 되며은 https를 통해 액세스할 수 있습니다.  
  
자세한 내용은 참조 [관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>시스템 뷰  
관리 콘솔은 시스템 뷰 쿼리를 기반으로 합니다. 개별적으로 특정 개수의 필요한 정보를 가져오려는 시스템 뷰를 쿼리할 수 있습니다.  

자세한 내용은 참조 [종료 하거나 다시 사용 하 여 시스템 뷰 &#40; 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW 용 관리 팩을 System Center Operations Manager (SCOM) 있습니다. 

SCOM에 대 한 어플라이언스를 구성 하려면 참조 [종료 하거나 다시 사용 하 여 System Center Operations Manager &#40; 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
