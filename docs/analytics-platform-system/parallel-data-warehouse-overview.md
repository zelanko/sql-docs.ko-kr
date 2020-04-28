---
title: 병렬 데이터 웨어하우스 구성 요소
description: 이 문서에서는 분석 플랫폼 시스템의 어플라이언스 소프트웨어 및 비 어플라이언스 소프트웨어 구성 요소에 대해 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400929"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>병렬 데이터 웨어하우스 구성 요소-분석 플랫폼 시스템
이 문서에서는 분석 플랫폼 시스템의 어플라이언스 소프트웨어 및 비 어플라이언스 소프트웨어 구성 요소에 대해 설명 합니다.  
  
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
  
## <a name="appliance-software---query-processing-and-user-data-storage"></a><a name="sec1"></a>어플라이언스 소프트웨어-쿼리 처리 및 사용자 데이터 저장소  
  
### <a name="control-node"></a>제어 노드  
MPP 엔진  
MPP 엔진은 MPP (대규모 Parallel Processing) 시스템의 brains입니다. 메서드는 다음 작업을 수행합니다.  
  
-   병렬 쿼리 계획을 만들고 계산 노드에서 병렬 쿼리 실행을 조정 합니다.  
  
-   모든 데이터베이스에 대 한 메타 데이터 및 구성 데이터를 저장 하 고 조정 합니다.  
  
-   SQL Server PDW 데이터베이스 인증 및 권한 부여를 관리 합니다.  
  
-   하드웨어 및 소프트웨어 상태를 추적 합니다.  
  
### <a name="data-movement-service-dms"></a>DMS (데이터 이동 서비스)  
DMS (데이터 이동 서비스)는 PDW의 "secret 기술인"에 포함 되어 있습니다. 메서드는 다음 작업을 수행합니다.  
  
-   SQL Server PDW 노드와 데이터를 전송 합니다.  
  
-   노드 간에 데이터를 전송 해야 하는 쿼리 작업을 처리 합니다.  
  
-   데이터 전송 속도를 최적화 하 여 쿼리 성능을 향상 시킵니다.  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔은 어플라이언스 상태, 상태 및 성능 정보를 표시 하는 웹 응용 프로그램입니다.  
  
### <a name="configuration-manager"></a>Configuration Manager  
Configuration Manager (dwconfig .exe)는 어플라이언스 관리자가 분석 플랫폼 시스템을 구성 하는 데 사용 하는 도구입니다.  
  
### <a name="control-node-databases"></a>제어 노드 데이터베이스  
SQL Server는 제어 노드의 모든 데이터베이스를 관리 합니다.  
  
-   셸 데이터베이스는 모든 분산 사용자 데이터베이스에 대 한 메타 데이터를 관리 합니다.  
  
-   TempDB에는 어플라이언스 전체의 모든 사용자 임시 테이블에 대 한 메타 데이터가 포함 됩니다.  
  
-   Master는 컨트롤 노드의 SQL Server에 대 한 마스터 테이블입니다.  
  
### <a name="compute-node"></a>계산 노드  
계산 노드는 병렬 데이터 처리 및 저장 단위입니다. 직접 연결 된 저장소를 사용 하 고 SQL Server를 사용 하 여 사용자 데이터를 관리 합니다.  
  
### <a name="data-movement-service-dms"></a>DMS (데이터 이동 서비스)  
DMS (데이터 이동 서비스)는 다음을 수행 하기 위해 각 계산 노드에서 실행 됩니다.  
  
-   병렬 쿼리를 처리 하는 과정에서 DMS는 다른 컴퓨터 노드와 제어 노드에 데이터를 전송 합니다.  
  
-   각 계산 노드에서 실행 되는 DMS는 동시에 데이터 로드를 수신 합니다. 데이터는 로드 서버에서 계산 노드로 직접 병렬로 로드 됩니다.  
  
-   DMS는 각 계산 노드의 데이터를 백업 서버로 직접 전송 합니다.  
  
-   PolyBase를 사용 하 여 DMS는 외부 Hadoop 클러스터 또는 Azure Storage Blob에서 데이터를 전송 합니다.  
  
### <a name="compute-node-databases"></a>계산 노드 데이터베이스 
각 계산 노드는 SQL Server의 인스턴스를 실행 하 여 쿼리를 처리 하 고 사용자 데이터를 관리 합니다.  
  
