---
title: "Stretch Database | Microsoft 문서"
ms.custom: 
ms.date: 06/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 30361d4466b7495945a7dae857bbcd52fd86103a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database는 콜드 데이터를 Microsoft Azure 클라우드에 투명하고 안전하게 마이그레이션합니다.  
  
 Stretch Database를 지금 시작하려면 [Stretch에 데이터베이스 사용 마법사를 실행하여 시작](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)을 참조하세요.  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Stretch Database의 이점  
 Stretch Database는 다음과 같은 이점을 제공합니다.  
  
 **콜드 데이터에 대한 비용 효율적인 가용성 제공**  
 SQL Server 스트레치 데이터베이스를 사용하여 웜 및 콜드 트랜잭션 데이터를 SQL Server에서 Microsoft Azure로 동적으로 확장할 수 있습니다. 일반적인 콜드 데이터 저장소와 달리 데이터가 항상 온라인 상태로 유지되며 쿼리할 수 있습니다. 고객 주문 기록과 같은 큰 테이블에 대한 부담 없이 보다 긴 데이터 보존 일정을 제공할 수 있습니다. 비용이 많이 드는 온-프레미스 저장소를 확장하는 대신 저렴한 Azure를 이용할 수 있습니다. Azure 포털에서 가격 책정 계층을 선택하고 설정을 구성하여 가격 및 비용을 관리할 수 있습니다. 필요에 따라 확장하거나 축소할 수 있습니다. 자세한 내용은 [SQL Server Stretch Database 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) 를 참조하세요.  
  
 **쿼리 또는 응용 프로그램을 변경할 필요가 없음**  
 온-프레미스에 있든 클라우드로 확장되든 상관없이 SQL Server 데이터에 원활하게 액세스할 수 있습니다.  데이터 저장 위치를 결정하는 정책을 설정하면 SQL Server가 백그라운드에서 데이터 이동을 처리합니다. 전체 테이블은 항상 온라인 상태이며 쿼리할 수 있습니다. 또한 Stretch Database는 기존 쿼리 또는 응용 프로그램을 변경할 필요가 없습니다. 데이터의 위치가 응용 프로그램에 완전히 투명합니다.  
  
 **온-프레미스 데이터 유지 관리 간소화**  
 데이터에 대한 온-프레미스 유지 관리 및 저장소를 줄일 수 있습니다. 온-프레미스 데이터 백업은 보다 빠르게 실행되며 유지 관리 기간 내에 완료됩니다. 데이터의 클라우드 부분에 대한 백업이 자동으로 실행됩니다. 온-프레미스 저장소 요구 사항이 크게 감소합니다. Azure Storage는 온-프레미스 SSD에 추가하는 것보다 80% 더 저렴할 수 있습니다.  
  
 **마이그레이션 중 데이터 보안 유지**  
 가장 중요한 응용 프로그램을 클라우드로 안전하게 확장할 수 있습니다. SQL Server의 상시 암호화는 이동 중인 데이터에 대한 암호화를 제공합니다. RLS(행 수준 보안) 및 기타 고급 SQL Server 보안 기능도 스트레치 데이터베이스와 함께 작동하여 데이터를 보호합니다.  
  
## <a name="what-does-stretch-database-do"></a>Stretch Database의 기능  
 SQL Server 인스턴스, 데이터베이스 및 하나 이상의 테이블에 Stretch Database를 사용하도록 설정한 경우 Stretch Database는 콜드 데이터를 Azure로 자동으로 마이그레이션하기 시작합니다.  
  
-   콜드 데이터를 별도 테이블에 저장하는 경우 전체 테이블을 마이그레이션할 수 있습니다.  
  
-   테이블에 핫 데이터와 콜드 데이터가 모두 포함된 경우 필터 함수를 지정하여 마이그레이션할 행을 선택할 수 있습니다.

**기존 쿼리 및 클라이언트 앱을 변경할 필요가 없습니다.** 데이터 마이그레이션 중에도 로컬 및 원격 데이터에 계속 원활하게 액세스할 수 있습니다. 원격 쿼리에 대한 짧은 대기 시간이 있지만 이러한 대기 시간은 콜드 데이터를 쿼리할 때만 발생합니다.

