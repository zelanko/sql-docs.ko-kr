---
title: 병렬 데이터 웨어하우스 구성 요소-Analytics Platform System | Microsoft Docs
description: 이 문서는 어플라이언스 소프트웨어 및 Analytics Platform System의 비 어플라이언스 소프트웨어 구성 요소를 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: aaf90124cc7877b633a997a2c4f170057b965028
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639890"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>병렬 데이터 웨어하우스 구성 요소-Analytics Platform System
이 문서는 어플라이언스 소프트웨어 및 Analytics Platform System의 비 어플라이언스 소프트웨어 구성 요소를 설명합니다.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![병렬 데이터 웨어하우스 소프트웨어로](media/parallel-data-warehouse-software.png "병렬 데이터 웨어하우스 소프트웨어")  
  
## <a name="sec1"></a>어플라이언스 소프트웨어-쿼리 처리 및 사용자 데이터 저장소  
  
### <a name="control-node"></a>제어 노드  
MPP 엔진  
MPP 엔진 대규모 병렬 처리 (MPP) 시스템의 중추 이며 메서드는 다음 작업을 수행합니다.  
  
-   병렬 쿼리 계획을 작성 하 고 계산 노드에서 병렬 쿼리 실행을 조정 합니다.  
  
-   저장 하 고 모든 데이터베이스에 대 한 메타 데이터 및 구성 데이터를 조정 합니다.  
  
-   SQL Server PDW database 인증 및 권한 부여를 관리합니다.  
  
-   하드웨어 및 소프트웨어 상태를 추적합니다.  
  
### <a name="data-movement-service-dms"></a>데이터 이동 서비스 (DMS)  
데이터 이동 서비스 (DMS)는 PDW의 "비밀"의 일부입니다. 메서드는 다음 작업을 수행합니다.  
  
-   SQL Server PDW 노드 간에 데이터를 전송합니다.  
  
-   프로세스 노드 간에 데이터를 전송 해야 하는 작업을 쿼리 합니다.  
  
-   데이터 전송 속도 최적화 하 여 쿼리 성능을 향상 시킵니다.  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔 어플라이언스 상태, 상태 및 성능 정보를 제공 하는 웹 응용 프로그램은  
  
### <a name="configuration-manager"></a>구성 관리자  
Configuration Manager (dwconfig.exe)는 도구 분석 플랫폼 시스템 구성를 사용 하 여 어플라이언스 관리자입니다.  
  
### <a name="control-node-databases"></a>제어 노드 데이터베이스  
SQL Server는 제어 노드가 있는 데이터베이스의 모든 관리합니다.  
  
-   셸 데이터베이스는 모든 분산된 사용자 데이터베이스에 대 한 메타 데이터를 관리 합니다.  
  
-   어플라이언스 전반에 걸친 모든 사용자의 임시 테이블에 대 한 메타 데이터를 포함 하는 TempDB입니다.  
  
-   마스터는 제어 노드에 SQL Server에 대 한 마스터 테이블입니다.  
  
### <a name="compute-node"></a>계산 노드  
Compute 노드는 병렬 데이터 처리 및 저장 단위는 합니다. 직접 연결 된 저장소를 보유 하 고 사용자 데이터를 관리 하려면 SQL Server를 사용 합니다.  
  
### <a name="data-movement-service-dms"></a>데이터 이동 서비스 (DMS)  
데이터 이동 서비스 (DMS)는 다음을 수행 하려면 각 계산 노드에서 실행 됩니다.  
  
-   DMS는 병렬 쿼리 처리의 일부로, 다른 컴퓨터 노드 및 제어 노드 간에 데이터를 전송 합니다.  
  
-   DMS를 각 계산 노드에서 실행 되는 동시에 데이터 로드를 받습니다. 계산 노드에 로드 서버에서 직접 병렬로 데이터를 로드  
  
-   DMS 각 계산 노드에서 백업 서버에 직접 데이터를 전송합니다.  
  
-   DMS는 PolyBase를 사용 하는 외부 Hadoop 클러스터 또는 Azure Storage Blob에서 데이터를 전송 합니다.  
  
### <a name="compute-node-databases"></a>계산 노드 데이터베이스 
각 계산 노드 쿼리를 처리 하 고 사용자 데이터를 관리 하도록 SQL server 인스턴스를 실행 합니다.  
  