## <a name="appliance-fabric"></a>어플라이언스 패브릭  
어플라이언스 패브릭은 어플라이언스에 대 한 운영 체제, 서비스 및 네트워크 인프라를 제공 합니다.  
  
### <a name="domain-controller"></a>도메인 컨트롤러  
AD (Active Directory) 도메인 서비스 (DS)  
분석 플랫폼 시스템은 분석 플랫폼 시스템 노드 간 인증을 수행 하 고 SQL Server PDW Windows 인증 로그인의 인증을 관리 합니다.  
  
DNS 서비스  
Windows DNS (도메인 이름 서비스)는 도메인 이름을 분석 플랫폼 시스템 어플라이언스에 대 한 IP 주소로 확인 합니다.  
  
### <a name="windows-deployment-service"></a>Windows 배포 서비스  
WDS (windows 배포 서비스)는 Windows Server 운영 체제를 어플라이언스로 배포 합니다. 기기의 모든 호스트 및 가상 컴퓨터에 배포 됩니다.  
  
DHCP 서비스는 어플라이언스 도메인 내의 호스트가 미리 구성 된 IP 주소 없이 어플라이언스 네트워크에 연결할 수 있도록 IP 주소를 만듭니다.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
분석 플랫폼 시스템은 가상화를 사용 하 여 고가용성을 구현 합니다. Virtual Machine Manager은 물리적 호스트에 운영 체제를 배포 하는 System Center를 호스팅합니다.  
  
모든 호스트 및 가상 컴퓨터에서 Windows 업데이트를 적용 하거나 제거 하는 WSUS (Windows Server Update Services)  
  
### <a name="windows-server"></a>Windows Server  
기기의 모든 호스트 및 가상 컴퓨터는 Windows Server 운영 체제를 실행 합니다.  
  
### <a name="failover-clustering"></a>장애 조치(failover) 클러스터링  
Windows 장애 조치 (Failover) 클러스터링은 호스트에 오류가 발생 하는 경우 수동 호스트에서 프로세스를 다시 시작 하는 기능을 제공 합니다.  
  
### <a name="storage-spaces"></a>스토리지 공간  
Windows 저장소 공간은 작은 계산 노드 그룹의 저장소 풀로 사용자 데이터를 관리 합니다. 계산 노드가 실패 하는 경우 그룹의 다른 계산 노드를 통해 데이터에 계속 액세스할 수 있습니다.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server는 간단 하 고 신뢰할 수 있는 가상화 솔루션을 제공 합니다. 분석 플랫폼 시스템은 가상화를 사용 하 여 CPU 리소스의 균형을 조정 하 고 PDW 노드 및 어플라이언스 패브릭 구성 요소에 대 한 고가용성을 제공 합니다.  
  
## <a name="non-relational-data"></a><a name="sec2"></a>비관계형 데이터
PolyBase 기술은 SQL Server PDW 데이터를 외부 Hadoop 데이터와 통합 합니다. Hadoop 데이터는 다음 Hadoop 데이터 원본에 저장할 수 있습니다.  
  
-   Hortonworks Hadoop 배포  
  
-   Hadoop의 Cloudera 배포  
  
-   Azure Storage Blob에 저장 된 HDInsight 데이터  
  
## <a name="query-tools"></a>쿼리 도구   
  
쿼리는 쿼리의 MPP 특성\-에 맞게 수정 된 transact-sql로 작성 됩니다. 모든 쿼리는 계산 노드에서 쿼리를 실행 하는 병렬 쿼리 계획을 생성 하는 제어 노드로 전송 됩니다.  
  
### <a name="sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)  
SQL Server Data Tools는 Visual Studio 내에서 실행 되며 SQL Server PDW에 쿼리를 전송 하기 위한 권장 GUI 도구입니다. 개체 탐색기를 탐색 하도록 허용 하 여 SQL Server Management Studio와 비슷합니다.  
  
