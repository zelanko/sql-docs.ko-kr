---
title: SQL Server 2014 하이브리드 클라우드 소개 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccd4169245421dd33cb5f41bac85861679de823
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088607"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 하이브리드 클라우드 소개
 대부분의 애플리케이션에는 높은 효율성, 비즈니스 가치, 복잡한 하드웨어 구성, 수요의 엄청난 폭증, 업계 및 회사 규정 준수 등의 주요 문제가 있습니다. 이러한 요소를 모두 고려하고 엔터프라이즈급 기술을 구현하는 작업은 매우 어려울 수 있습니다. Microsoft 하이브리드 클라우드 전략은 이러한 주요 문제를 극복할 수 있도록 기존, 사설 클라우드, 공용 클라우드 및 하이브리드 클라우드 환경에 대한 지원을 제공합니다. 
 
 비즈니스 필요에 따라 확장할 수 있는 유연한 IT 인프라에 필요한 경우에 데이터 센터에서 사설 클라우드 또는 Azure 글로벌 데이터 센터에서 공용 클라우드를 빌드할 수 있습니다. 공용 클라우드와 합쳐지도록 데이터 센터를 확장하면 하이브리드 클라우드 모델을 구축하게 됩니다. 
 
 이 항목에서는 하이브리드 클라우드 시나리오를 지원하는 SQL Server 2014 기능을 소개합니다. Microsoft 하이브리드 클라우드 전략 및 SQL Server에 대한 자세한 내용은 [SQL Server 하이브리드 IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 웹 사이트를 참조하십시오. 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure 및 하이브리드 클라우드 
 Microsoft 기술을 사용하여 온-프레미스와 클라우드 양쪽에서 코드를 실행하거나, 온-프레미스 데이터를 사용하여 클라우드에서 실행하거나, 두 개 이상의 데이터 센터를 이용하여 완전히 클라우드에서 실행할 수 있습니다. 따라서 기존 레거시 IT 투자를 보존하면서 원하는 속도로 애플리케이션을 클라우드로 이동할 수 있습니다. 
 
 이 문서에서는 온-프레미스 SQL Server에서 Azure 공용 클라우드 제품인 포괄 하는 하이브리드 클라우드 시나리오 집중 합니다. [Azure Virtual Machines의 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx) 하 고 [Azure Storage](http://www.azure.com/documentation/services/storage/)합니다. 특히 다음 시나리오를 설명 하겠습니다. 
 
-  [백업 및 Azure Storage에서 데이터베이스 복원](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Azure Virtual Machines에서 데이터베이스 복제본을 유지 관리](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Azure Storage에서 SQL Server 데이터 파일을 저장 합니다.](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [기존 SQL Server 데이터베이스를 Azure Virtual Machines 마이그레이션](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>SQL Server 및 Microsoft Azure에 대 한 하이브리드 클라우드 시나리오 
 
#### <a name="backup"></a> 백업 및 Azure Storage에서 데이터베이스 복원 
 가장 기본적인 관리자 작업 중 하나는 데이터베이스 백업 및 복원입니다. SQL Server 및 Azure를 사용 하 여 클라우드에서 데이터베이스를 안전 하 게 백업할 수 있습니다. 
 
 Azure Storage를 사용 하 여 SQL Server의 백업 및 복원 기능을 사용 하 여 백업 대상으로의 주요 이점은 다음과 같습니다. 
 
-  무제한 저비용 스토리지 
 
-  고가용성 스토리지(데이터 손실을 방지하기 위해 지리적으로 복제됨) 
 
-  재해 복구 및 규정 준수 요구 사항을 지원할 수 있는 오프사이트 스토리지 
 
-  단순화된 원격 백업 및 복원 프로세스 
 
 다음은 클라우드 및 온-프레미스 시나리오에 대한 SQL Server의 백업 및 복원 기능 목록입니다. 
 
-  합니다 [SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) 기능을 사용 하면 백업 대상으로 URL을 지정 하 여 Azure Storage에 백업할 수 있습니다. 이 기능을 사용하여 로컬 스토리지나 다른 오프사이트 옵션의 경우처럼 수동 백업을 수행하거나 자체 백업 전략을 구성할 수 있습니다. 
 
-  합니다 [백업 암호화](../relational-databases/backup-restore/backup-encryption.md) 기능을 사용 하면 저장소 대상에 대 한 백업을 만드는 동안 데이터를 암호화할 수 있습니다: 온-프레미스 및 Azure Storage. 
 
-  합니다 [백업 압축 (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) 기능을 사용 하면 동일한 데이터의 압축 되지 않은 백업 보다 작은 백업을 만들 수 있습니다. 백업을 압축하면 필요한 디바이스 I/O가 감소하므로 일반적으로 백업 속도가 크게 향상됩니다. Azure Storage에 백업 파일을 저장할 때 큰 혜택을 얻을 수 있습니다이 있습니다. 
 
-  합니다 [SQL Server Managed Backup to Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) 기능에 SQL Server 데이터베이스를 자동으로 백업 수 있습니다 [Azure Storage](http://www.azure.com/documentation/services/storage/)합니다. 이 기능을 사용하여 백업 전략을 관리하고 단일 데이터베이스나 여러 데이터베이스에 대한 백업을 예약하도록 SQL Server를 구성하거나 인스턴스 수준에서 기본값을 설정할 수 있습니다. 
 
-  합니다 [SQL Server Backup to Azure Tool](https://www.microsoft.com/download/details.aspx?id=40740) Azure Blob Storage에 백업을 사용 하도록 설정 하 고 암호화 하 고 로컬 이나 클라우드에 저장 된 SQL Server 백업을 압축 합니다. 이 도구를 통해 SQL Server 2005, 2008, 2008 R2 및 2014와 같은 SQL Server의 여러 버전에 대한 단일 클라우드 백업 전략을 수립할 수 있습니다. 
 
#### <a name="replica"></a> Azure Virtual Machines에서 데이터베이스 복제본을 유지 관리 
 데이터베이스에 대 한 안정적인 재해 복구 솔루션을는 것이 비즈니스의 성공에 필수적입니다. 대부분의 고객은 재해 복구 사이트를 구성하고 데이터베이스 복제본을 위한 추가 하드웨어를 구입해야 합니다. SQL Server 및 Azure를 사용 하 여 클라우드에서 데이터베이스의 하나 이상의 복제본을 유지할 수 있습니다. 
 
 Azure에서 보조 복제본을 유지 관리의 주요 이점은 다음과 같습니다. 
 
-  저비용 재해 복구 솔루션 
 
-  투명한 애플리케이션 장애 조치(failover) 
 
-  읽기 작업과 백업을 오프로드하기 위한 가용 복제본 
 
 다음 방법 중 하나를 사용 하 여 Azure에서 보조 복제본을 유지 관리할 수 있습니다. 
 
-  합니다 [Azure 복제본 추가 마법사](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) 하나 이상의 복제본 데이터베이스의 재해 복구를 위해 Azure에서 가상 컴퓨터에 배포할 수 있습니다. 
 
-  AlwaysOn 가용성 그룹, 데이터베이스 미러링 및 로그 전달 재해 복구 요구 사항 및 응용 프로그램의 고가용성을 처리 하는 데 사용할 수 있는 가장 일반적인 기술 됩니다. 정보를 참조 하세요 [고가용성 및 재해 복구 Azure Virtual Machines에서 SQL Server에 대 한](https://msdn.microsoft.com/library/azure/jj870962.aspx)합니다. 
 
#### <a name="store"></a> Azure Storage에서 SQL Server 데이터 파일을 저장 합니다. 
 Azure Storage에 온-프레미스 SQL Server 데이터 파일을 저장할 데이터베이스에 대 한 유연 하 고 안정적인 무제한 오프 사이트 저장소를 제공 합니다. SQL Server 2014부터 사용할 수 있습니다 [Miceosoft Azure의 SQL Server 데이터 파일](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) Azure Storage에서 SQL Server 데이터베이스 파일을 저장 합니다. 이 기능을 사용 하 여 데이터를 이동할 수 있으며 로그 파일 온-프레미스 데이터베이스에서 Azure Storage로 온-프레미스를 실행 중인 SQL Server의 계산 노드를 유지 하는 동안 키를 누릅니다. 이 기능을 사용 하면 더 Azure Storage에는 무제한 저장소 용량입니다. 
 
 Azure Storage의 SQL Server 데이터 파일을 저장할 경우의 주요 이점은 다음과 같습니다. 
 
-  Azure Storage의 무제한 저비용 저장소 
 
-  온-프레미스 보고 애플리케이션을 지원하기 위해 기록 읽기 작업을 클라우드로 오프로드하는 데 가장 적합함 
 
-  컴퓨팅 인스턴스(SQL Server 인스턴스)와 데이터(SQL Server 데이터 파일)를 분리하여 재해 복구 촉진. 이렇게 하면 재해 발생 시 Azure 가상 컴퓨터 또는 온-프레미스 환경에서 SQL Server의 다른 인스턴스로 데이터베이스를 쉽게 연결할 수 있습니다. 
 
#### <a name="migrate"></a> 기존 SQL Server 데이터베이스를 Azure Virtual Machines 마이그레이션 
 클라우드 컴퓨팅은 기업에 몇 가지 주요 혜택을 제공합니다. 예를 들어 무제한의 가상화된 리소스를 종량제 기준으로 사용할 수 있으며, 자체적으로 데이터 센터를 구축하여 관리하는 대신 공용으로 사용 가능한 클라우드 데이터 센터를 활용할 수 있으므로 IT 및 하드웨어 비용을 낮출 수 있습니다. 
 
 사용 하 여 [Azure Virtual Machines에서 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx), 기존 온-프레미스 응용 프로그램 Azure에 최소를 이동할 수 있습니다 또는 코드 없이 변경 합니다. 관리자와 개발자는 온-프레미스에서 사용 가능한 동일한 개발 및 관리 도구를 계속해서 사용할 수 있습니다. 
 
 이러한 경로 중 하나를 사용 하려면 일반적으로 Azure 가상 컴퓨터에서 실행 중인 SQL Server 온-프레미스 SQL Server에서 데이터베이스를 이동: 
 
-  **데이터베이스만 이동:** 다양 한 도구와 기술을 Azure Virtual Machines에서 SQL Server에 기존 온-프레미스 데이터베이스를 이동할 수 있습니다. 지침 및 Azure Virtual Machines에서 SQL Server로 마이그레이션에 대 한 권장 사항을 참조 하세요 [Azure Virtual Machines에서 SQL Server로 마이그레이션할 준비 하기](https://msdn.microsoft.com/library/dn133142.aspx) 그리고 [Azure 가상 컴퓨터에서 SQL Server로 마이그레이션 ](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   또한 SQL Server 2014 새 마법사를 사용 하 여 시작 [Microsoft Azure Virtual Machine에 SQL Server 데이터베이스 배포](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) 데이터베이스를 Azure 가상 컴퓨터에서 실행 하는 다른 SQL Server 인스턴스를 배포할 수 있습니다. 
 
-  **전체 가상 컴퓨터 이동:** 사용자 고유의 SQL Server 가상 컴퓨터를 Azure로 가져올 수도 있고 플랫폼 이미지를 사용 하 여 만들 수 있습니다. 그런 다음 데이터가 이미 포함되어 있는 데이터 디스크를 업로드하여 가상 머신에 연결하거나 빈 디스크를 머신에 연결할 수 있습니다. 연결 된 데이터 디스크를 사용 하 여 Azure Virtual Machines에서 SQL Server 데이터 인스턴스가 있으면 데이터 파일 및 응용 프로그램 데이터에 대 한 다른 영구 저장소를 제공 합니다. 포괄적인 정보 및 방법에 대 한 참조 [Azure Virtual Machines에서 SQL Server 배포](https://msdn.microsoft.com/library/dn133141.aspx)합니다. 
 
 Azure Virtual Machines에 응용 프로그램 계층 (프레젠테이션 계층, 비즈니스 계층, 데이터베이스 계층 등)을 이동 하려는 경우에 지정 된 권장 사항을 검토 하는 것이 좋습니다는 [응용 프로그램 패턴 및 개발 Azure Virtual Machines에서 SQL Server에 대 한 전략](https://msdn.microsoft.com/library/dn574746.aspx) 문서. 이 문서의 목적은 좋은 응용 프로그램 아키텍처 및 기존 응용 프로그램을 Azure에서 새 응용 프로그램을 개발할 뿐만 아니라 Azure로 마이그레이션할 때 따를 수 있는 디자인에 대 한 솔루션 설계자와 개발자가 기반을 제공 하는 것입니다. 이 문서에서는 각 애플리케이션 패턴에 대한 온-프레미스 시나리오, 해당 클라우드 사용 솔루션 및 관련된 기술 권장 사항을 설명합니다. 또한 문서 응용 프로그램을 올바르게 디자인할 수 있도록 Azure 특정 개발 전략을 설명 합니다. 
 
## <a name="see-also"></a>참고자료 
 [SQL Server 2014 CTP2 제품 가이드](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server 하이브리드 클라우드 블로그 시리즈](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [Azure로 데이터 중심 응용 프로그램 마이그레이션](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
 
