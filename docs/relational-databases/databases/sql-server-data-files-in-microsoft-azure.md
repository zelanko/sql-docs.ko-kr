---
title: "Microsoft Azure의 SQL Server 데이터 파일 | Microsoft 문서"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f04f47c6230a65140c405db039ce737ad3aa7762
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-data-files-in-microsoft-azure"></a>Microsoft Azure의 SQL Server 데이터 파일
  ![Azure의 데이터 파일](../../relational-databases/databases/media/data-files-on-azure.png "Data files on Azure")  
  
 Microsoft Azure에서 SQL Server 데이터 파일을 통해 Microsoft Azure Blob으로 저장된 SQL Server 데이터베이스 파일이 기본적으로 지원됩니다. 이 기능을 사용하면 온-프레미스로 실행 중인 SQL Server에서 또는 Microsoft Azure BLOB 저장소에서 사용자의 데이터에 대한 전용 저장소 위치를 갖는 Microsoft Azure의 가상 컴퓨터에서 데이터베이스를 만들 수 있습니다. 특히, 이 향상된 기능은 분리 및 연결 작업을 사용하여 컴퓨터 간의 데이터 이동을 간소화합니다. 또한 Microsoft Azure Storage를 원본 또는 대상으로 복원하도록 허용하여 데이터베이스 백업 파일에 대한 대체 저장소 위치를 제공합니다. 따라서 데이터 가상화, 데이터 이동, 보안 및 가용성, 고가용성 및 탄력적인 크기 조정을 위한 쉽고 저렴한 비용 및 유지 관리 등 여러 가지 이점을 제공하여 다양한 하이브리드 솔루션을 사용할 수 있도록 지원합니다.
 