마이그레이션 중에 오류가 발생한 경우**Stretch Database를 사용하면 데이터가 손실되지 않습니다** . 또한 마이그레이션 중에 발생할 수 있는 연결 문제를 처리하는 다시 시도 논리가 있습니다. 동적 관리 뷰에서 마이그레이션 상태를 제공합니다.

로컬 서버에서 문제를 해결하거나 사용 가능한 네트워크 대역폭을 최대화하기 위해**데이터 마이그레이션을 일시 중지할 수 있습니다** .  
  
 ![Stretch Database 개요](../../sql-server/stretch-database/media/stretch-overview.png "Stretch Database 개요")  
  
## <a name="is-stretch-database-for-you"></a>Stretch Database의 대상 사용자  
 다음에 해당하는 경우 Stretch Database를 사용하여 요구 사항을 충족하고 문제를 해결할 수 있습니다.  
  
|의사 결정권자인 경우|DBA인 경우|  
|--------------------------------|---------------------|  
|오랜 시간 동안 트랜잭션 데이터를 유지해야 합니다.|테이블 크기가 제어 범위를 벗어났습니다.|  
|경우에 따라 콜드 데이터를 쿼리해야 합니다.|사용자들이 콜드 데이터에 액세스하고 싶다고 말하지만 거의 사용하지 않습니다.|  
|오래된 앱을 포함하여 업데이트하고 싶지 않은 앱이 있습니다.|추가 저장소를 계속 구입하고 추가해야 합니다.|  
|저장소 비용을 절감할 수 있는 방법을 찾고 싶습니다.|큰 테이블을 SLA 내에서 백업하거나 복원할 수 없습니다.|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>Stretch Database에 적합한 데이터베이스 및 테이블 종류  
 Stretch Database는 많은 양의 콜드 데이터가 있고 일반적으로 소수의 테이블에 저장된 트랜잭션 데이터베이스를 대상으로 합니다. 이러한 테이블은 1억 개가 넘는 행을 포함할 수 있습니다.  
  
 
            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 temporal 테이블 기능을 사용하는 경우 스트레치 데이터베이스를 사용하여 연결된 기록 테이블의 전부 또는 일부를 Azure의 비용 효율적인 저장소로 마이그레이션할 수 있습니다. 자세한 내용은 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)를 참조하세요.  
  
 SQL Server 2016 업그레이드 관리자의 기능인 Stretch Database 관리자를 사용하여 Stretch Database용 데이터베이스 및 테이블을 식별할 수 있습니다. 자세한 내용은 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)을 참조하세요. 잠재적 차단 문제에 대한 자세한 내용은 [Stretch Database에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)을 참조하세요.  

## <a name="test-drive-stretch-database"></a>Stretch Database 시험 사용  
 **AdventureWorks 예제 데이터베이스를 사용하여 Stretch Database를 시험 사용합니다.** AdventureWorks 예제 데이터베이스를 가져오려면 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=49502). 예제 데이터베이스를 SQL Server 2016 인스턴스로 복원한 후 예제 파일의 압축을 풀고 Stretch DB 폴더에서 Stretch DB Samples 파일을 엽니다. 이 파일의 스크립트를 실행하여 Stretch Database를 사용하도록 설정하기 전과 후에 데이터에 사용되는 공간을 확인하고, 데이터 마이그레이션 진행 상황을 추적하고, 데이터 마이그레이션 중에, 그리고 그 후에 계속해서 기존 데이터를 쿼리하고 새 데이터를 삽입할 수 있는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
 **Stretch Database에 적합한 데이터베이스 및 테이블 식별.** SQL Server 2016 업그레이드 관리자를 다운로드하고 스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스의 후보 데이터베이스 및 테이블을 식별할 수 있습니다. Stretch Database 관리자는 차단 문제도 식별합니다. 자세한 내용은 [Stretch Database 관리자를 실행하여 Stretch Database용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)을 참조하세요.  
  
  
