---
title: Stretch Database
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ff3c8a24624b3833c04b4e6269fb3618b36568f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488364"
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database는 콜드 데이터를 투명하고 안전하게 Microsoft Azure 클라우드로 마이그레이션합니다.  
  
 Stretch Database를 지금 바로 시작하려면 [스트레치에 데이터베이스 사용 마법사를 실행하여 시작](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)을 참조하세요.  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Stretch Database의 장점은 무엇입니까?  
 Stretch Database는 다음과 같은 이점을 제공합니다.  
  
 **콜드 데이터에 대한 비용 효율적인 가용성 제공**  
 SQL Server Stretch Database를 통해 콜드 및 웜 트랜잭션 데이터를 SQL Server에서 Microsoft Azure로 동적으로 확장합니다. 일반적인 콜드 데이터 스토리지와 달리 데이터가 항상 온라인 상태이며 쿼리할 수 있습니다. 고객 주문 기록과 같은 큰 테이블에 대한 부담 없이 보다 긴 데이터 보존 일정을 제공할 수 있습니다. 값비싼 온-프레미스 스토리지를 확장하는 대신 저렴한 비용의 Azure의 이점을 활용합니다. Azure 포털에서 가격 책정 계층을 선택하고 설정을 구성하여 가격 및 비용을 관리할 수 있습니다. 필요한 만큼 규모를 확장하거나 축합니다. 자세한 내용은 [SQL Server Stretch Database 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) 를 참조하세요.  
  
 **쿼리 또는 애플리케이션을 변경할 필요가 없음**  
 온-프레미스에 있든 클라우드로 확장되든 상관없이 SQL Server 데이터에 원활하게 액세스할 수 있습니다.  데이터를 저장하고 SQL Server가 백그라운드에서 데이터 이동을 처리하는 위치를 결정하는 정책을 설정합니다. 전체 테이블은 항상 온라인 상태이며 쿼리할 수 있습니다. 또한 Stretch Database는 기존 쿼리 또는 애플리케이션을 변경할 필요가 없습니다. 데이터의 위치가 애플리케이션에 완전히 투명합니다.  
  
 **온-프레미스 데이터 유지 관리 간소화**  
 온-프레미스 유지 관리와 데이터의 스토리지를 줄입니다. 온-프레미스 데이터에 대한 백업을 더 빠르게 실행하고 유지 관리 기간 내에 완료합니다. 데이터의 클라우드 부분에 대한 백업이 자동으로 실행됩니다. 온-프레미스 스토리지 요구량이 크게 감소합니다. Azure Storage는 온-프레미스 SSD에 추가하는 비용의 80%까지 절약할 수 있습니다.  
  
 **마이그레이션 중 데이터 보안 유지**  
 가장 중요한 애플리케이션을 클라우드로 안전하게 확장할 수 있습니다. SQL Server의 Always Encrypted는 이동 중인 데이터에 대한 암호화를 제공합니다. 행 수준 보안(RLS) 및 기타 고급 SQL Server 보안 기능 또한 Stretch Database와 함께 데이터를 보호합니다.  
  
## <a name="what-does-stretch-database-do"></a>Stretch Database의 기능은 무엇입니까?  
 SQL Server 인스턴스 및 데이터베이스에 Stretch Database를 사용하도록 설정하였고 하나 이상의 테이블을 선택했다면 Stretch Database는 콜드 데이터를 Azure로 자동으로 마이그레이션하기 시작합니다.  
  
-   콜드 데이터를 별도 테이블에 저장하는 경우 전체 테이블을 마이그레이션할 수 있습니다.  
  
-   테이블에 핫 데이터와 콜드 데이터가 모두 포함된 경우 필터 함수를 지정하여 마이그레이션할 행을 선택할 수 있습니다.

**기존 쿼리 및 클라이언트 앱을 변경할 필요가 없습니다.** 데이터 마이그레이션 중에도 로컬 및 원격 데이터에 계속 원활하게 액세스할 수 있습니다. 원격 쿼리에 대한 짧은 대기 시간이 있지만 이러한 대기 시간은 콜드 데이터를 쿼리할 때만 발생합니다.