## <a name="appliance-fabric"></a>어플라이언스 패브릭  
어플라이언스 패브릭 어플라이언스에 대 한 운영 체제, 서비스 및 네트워크 인프라를 제공합니다.  
  
### <a name="domain-controller"></a>도메인 컨트롤러  
Active Directory (AD) 도메인 서비스 (DS)  
Analytics Platform System Analytics Platform System 노드 간에 인증을 수행 하 고 SQL Server PDW Windows 인증 로그인의 인증을 관리 합니다.  
  
DNS 서비스  
Analytics Platform System 어플라이언스에 대 한 IP 주소에 도메인 이름을 확인 하는 Windows 도메인 이름 서비스 (DNS) 합니다.  
  
### <a name="windows-deployment-service"></a>Windows 배포 서비스  
Windows 배포 서비스 (WDS) 어플라이언스를 Windows Server 운영 체제를 배포합니다. 어플라이언스 전반에 걸친 모든 호스트 및 가상 컴퓨터에 배포 됩니다.  
  
DHCP 서비스가 어플라이언스 도메인 내에서 호스트 미리 구성 된 IP 주소를 사용 하지 않고도 어플라이언스 네트워크에 참가할 수 있도록 IP 주소를 만듭니다.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System 고가용성을 달성 하기 위해 가상화를 사용 합니다. Virtual Machine Manager 실제 호스트의 운영 체제를 배포 하려면 System Center를 호스팅합니다.  
  
Windows Server Update Services (WSUS)을 적용 하거나 모든 호스트 및 virtual machines에서 Windows 업데이트를 제거 합니다.  
  
### <a name="windows-server"></a>Windows Server  
호스트 및 어플라이언스의 가상 컴퓨터의 모든 Windows Server 운영 체제를 실행합니다.  
  
### <a name="failover-clustering"></a>장애 조치(Failover) 클러스터링  
Windows 장애 조치 클러스터링 호스트가 실패 하는 경우에 수동 호스트에는 프로세스를 다시 시작 하는 기능을 제공 합니다.  
  
### <a name="storage-spaces"></a>저장소 공간  
Windows 저장소 공간 계산 노드의 작은 그룹에 대 한 저장소 풀으로 사용자 데이터를 관리합니다. 계산 노드가 실패 한 경우 데이터는 그룹에 다른 계산 노드를 통해 계속 액세스할 수 있습니다.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-v Server는 간단 하 고 신뢰할 수 있는 가상화 솔루션을 제공합니다. Analytics Platform System를 CPU 리소스를 조정 하 고 패브릭 구성 요소 노드 PDW 및 어플라이언스 고가용성을 제공 하려면 virtualizations를 사용 합니다.  
  
## <a name="sec2"></a>비관계형 데이터
PolyBase 기술을 외부 Hadoop 데이터를 사용 하 여 SQL Server PDW 데이터를 통합 합니다. Hadoop 데이터의 이러한 Hadoop 데이터 원본에 저장할 수 있습니다.  
  
-   Hortonworks Hadoop 배포  
  
-   Cloudera Hadoop 배포  
  
-   Azure Storage Blob에 저장 된 HDInsight 데이터  
  
## <a name="query-tools"></a>쿼리 도구   
  
Transact를 사용 하 여 쿼리 작성\-SQL 쿼리의 MPP 특성에 맞게 수정 합니다. 모든 쿼리는 계산 노드에서 쿼리를 실행 하는 병렬 쿼리 계획을 생성 하는 제어 노드에 제출 됩니다.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL  Server  Data  Tools(SSDT)  
SQL Server Data Tools Visual Studio 내에서 실행 되며 SQL Server PDW에 대 한 쿼리를 제출 하는 것에 대 한이 권장 되는 GUI 도구입니다. 이 개체 탐색기를 탐색할 수 있도록 하 여 SQL Server Management Studio와 비슷합니다.  
  