> [AZURE.IMPORTANT]시스템 데이터베이스를 Azure Blob Storage에 저장하는 것은 좋지 않으며 지원되지 않습니다. 
  
 이 항목에서는 SQL Server 데이터 파일을 Microsoft Azure Storage 서비스에 저장하는 데 중요한 개념 및 고려 사항에 대해 설명합니다.  
  
 이 새 기능을 사용하는 방법을 실제로 실습하려면 [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 저장소 서비스 사용 ](https://msdn.microsoft.com/library/dn466438.aspx)을 참조하세요.  
  
## <a name="why-use-sql-server-data-files-in-microsoft-azure"></a>Microsoft Azure의 SQL Server 데이터 파일을 사용하는 이유는 무엇인가요? 
  
-   **쉽고 빠른 마이그레이션 이점:** 이 기능은 응용 프로그램 변경 없이 온-프레미스 내 컴퓨터 간에 또는 온-프레미스와 클라우드 환경 간에 데이터베이스를 한 번에 하나씩 이동하여 마이그레이션 프로세스를 간소화합니다. 따라서 기존 온-프레미스 인프라를 현재 위치에 유지하면서 증분 마이그레이션을 지원합니다. 또한 온-프레미스 환경의 여러 위치에서 응용 프로그램을 실행해야 할 경우 중앙 집중식 데이터 저장소에 액세스하여 응용 프로그램 논리를 간소화합니다. 경우에 따라 지리적으로 분산된 위치에 컴퓨터 센터를 신속하게 설치하여 여러 소스에서 데이터를 수집해야 할 수도 있습니다. 데이터를 다른 위치로 이동하는 대신 이 새로운 향상된 기능을 사용하여 많은 데이터베이스를 Microsoft Azure BLOB으로 저장한 다음 Transact-SQL 스크립트를 실행하여 로컬 컴퓨터 또는 가상 컴퓨터에 데이터베이스를 만들 수 있습니다.  
  
-   **비용 및 무제한 저장소 이점:** 이 기능을 사용하면 온-프레미스 컴퓨터 리소스를 활용하면서 Microsoft Azure에서 무제한 오프사이트 저장소를 사용할 수 있습니다. Microsoft Azure를 저장소 위치로 사용하면 하드웨어 관리 오버헤드 없이 응용 프로그램 논리에만 쉽게 집중할 수 있습니다. 온-프레미스에서 계산 노드가 손실되더라도 데이터를 이동하지 않고 새 계산 노드를 설정할 수 있습니다.  
  
-   **고가용성 및 재해 복구 이점:** Microsoft Azure의 SQL Server 데이터 파일 기능을 사용하면 고가용성 및 재해 복구 솔루션을 간소화할 수 있습니다. 예를 들어 Microsoft Azure의 가상 컴퓨터 또는 SQL Server 인스턴스가 충돌할 경우 Microsoft Azure BLOB에 대한 링크를 다시 설정하여 새 SQL Server 인스턴스에 데이터베이스를 다시 만들 수 있습니다.  
  
-   **보안 이점:** 이 새로운 향상된 기능을 사용하여 계산 인스턴스를 저장소 인스턴스와 구분할 수 있습니다. 저장소 인스턴스가 아닌 계산 인스턴스에서만 암호 해독이 포함된 완전히 암호화된 데이터베이스를 설정할 수 있습니다. 즉, 이 새로운 향상된 기능을 사용하면 데이터와 물리적으로 구분되는 TDE(투명한 데이터 암호화) 인증서로 공용 클라우드의 모든 데이터를 암호화할 수 있습니다. TDE 키를 master 데이터베이스에 저장한 다음 이 master 데이터베이스를 물리적으로 안전한 온-프레미스 컴퓨터에 로컬로 저장하고 로컬로 백업할 수 있습니다. 이러한 로컬 키를 사용하여 Microsoft Azure Storage에 있는 데이터를 암호화할 수 있습니다. 클라우드 스토리지 계정 자격 증명을 도난 당한 경우에도 TDE 인증서가 항상 온-프레미스에 있으므로 데이터는 여전히 안전합니다.  
  
-   **스냅숏 백업:**  이 기능은 Azure 스냅숏을 사용하여 Azure Blob 저장소 서비스를 통해 저장된 데이터베이스 파일에 대한 거의 즉시 백업 및 보다 신속한 복원을 제공합니다. 이 기능을 사용하면 백업 및 복원 정책을 간소화할 수 있습니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
## <a name="concepts-and-requirements"></a>개념 및 요구 사항  
  
### <a name="azure-storage-concepts"></a>Azure Storage 개념  
 Windows Azure의 SQL Server 데이터 파일 기능을 사용할 경우 Windows Azure에서 저장소 계정과 컨테이너를 만들어야 합니다. 그런 다음 컨테이너에 액세스하는 데 필요한 공유 액세스 서명과 컨테이너 정책에 대한 정보가 들어 있는 SQL Server 자격 증명을 만들어야 합니다.  
  
 [Microsoft Azure](https://azure.microsoft.com)에서 [Azure Storage](https://azure.microsoft.com/services/storage/) 계정은 BLOB에 액세스하는 데 필요한 가장 높은 수준의 네임스페이스를 나타냅니다. 저장소 계정에 포함될 수 있는 컨테이너의 개수 제한은 없지만 총 크기가 500TB 미만이어야 합니다. 저장소 제한에 대한 최신 정보는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](http://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/)(영문)을 참조하세요. 컨테이너는 [BLOB](https://azure.microsoft.com/documentation/articles/storage-introduction/#blob-storage)집합을 그룹화합니다. 모든 BLOB은 컨테이너에 있어야 합니다. 계정에 포함될 수 있는 컨테이너의 개수 제한은 없습니다. 마찬가지로 컨테이너에 저장될 수 있는 BLOB의 개수도 제한되지 않습니다. Azure Blob Storage 서비스에는 블록 Blob과 페이지 Blob이라는 두 가지 유형의 Blob을 저장할 수 있습니다. 이 새로운 기능은 최대 1TB 이하의 페이지 BLOB을 사용하며, 파일의 바이트 범위가 자주 수정될 때 더 효율적입니다. `http://storageaccount.blob.core.windows.net/<container>/<blob>`URL 형식을 사용하여 BLOB에 액세스할 수 있습니다.  
  
### <a name="azure-billing-considerations"></a>Azure 청구 고려 사항  
 의사 결정 및 계획 과정에서 Azure 서비스 사용 비용에 대한 예측은 중요한 사항입니다. Azure Storage에 SQL Server 데이터 파일을 저장할 경우 저장소 및 트랜잭션과 관련된 비용을 지불해야 합니다. 또한 Azure Storage의 SQL Server 데이터 파일 기능을 구현하려면 45-60초마다 BLOB 임대를 암시적으로 갱신해야 합니다. 또한 데이터베이스 파일(예: .mdf 또는 .ldf)당 트랜잭션 비용이 발생합니다. 현재 가격 모델에 따라 두 데이터베이스 파일(.mdf 및 .ldf)의 임대를 갱신하는 비용은 1개월에 약 2센트로 예상됩니다. Azure Storage 및 Azure 가상 컴퓨터의 사용과 관련한 월별 비용을 예측하려면 [Azure 가격](http://azure.microsoft.com/pricing/) 페이지의 정보를 참조하세요.  
  
### <a name="sql-server-concepts"></a>SQL 서버 개념  
 이 새로운 향상된 기능을 사용할 경우 다음을 수행해야 합니다.  
  
-   컨테이너에 대한 정책을 만들고 SAS(공유 액세스 서명) 키를 생성해야 합니다.  
  
-   데이터 또는 로그 파일에서 사용하는 각 컨테이너에 대해 컨테이너 경로와 일치하는 이름의 SQL Server 자격 증명을 만들어야 합니다.  
  
-   Azure Storage 컨테이너, 연결된 정책 이름 및 SAS 키를 SQL Server 자격 증명 저장소에 저장해야 합니다.  
  
 다음 예에서는 Azure Storage 컨테이너를 만들고 읽기, 쓰기 및 나열 권한이 있는 정책을 만들었다고 가정합니다. 컨테이너에 대한 정책을 만들면 메모리에 암호화되지 않은 상태로 유지해도 안전하고 SQL Server에서 컨테이너의 BLOB 파일에 액세스하는 데 필요한 SAS 키가 생성됩니다. 다음 코드 조각에서 `'your SAS key'` 를 `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`와 유사한 항목으로 바꾸십시오. 자세한 내용은 [Azure Storage 리소스에 대한 액세스 관리](http://azure.microsoft.com/en-us/documentation/articles/storage-manage-access-to-resources/)를 참조하십시오.  
  
```  
  
-- Create a credential  
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = 'your SAS key'  
  
-- Create database with data and log files in Windows Azure container.  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
  
```  
  
 **중요 정보:** 컨테이너의 데이터 파일에 대한 활성 참조가 있는 경우 해당 SQL Server 자격 증명을 삭제하려고 하면 실패합니다.  
  
### <a name="security"></a>보안  
 Azure Storage에 SQL Server 데이터 파일을 저장할 경우의 보안 고려 사항 및 요구 사항은 다음과 같습니다.  
  
-   Azure Blob Storage 서비스의 컨테이너를 만들 때 액세스 권한을 개인으로 설정하는 것이 좋습니다. 액세스 형식을 개인으로 설정하면 Azure 계정 소유자만 컨테이너 및 BLOB 데이터를 읽을 수 있습니다.  
  
-   Azure Storage에 SQL Server 데이터베이스 파일을 저장할 경우 컨테이너, BLOB, 큐 및 테이블에 대한 제한된 액세스 권한을 부여하는 URI인 공유 액세스 서명을 사용해야 합니다. 공유 액세스 서명을 사용하면 Azure Storage 계정 키를 공유하지 않고 SQL Server에서 저장소 계정의 리소스에 액세스할 수 있습니다.  
  
-   또한 데이터베이스에 대한 기존 온-프레미스 보안 방법을 계속 구현하는 것이 좋습니다.  
  
### <a name="installation-prerequisites"></a>필수 구성 요소 설치  
 Azure에 SQL Server 데이터 파일을 저장할 경우 설치를 위한 필수 조건은 다음과 같습니다.  
  
-   **SQL Server 온-프레미스:** SQL Server 2016 버전에 이 기능이 포함됩니다. SQL Server 2016을 다운로드하는 방법을 알아보려면 [SQL Server 2016](https://www.microsoft.com/en-us/cloud-platform/sql-server)을 참조하세요.  
  
-   Azure 가상 컴퓨터에서 실행 중인 SQL Server: [Azure 가상 컴퓨터에 SQL Server](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)를 설치하는 경우 SQL Server 2016을 설치하거나 기존 인스턴스를 업데이트하세요. 이와 마찬가지로 SQL Server 2016 플랫폼 이미지를 사용하여 Azure에서 새 가상 컴퓨터를 만들 수도 있습니다.

  
###  <a name="bkmk_Limitations"></a> 제한 사항  
  
-   이 기능의 현재 릴리스에서는 Azure Storage에 **FileStream** 데이터를 저장할 수 없습니다. Azure Storage 통합 로컬 데이터베이스에 **Filestream** 데이터를 저장할 수 있지만 Azure Storage를 사용하여 컴퓨터 간에 Filestream 데이터를 이동할 수는 없습니다. **FileStream** 데이터의 경우 컴퓨터 간에 Filestream과 연관된 파일(.mdf, .ldf)을 이동하는 데 기존 기술을 계속 사용하는 것이 좋습니다.  
  
-   현재 이 새로운 향상된 기능을 사용하여 여러 SQL Server 인스턴스에서 Azure Storage의 동일한 데이터베이스 파일에 동시에 액세스할 수 없습니다. 활성 데이터베이스 파일이 있는 서버 A가 온라인 상태인 동안 동일한 데이터 파일을 가리키는 데이터베이스를 포함하는 서버 B를 실수로 시작한 경우, 두 번째 서버에서는 데이터베이스가 시작되지 않고 오류 **코드 5120 물리적 파일 "%.\*ls"를 열 수 없습니다. 운영 체제 오류 %d: "%ls"**.  
  
-   .mdf, .ldf 및 .ndf 파일만 Azure의 SQL Server 데이터 파일 기능을 사용하여 Azure Storage에 저장할 수 있습니다.  
  
-   Azure의 SQL Server 데이터 파일 기능을 사용할 경우 저장소 계정에 대한 지리적 복제는 지원되지 않습니다. 저장소 계정이 지리적으로 복제되는 동안 지리적 장애 조치(failover)가 발생할 경우 데이터베이스가 손상될 수 있습니다.  
  
-   각 BLOB의 최대 크기는 1TB입니다. 이로 인해 Azure Storage에 저장할 수 있는 개별 데이터베이스 데이터 및 로그 파일의 상한이 설정됩니다.  
  
-   Azure Storage의 SQL Server 데이터 파일 기능을 사용하여 Azure BLOB에 메모리 내 OLTP 데이터를 저장할 수 없습니다. 메모리 내 OLTP는 **FileStream** 에 종속되지만 이 기능의 현재 릴리스에서는 Azure Storage에 **FileStream** 데이터를 저장할 수 없기 때문입니다.  
  
-   Azure의 SQL Server 데이터 파일 기능을 사용할 경우 SQL Server에서는 **master** 데이터베이스에 설정된 데이터 정렬을 사용하여 모든 URL 또는 파일 경로를 비교합니다.  
  
-   **Always On 가용성 그룹** 은 주 데이터베이스에 새 데이터베이스 파일을 추가하지 않는 한 지원됩니다. 데이터베이스 작업 중에 주 데이터베이스에서 새 파일을 만들어야 하는 경우 먼저 보조 노드에서 Always On 가용성 그룹을 사용하지 않도록 설정합니다. 그런 다음 기본 데이터베이스에서 데이터베이스 작업을 수행하고 기본 노드에 데이터베이스를 백업합니다. 그런 다음 데이터베이스를 보조 노드에 복원하고 보조 노드에서 Always On 가용성 그룹을 사용하도록 설정합니다. Azure의 SQL Server 데이터 파일 기능을 사용할 경우 Always On 장애 조치(failover) 클러스터 인스턴스는 지원되지 않습니다.  
  
-   정상적인 작업 중에 SQL Server는 임시 임대를 사용하여 저장소에 대한 BLOB을 예약하고 45-60초마다 각 BLOB 임대를 갱신합니다. 서버가 충돌하는 상태에서 동일한 BLOB을 사용하도록 구성된 SQL Server의 다른 인스턴스가 시작될 경우 새 인스턴스는 BLOB의 기존 임대가 만료될 때까지 최대 60초 동안 기다립니다. 데이터베이스를 다른 인스턴스에 첨부하고 60초 내에 임대가 만료되도록 기다릴 수 없는 경우 BLOB에서 임대를 명시적으로 해제하여 첨부 작업의 오류를 방지할 수 있습니다.  
  
## <a name="tools-and-programming-reference-support"></a>도구 및 프로그래밍 참조 지원  
 이 섹션에서는 Azure Storage에 SQL Server 데이터 파일을 저장할 때 사용할 수 있는 도구 및 프로그래밍 참조 라이브러리에 대해 설명합니다.  
  
### <a name="powershell-support"></a>PowerShell 지원  
 PowerShell cmdlet을 통해 파일 경로 대신 Blob Storage URL을 참조하여 Azure Blob Storage 서비스에 SQL Server 데이터 파일을 저장합니다. 다음 URL 형식을 사용하여 BLOB에 액세스합니다.`: http://storageaccount.blob.core.windows.net/<container>/<blob>`  
  
### <a name="sql-server-object-and-performance-counters-support"></a>SQL Server 개체 및 성능 카운터 지원  
 SQL Server 2014 이상에서는 Azure Storage의 SQL Server 데이터 파일 기능에 사용할 새로운 SQL Server 개체를 추가했습니다. 이 새 SQL Server 개체를 [SQL Server, HTTP_STORAGE_OBJECT](../../relational-databases/performance-monitor/sql-server-http-storage-object.md) 라고 하며, SQL Server를 Microsoft Azure Storage와 함께 실행할 때 시스템 모니터에서 활동을 모니터링하는 데 사용할 수 있습니다.  
  
### <a name="sql-server-management-studio-support"></a>SQL Server Management Studio 지원  
 SQL Server Management Studio에서 다양한 대화 상자 창을 통해 이 기능을 사용할 수 있습니다. 예를 들어 https://teststorageaccnt.blob.core.windows.net/testcontainer/와 같이 저장소 컨테이너의 URL 경로를 입력할 수 있습니다.
 
 여러 대화 상자 창(예: **새 데이터베이스**, **데이터베이스 연결** 및 **데이터베이스 복원**)에 **경로**로 입력할 수 있습니다. 자세한 내용은 [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob Storage 서비스 사용](https://msdn.microsoft.com/library/dn466438.aspx)을 참조하세요.  
  
### <a name="sql-server-management-objects-support"></a>SQL Server 관리 개체 지원  
 Azure의 SQL Server 데이터 파일 기능을 사용할 경우 모든 SMO(SQL Server 관리 개체)가 지원됩니다. SMO 개체에 파일 경로가 필요한 경우 로컬 파일 경로 대신 BLOB URL 형식을 사용합니다(예: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`). SMO(SQL Server 관리 개체)에 대한 자세한 내용은 SQL Server 온라인 설명서의 [SMO&#40;SQL Server 관리 개체&#41; 프로그래밍 가이드](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)를 참조하세요.  
  
### <a name="transact-sql-support"></a>Transact-SQL 지원  
 이 새로운 기능에서는 Transact-SQL 노출 영역을 다음과 같이 변경했습니다.  
  
-   **sys.master_files** 시스템 뷰의 새로운 **int**열 **credential_id** . **credential_id** 열은 Azure Storage 사용 데이터 파일이 생성된 자격 증명에 대한 sys.credentials를 다시 상호 참조하도록 설정하는 데 사용됩니다. 이 열을 문제 해결에 사용할 수 있습니다. 예를 들어 이 열을 사용하는 데이터베이스 파일이 있는 경우 자격 증명을 삭제할 수 없습니다.  
  
##  <a name="bkmk_Troubleshooting"></a> Microsoft Azure의 SQL Server 데이터 파일 문제 해결  
 지원되지 않는 기능 또는 제한 때문에 발생하는 오류를 방지하려면 먼저 [Limitations](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations)을 검토하세요.  
  
 Azure Storage의 SQL Server 데이터 파일 기능을 사용할 때 발생할 수 있는 오류 목록은 다음과 같습니다.  
  
 **인증 오류**  
  
-   *활성 데이터베이스 파일이 사용하고 있으므로 자격 증명 '%.\*ls'을(를) 삭제할 수 없습니다.*   
    해결 방법: Azure Storage에서 활성 데이터베이스 파일이 사용 중인 자격 증명을 삭제하려고 하면 이 오류가 나타날 수 있습니다. 자격 증명을 삭제하려면 이 데이터베이스 파일을 포함하는 연결된 BLOB을 먼저 삭제해야 합니다. 활성 임대가 있는 BLOB을 삭제하려면 먼저 임대를 해제해야 합니다.  
  
-   *공유 액세스 서명이 컨테이너에서 올바르게 만들어지지 않습니다.*   
     해결 방법: 컨테이너에서 공유 액세스 서명을 올바르게 만들었는지 확인하세요. [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 저장소 서비스 사용 ](https://msdn.microsoft.com/library/dn466435.aspx)에서 2단원에 제공된 지침을 검토하세요.  
  
-   *SQL Server 자격 증명이 올바르게 만들어지지 않았습니다.*   
    해결 방법: **Identity** 필드에서 '공유 액세스 서명'을 사용하고 암호를 올바르게 만들었는지 확인합니다. [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob Storage 서비스 사용](https://msdn.microsoft.com/library/dn466436.aspx)에서 3단원에 제공된 지침을 검토하세요.  
  
 **임대 BLOB 오류:**  
  
-   동일한 BLOB 파일을 사용하는 다른 인스턴스가 충돌한 후 SQL Server를 시작하려고 하면 오류가 발생합니다. 해결 방법: 정상적인 작업 중에 SQL Server는 임시 임대를 사용하여 저장소에 대한 BLOB을 예약하고 45-60초마다 각 BLOB 임대를 갱신합니다. 서버가 충돌하는 상태에서 동일한 BLOB을 사용하도록 구성된 SQL Server의 다른 인스턴스가 시작될 경우 새 인스턴스는 BLOB의 기존 임대가 만료될 때까지 최대 60초 동안 기다립니다. 데이터베이스를 다른 인스턴스에 첨부하고 60초 내에 임대가 만료되도록 기다릴 수 없는 경우 BLOB에서 임대를 명시적으로 해제하여 첨부 작업의 오류를 방지할 수 있습니다.  
  
 **데이터베이스 오류**  
  
1.  *데이터베이스를 만들 때 발생하는 오류*   
    해결 방법: [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob Storage 서비스 사용](https://msdn.microsoft.com/library/dn466431.aspx)에서 4단원에 제공된 지침을 검토하세요.  
  
2.  *Alter 문을 실행할 때 발생하는 오류*   
    해결 방법: 데이터베이스가 온라인 상태일 때 Alter Database 문을 실행해야 합니다. 데이터 파일을 Azure Storage에 복사할 경우 항상 블록 BLOB이 아닌 페이지 BLOB을 만듭니다. 그렇지 않으면 ALTER Database 문이 실패합니다. [자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob Storage 서비스 사용](https://msdn.microsoft.com/library/dn466438.aspx)에서 7단원에 제공된 지침을 검토하세요.  
  
3.  *오류 코드 5120 물리적 파일 "%.\*ls"을(를) 열 수 없습니다. 운영 체제 오류 %d: "%ls"*   
    해결 방법: 현재 이 새로운 향상된 기능을 사용하여 여러 SQL Server 인스턴스에서 Azure Storage의 동일한 데이터베이스 파일에 동시에 액세스할 수 없습니다. 활성 데이터베이스 파일이 있는 서버 A가 온라인 상태인 동안 동일한 데이터 파일을 가리키는 데이터베이스를 포함하는 서버 B를 실수로 시작한 경우, 두 번째 서버에서는 데이터베이스가 시작되지 않고 오류 *코드 5120 물리적 파일 "%.\*ls"를 열 수 없습니다. 운영 체제 오류 %d: "%ls"*.  
  
     이 문제를 해결하려면 먼저 Azure Storage의 데이터베이스 파일에 액세스하려면 서버 A가 필요한지 여부를 확인해야 합니다. 서버 A가 필요하지 않은 경우 서버 A와 Azure Storage에 있는 데이터베이스 파일 사이의 연결을 제거하면 됩니다. 이렇게 하려면 다음 단계를 수행합니다.  
  
    1.  ALTER Database 문을 사용하여 서버 A의 파일 경로를 로컬 폴더로 설정합니다.  
  
    2.  서버 A에서 데이터베이스를 오프라인으로 설정합니다.  
  
    3.  그런 다음 데이터베이스 파일을 Azure Storage에서 서버 A의 로컬 폴더로 복사합니다. 그러면 서버 A에 데이터베이스의 로컬 복사본이 여전히 있습니다.  
  
    4.  데이터베이스를 온라인으로 설정합니다.  

  
  