**Stretch Database는 마이그레이션 중에 오류가 발생할 경우 데이터가 손실되지 않도록 합니다** . 또한 마이그레이션하는 동안 발생할 수 있는 연결 문제를 처리하기 위한 재시도 논리도 있습니다. 동적 관리 뷰를 통해 마이그레이션 상태를 확인합니다.

로컬 서버에서 문제를 해결하거나 사용 가능한 네트워크 대역폭을 최대화하기 위해**데이터 마이그레이션을 일시 중지할 수 있습니다** .  
  
 ![Stretch 데이터베이스 개요](../../sql-server/stretch-database/media/stretch-overview.png "Stretch 데이터베이스 개요")  
  
## <a name="is-stretch-database-for-you"></a>Stretch Database는 어떤 도움을 줍니까?  
 다음 문을 만들 수 있는 경우 Stretch Database가 요구 사항을 충족하고 문제를 해결하는 데 도움이 될 수 있습니다.  
  
|의사 결정권자인 경우|DBA인 경우|  
|--------------------------------|---------------------|  
|오랜 시간 동안 트랜잭션 데이터를 유지해야 합니다.|테이블 크기가 통제 수준을 벗어나고 있습니다.|  
|경우에 따라 콜드 데이터를 쿼리해야 합니다.|사용자들이 콜드 데이터에 액세스하고 싶다고 말하지만 거의 사용하지 않습니다.|  
|오래된 앱을 포함하여 업데이트하고 싶지 않은 앱이 있습니다.|스토리지를 계속 구입하고 추가해야 합니다.|  
|스토리지에 대한 비용을 절약하고 싶습니다.|큰 테이블을 SLA 내에서 백업하거나 복원할 수 없습니다.|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>어떤 종류의 데이터베이스 및 테이블이 Stretch Database가 될 수 있습니까?  
 Stretch Database는 일반적으로 대용량의 콜드 데이터가 적은 수의 테이블에 저장되는 트랜잭션 데이터베이스를 위한 것입니다. 이러한 테이블은 1억 개가 넘는 행을 포함할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 temporal 테이블 기능을 사용하는 경우 스트레치 데이터베이스를 사용하여 연결된 기록 테이블의 전부 또는 일부를 Azure의 비용 효율적인 스토리지로 마이그레이션할 수 있습니다. 자세한 내용은 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)를 참조하세요.  
  
 SQL Server 2016 업그레이드 관리자의 기능인 Stretch Database 관리자를 사용하여 Stretch Database용 데이터베이스 및 테이블을 식별합니다. 자세한 내용은 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)을 참조하세요. 잠재적인 차단 문제에 대한 자세한 내용은 [Stretch Database에 대한 제한](../../sql-server/stretch-database/limitations-for-stretch-database.md)을 참조하세요.  

## <a name="test-drive-stretch-database"></a>Stretch Database 시험 사용  
 **AdventureWorks 예제 데이터베이스를 사용하여 Stretch Database를 시험 사용합니다.** AdventureWorks 예제 데이터베이스를 가져오려면 [여기](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks). 샘플 데이터베이스를 SQL Server 2016의 인스턴스에 복원한 후, 샘플 파일의 압축을 풀고 스트레치 DB 폴더에서 스트레치 DB 샘플 파일을 엽니다. 이 파일에서 스크립트를 실행하여 Stretch Database 사용 전후 데이터가 사용하는 공간을 확인하고, 데이터 마이그레이션의 진행 상황을 추적하며, 그리고 데이터 마이그레이션 도중 및 이후에도 계속 기존 데이터를 쿼리하고 새 데이터를 삽입할 수 있는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
 **스트레치 데이터베이스에 적합한 데이터베이스 및 테이블 식별.** Data Migration Assistant를 다운로드하고 평가를 실행하여 Stretch Database의 후보인 데이터베이스 및 테이블을 식별합니다. 자세한 내용은 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)을 참조하세요.  
  
  