Visual Studio가 아직 없는 경우 무료로 필요한 도구를 다운로드할 수 있습니다. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 명령줄 쿼리 도구  
sqlcmd는 Transact-sql\-명령과 시스템 명령을 실행 하기 위한 SQL Server 명령줄 도구입니다. SQL Server PDW와 함께 작동 하며 SQL Server PDW을 쿼리 하는 데 권장 되는 명령줄 도구입니다. Sqlcmd를 사용 하면 명령줄,\-배치 파일 또는 Windows PowerShell에서 대화형으로 transact-sql 문을 실행할 수 있습니다.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Integration Services를 사용 하 여 SQL Server PDW를 쿼리할 수 있습니다. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>연결된 서버  
SQL Server 연결 된 서버 연결을 사용 하 여 SQL Server를 사용 하 여 SQL Server PDW\-에 transact-sql 문을 전송할 수 있습니다. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>비즈니스 인텔리전스 도구
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW은 Analysis Services 데이터베이스 및 Excel PowerPivot 모델의 유효한 데이터 원본입니다. OLE DB 공급자를 사용 하 여 다차원 MOLAP (온라인 분석 처리) 또는 ROLAP (관계형 온라인 분석 처리) 저장소를 사용 하도록 Analysis Services 큐브를 구성할 수 있습니다.  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>보고서 작성기  
SQL Server 보고서 작성기를 사용 하 여 Reporting Services 용으로 개발 하는 보고서의 SQL Server 데이터 원본으로 SQL Server PDW를 사용할 수 있습니다. SQL Server PDW를 보고서 모델의 SQL Server 원본으로 사용할 수도 있습니다. 보고서 관리자 또는 보고서 서버 API를 사용 하 여 SQL Server PDW 데이터베이스에서 모델을 생성할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
Excel의 데이터 분석 기능을 크게 확장 하는 무료 다운로드 인 PowerPivot for Excel을 사용 하 여 SQL Server PDW에 연결할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>로드 도구 
  
### <a name="integration-services"></a>Integration Services  
SQL ServerIntegration Services를 사용 하 여 데이터를 SQL Server PDW 로드 하는 데 사용할 수 있는 PDW 관련 대상 어댑터를 설치 합니다.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 명령줄 로더  
dwloader는 로드 하는 서버에서 SQL Server PDW 계산 노드로 데이터를 병렬로 로드 하는 명령줄 로드 도구입니다. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>Hadoop 통합을 위한 PolyBase  
PolyBase 기술을 사용 하 여 Hadoop 클러스터에서 비관계형 데이터를 SQL Server PDW의 관계형 테이블로 로드할 수 있습니다. Hadoop 데이터는 외부 Hadoop 클러스터 또는 Azure Storage Blob에서 찾을 수 있습니다.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>데이터베이스 백업 및 복원  
SQL Server PDW는 Transact-sql 데이터베이스 백업 및 복원 명령을 사용 하 여 백업 서버에 대 한 사용자 데이터베이스를 병렬로 백업 하 고 복원 합니다. SQL Server PDW은 Windows 파일 공유의 디렉터리에 백업을 쓴 다음 마찬가지로 Windows 파일 공유에서 데이터를 복원 합니다.  
  
자세한 내용은 [백업 및 하드웨어 로드 계획](backup-and-loading-hardware.md) 및 [백업 및 복원 개요](backup-and-restore-overview.md) 를 참조 하세요.  
  
## <a name="remote-table-copy"></a>원격 테이블 복사  
원격 테이블 복사 기능을 사용 하면 SQL Server PDW 데이터베이스에서 원격 (비 어플라이언스) SMP SQL Server 데이터베이스로 테이블을 복사할 수 있습니다. 이렇게 하면 SQL Server PDW에 대 한 허브 및 스포크 시나리오를 사용할 수 있습니다.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>모니터링  
분석 플랫폼 시스템에는 어플라이언스 활동을 모니터링 하는 여러 가지 방법이 있습니다.  
  
### <a name="admin-console"></a>관리 사용자  
관리 콘솔에서 어플라이언스 상태에 대 한 현재 상태를 볼 수 있습니다. 이는 컨트롤 노드에서 웹 응용 프로그램으로 실행 되며 https를 통해 액세스할 수 있습니다.  
  
자세한 내용은 [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요&#41;  

### <a name="system-views"></a>시스템 뷰  
관리 콘솔은 시스템 뷰 쿼리를 기반으로 합니다. 시스템 뷰를 개별적으로 쿼리하여 필요한 특정 정보를 얻을 수 있습니다.  

자세한 내용은 [시스템 뷰를 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템](monitor-the-appliance-by-using-system-views.md) 을 참조 하세요&#41; 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW에 대 한 System Center Operations Manager (SCOM) 관리 팩이 있습니다. 

SCOM에 대 한 어플라이언스를 구성 하려면 [System Center Operations Manager &#40;Analytics Platform System을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-system-center-operations-manager.md) 을 참조 하세요&#41;  
  