Visual Studio를 아직 없는 경우 무료로 해야 하는 도구를 다운로드할 수 있습니다. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 명령줄 쿼리 도구  
sqlcmd는 Transact 실행에 대 한 SQL Server 명령줄 도구\-SQL 문 및 시스템 명령입니다. SQL Server PDW를 사용 하 여 작동 하 고 쿼리 하는 SQL Server PDW에 대 한 권장 되는 명령줄 도구인은 합니다. Sqlcmd를 사용 하 여 Transact를 실행할 수 있습니다\-에서 일괄 처리 파일로 명령줄에서 대화형으로 또는 Windows PowerShell에서 SQL 문입니다.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
SQL Server PDW 쿼리를 Integration Services를 사용할 수 있습니다. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>연결된 서버  
SQL Server 연결 된 서버 연결을 사용 하 여 Transact 전송할 SQL Server를 사용할 수 있습니다\-SQL Server PDW에 대 한 SQL 문입니다. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>비즈니스 인텔리전스 도구
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW는 Analysis Services 데이터베이스 및 Excel PowerPivot 모델에 대 한 올바른 데이터 소스입니다. OLE DB 공급자를 사용 하 여 다차원 온라인 분석 처리 (MOLAP) 또는 관계형 온라인 분석 처리 (ROLAP) 저장소를 사용 하는 Analysis Services 큐브를 구성할 수 있습니다.  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>보고서 작성기  
Reporting Services에 대 한 SQL Server 보고서 작성기를 사용 하 여 개발 하는 보고서에 대 한 SQL Server 데이터 원본으로 SQL Server PDW를 사용할 수 있습니다. 보고서 모델에 대 한 SQL Server 원본으로 SQL Server PDW를 사용할 수 있습니다. 보고서 관리자 또는 보고서 서버 API 사용 하 여 SQL Server PDW 데이터베이스에서 모델을 생성할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
Excel의 데이터 분석 기능을 크게 확장 되는 무료 다운로드 Excel 용 PowerPivot 사용 하 여 SQL Server PDW에 연결할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>도구를 로드합니다. 
  
### <a name="integration-services"></a>Integration Services  
SQL ServerIntegration Services SQL Server PDW 데이터를 로드 하는 데 사용할 수 있는 특정 PDW 대상 어댑터를 설치 합니다.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 명령줄 로더  
dwloader 명령줄 로드 도구 로드 서버에서 SQL Server PDW 계산 노드에 병렬로 데이터를 로드 하는 경우 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 통합  
PolyBase 기술을 사용 하 여 SQL Server PDW에서 관계형 테이블로 Hadoop 클러스터에서 비관계형 데이터를 로드할 수 있습니다. Hadoop 데이터는 Azure Storage Blob 또는 외부 Hadoop 클러스터에 있을 수 있습니다.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>데이터베이스 백업 및 복원  
SQL Server PDW Transact SQL 데이터베이스 백업을 사용 하 여 명령을 백업으로 복원 및 백업 서버에서 동시에 사용자 데이터베이스를 복원 합니다. SQL Server PDW 백업 Windows 파일 공유의 디렉터리를 쓰고 Windows 파일 공유에서 마찬가지로 데이터를 복원 합니다.  
  
자세한 내용은 [백업 및 로드 하드웨어에 대 한 계획](backup-and-loading-hardware.md) 고 [Backup 및 복원 개요](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>원격 테이블 복사  
원격 테이블 복사 기능을 사용 하면 원격 (비 어플라이언스) SMP SQL Server 데이터베이스에 SQL Server PDW 데이터베이스에서 테이블을 복사할 수 있습니다. SQL Server PDW에 대 한 허브 및 스포크 시나리오 지원 합니다.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>모니터링  
분석 플랫폼 시스템 어플라이언스 활동을 모니터링 하는 여러 가지 방법으로  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔을 사용 하면 어플라이언스 상태에 대 한 현재 상태를 볼 수 있습니다. 이 제어 노드에서 웹 응용 프로그램으로 실행 되며는 https를 통해 액세스할 수 있습니다.  
  
자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>시스템 뷰  
관리 콘솔은 시스템 뷰 쿼리를 기반으로 합니다. 개별적으로 특정 부분 필요한 정보를 가져오려는 시스템 뷰를 쿼리할 수 있습니다.  

자세한 내용은 [시스템 뷰를 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW 용 System Center Operations Manager (SCOM) 관리 팩에 있습니다. 

SCOM에 대 한 어플라이언스를 구성 하려면 [System Center Operations Manager를 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
