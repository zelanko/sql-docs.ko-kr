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
ms.openlocfilehash: 711d9d5bf7a3268b400eae4b1b117b4034133f5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75228067"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 하이브리드 클라우드 소개
 대부분의 애플리케이션에는 높은 효율성, 비즈니스 가치, 복잡한 하드웨어 구성, 수요의 엄청난 폭증, 업계 및 회사 규정 준수 등의 주요 문제가 있습니다. 이러한 요소를 모두 고려하고 엔터프라이즈급 기술을 구현하는 작업은 매우 어려울 수 있습니다. Microsoft 하이브리드 클라우드 전략은 이러한 주요 문제를 극복할 수 있도록 기존, 프라이빗 클라우드, 퍼블릭 클라우드 및 하이브리드 클라우드 환경에 대한 지원을 제공합니다. 
 
 비즈니스에 필요할 때 확장할 수 있는 유연한 IT 인프라가 필요한 경우 Azure 글로벌 데이터 센터에서 데이터 센터 또는 공용 클라우드에서 사설 클라우드를 구축할 수 있습니다. 퍼블릭 클라우드와 합쳐지도록 데이터 센터를 확장하면 하이브리드 클라우드 모델을 구축하게 됩니다. 
 
 이 항목에서는 하이브리드 클라우드 시나리오를 지원하는 SQL Server 2014 기능을 소개합니다. Microsoft 하이브리드 클라우드 전략 및 SQL Server에 대한 자세한 내용은 [SQL Server 하이브리드 IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 웹 사이트를 참조하십시오. 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure 및 하이브리드 클라우드 
 Microsoft 기술을 사용하여 온-프레미스와 클라우드 양쪽에서 코드를 실행하거나, 온-프레미스 데이터를 사용하여 클라우드에서 실행하거나, 두 개 이상의 데이터 센터를 이용하여 완전히 클라우드에서 실행할 수 있습니다. 따라서 기존 레거시 IT 투자를 보존하면서 원하는 속도로 애플리케이션을 클라우드로 이동할 수 있습니다. 
 
 이 문서에서는 온-프레미스 SQL Server에서 Azure 공용 클라우드 제품으로 확장 되는 하이브리드 클라우드 시나리오 ( [SQL Server azure Virtual Machines](https://msdn.microsoft.com/library/azure/jj823132.aspx) 및 [Azure Storage](https://www.azure.com/documentation/services/storage/)에 대해 집중적으로 설명 합니다. 구체적으로 다음 시나리오에 대해 설명 합니다. 
 
-  [Azure Storage에서 데이터베이스 백업 및 복원](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Azure Virtual Machines에서 데이터베이스 복제본 유지 관리](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Azure Storage에 SQL Server 데이터 파일 저장](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [기존 SQL Server 데이터베이스를 Azure Virtual Machines로 마이그레이션](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>SQL Server 및 Microsoft Azure에 대 한 하이브리드 클라우드 시나리오 
 
#### <a name="backup-and-restore-databases-tofrom-azure-storage"></a><a name="backup"></a>Azure Storage에서 데이터베이스 백업 및 복원 
 가장 기본적인 관리자 작업 중 하나는 데이터베이스 백업 및 복원입니다. SQL Server 및 Azure를 사용 하 여 클라우드에서 데이터베이스를 안전 하 게 백업할 수 있습니다. 
 
 Azure Storage를 백업 대상으로 사용 하는 SQL Server의 백업 및 복원 기능을 사용 하는 경우의 주요 이점은 다음과 같습니다. 
 
-  무제한 저비용 스토리지 
 
-  고가용성 스토리지(데이터 손실을 방지하기 위해 지리적으로 복제됨) 
 
-  재해 복구 및 규정 준수 요구 사항을 지원할 수 있는 오프사이트 스토리지 
 
-  단순화된 원격 백업 및 복원 프로세스 
 
 다음은 클라우드 및 온-프레미스 시나리오에 대한 SQL Server의 백업 및 복원 기능 목록입니다. 
 
-  [Url에 백업 SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url.md) 기능을 사용 하면 url을 백업 대상으로 지정 하 여 Azure Storage 백업할 수 있습니다. 이 기능을 사용하여 로컬 스토리지나 다른 오프사이트 옵션의 경우처럼 수동 백업을 수행하거나 자체 백업 전략을 구성할 수 있습니다. 
 
-  [백업 암호화](../relational-databases/backup-restore/backup-encryption.md) 기능을 사용 하면 저장소 대상 (온-프레미스 및 Azure Storage)에 대 한 백업을 만드는 동안 데이터를 암호화할 수 있습니다. 
 
-  [백업 압축 (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) 기능을 사용 하면 동일한 데이터의 압축 되지 않은 백업 보다 작은 백업을 만들 수 있습니다. 백업을 압축하면 필요한 디바이스 I/O가 감소하므로 일반적으로 백업 속도가 크게 향상됩니다. 이렇게 하면 Azure Storage에 백업 파일을 저장할 때 큰 혜택을 얻을 수 있습니다. 
 
-  [Azure에 대 한 관리 되는 백업](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) 기능을 사용 하 SQL Server 여 [Azure Storage](https://www.azure.com/documentation/services/storage/)에 SQL Server 데이터베이스를 자동으로 백업할 수 있습니다. 이 기능을 사용하여 백업 전략을 관리하고 단일 데이터베이스나 여러 데이터베이스에 대한 백업을 예약하도록 SQL Server를 구성하거나 인스턴스 수준에서 기본값을 설정할 수 있습니다. 
 
-  [Azure에 백업 SQL Server 도구](https://www.microsoft.com/download/details.aspx?id=40740) 를 사용 하 여 백업이 로컬 또는 클라우드에 저장 된 SQL Server 백업을 Azure Blob Storage 하 고 암호화 하 고 압축할 수 있습니다. 이 도구를 통해 SQL Server 2005, 2008, 2008 R2 및 2014와 같은 SQL Server의 여러 버전에 대한 단일 클라우드 백업 전략을 수립할 수 있습니다. 
 
#### <a name="maintain-database-replicas-on-azure-virtual-machines"></a><a name="replica"></a>Azure Virtual Machines에서 데이터베이스 복제본 유지 관리 
 데이터베이스에 대 한 안정적인 재해 복구 솔루션을 보유 하는 것은 비즈니스의 성공에 필수적입니다. 대부분의 고객은 재해 복구 사이트를 구성하고 데이터베이스 복제본을 위한 추가 하드웨어를 구입해야 합니다. SQL Server 및 Azure를 사용 하면 클라우드에서 데이터베이스의 복제본을 하나 이상 유지 관리할 수 있습니다. 
 
 Azure에서 보조 복제본을 유지 관리 하는 경우의 주요 이점은 다음과 같습니다. 
 
-  저비용 재해 복구 솔루션 
 
-  투명한 애플리케이션 장애 조치(failover) 
 
-  읽기 작업과 백업을 오프로드하기 위한 가용 복제본 
 
 다음 방법 중 하나를 사용 하 여 Azure에서 보조 복제본을 유지 관리할 수 있습니다. 
 
-  [Azure 복제본 추가 마법사](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) 를 사용 하면 재해 복구를 위해 azure의 가상 머신에 하나 이상의 데이터베이스 복제본을 배포할 수 있습니다. 
 
-  AlwaysOn 가용성 그룹, 데이터베이스 미러링 및 로그 전달은 응용 프로그램의 고가용성 및 재해 복구 요구 사항을 해결 하는 데 사용할 수 있는 가장 일반적인 기술입니다. 자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대 한 고가용성 및 재해 복구](https://msdn.microsoft.com/library/azure/jj870962.aspx)를 참조 하세요. 
 
#### <a name="store-sql-server-data-files-in-azure-storage"></a><a name="store"></a>Azure Storage에 SQL Server 데이터 파일 저장 
 온-프레미스 SQL Server 데이터 파일을 Azure Storage에 저장 하면 데이터베이스에 대해 유연 하 고 안정적 이며 무제한 오프 사이트 저장소를 제공 합니다. SQL Server 2014부터 [Miceosoft Azure의 SQL Server 데이터 파일](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) 을 사용 하 여 Azure Storage에 SQL Server 데이터베이스 파일을 저장할 수 있습니다. 이 기능을 사용 하 여 온-프레미스에서 실행 되는 SQL Server의 계산 노드를 유지 하면서 데이터와 로그 파일을 온-프레미스 데이터베이스에서 Azure Storage로 이동할 수 있습니다. 이 기능을 사용 하면 Azure Storage의 저장소 용량을 무제한으로 사용할 수 있습니다. 
 
 SQL Server 데이터 Azure Storage 파일을 저장 하는 경우의 주요 이점은 다음과 같습니다. 
 
-  Azure Storage의 무제한 저비용 저장소 
 
-  온-프레미스 보고 애플리케이션을 지원하기 위해 기록 읽기 작업을 클라우드로 오프로드하는 데 가장 적합함 
 
-  컴퓨팅 인스턴스(SQL Server 인스턴스)와 데이터(SQL Server 데이터 파일)를 분리하여 재해 복구 촉진. 이렇게 하면 재해 발생 시 온-프레미스 환경이 나 Azure 가상 컴퓨터의 다른 SQL Server 인스턴스에 데이터베이스를 쉽게 연결할 수 있습니다. 
 
#### <a name="migrate-existing-sql-server-databases-to-azure-virtual-machines"></a><a name="migrate"></a>기존 SQL Server 데이터베이스를 Azure Virtual Machines로 마이그레이션 
 클라우드 컴퓨팅은 기업에 몇 가지 주요 혜택을 제공합니다. 예를 들어 무제한의 가상화된 리소스를 종량제 기준으로 사용할 수 있으며, 자체적으로 데이터 센터를 구축하여 관리하는 대신 공용으로 사용 가능한 클라우드 데이터 센터를 활용할 수 있으므로 IT 및 하드웨어 비용을 낮출 수 있습니다. 
 
 [Azure Virtual Machines에서 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)를 사용 하면 코드를 최소한으로 변경 하거나 변경 하지 않고 기존 온-프레미스 응용 프로그램을 azure로 이동할 수 있습니다. 관리자와 개발자는 온-프레미스에서 사용 가능한 동일한 개발 및 관리 도구를 계속해서 사용할 수 있습니다. 
 
 온-프레미스 SQL Server에서 Azure 가상 머신에서 실행 되는 SQL Server로 데이터베이스를 이동 하는 작업은 일반적으로 다음 경로 중 하나를 사용 합니다. 
 
-  **데이터베이스만 이동:** Azure Virtual Machines에서 기존 온-프레미스 데이터베이스를 SQL Server로 이동 하는 데 사용할 수 있는 몇 가지 도구와 기술이 있습니다. Azure Virtual Machines에서 SQL Server로 마이그레이션하는 방법에 대 한 지침 및 권장 사항은 azure [Virtual Machines에서 SQL Server로 마이그레이션 준비를](https://msdn.microsoft.com/library/dn133142.aspx) 참조 하 고, [azure 가상 머신에서 SQL Server로 마이그레이션](https://msdn.microsoft.com/library/jj156165.aspx)을 참조 하세요. 
 
   또한 SQL Server 2014부터 새 마법사 인 [SQL Server 데이터베이스를 Microsoft Azure 가상 컴퓨터에 배포](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) 하 여 Azure 가상 컴퓨터에서 실행 되는 다른 SQL Server 인스턴스에 데이터베이스를 배포할 수 있습니다. 
 
-  **전체 가상 컴퓨터 이동:** 사용자 SQL Server 고유의 가상 컴퓨터를 Azure로 가져오거나 플랫폼 이미지를 사용 하 여 가상 컴퓨터를 만들 수 있습니다. 그런 다음 데이터가 이미 포함되어 있는 데이터 디스크를 업로드하여 가상 머신에 연결하거나 빈 디스크를 머신에 연결할 수 있습니다. 연결 된 데이터 디스크를 사용 하 여 Azure Virtual Machines에 SQL Server 데이터 인스턴스가 있으면 데이터 파일과 응용 프로그램 데이터에 대 한 또 다른 영구 저장소를 제공 합니다. 종합적인 정보 및 방법에 대 한 자세한 내용은 [Azure Virtual Machines에서 SQL Server 배포](https://msdn.microsoft.com/library/dn133141.aspx)를 참조 하세요. 
 
 응용 프로그램 계층 (예: 프레젠테이션 계층, 비즈니스 계층 및 데이터베이스 계층)을 Azure Virtual Machines로 이동 하려는 경우 [azure Virtual Machines의 SQL Server에 대 한 응용 프로그램 패턴 및 개발 전략](https://msdn.microsoft.com/library/dn574746.aspx) 문서에 제공 된 권장 사항을 검토 하는 것이 좋습니다. 이 글의 목표는 설계자 및 개발자들이 기존 애플리케이션을 Azure로 마이그레이션하고 Azure에서 새로운 애플리케이션을 개발할 때 활용할 수 있도록 좋은 애플리케이션 아키텍처 및 설계에 대한 기초 지식을 제공하는 것입니다. 이 문서에서는 각 애플리케이션 패턴에 대한 온-프레미스 시나리오, 해당 클라우드 사용 솔루션 및 관련된 기술 권장 사항을 설명합니다. 또한 애플리케이션의 올바른 개발에 도움이 되는 Azure 특정 개발 전략에 대해서도 논의합니다. 
 
## <a name="see-also"></a>참고 항목 
 [SQL Server 2014 CTP2 제품 가이드](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server 하이브리드 클라우드 블로그 시리즈](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [데이터 중심 응용 프로그램을 Azure로 마이그레이션](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
