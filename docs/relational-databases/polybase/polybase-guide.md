---
title: PolyBase란? | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: b414cf8eb783a64deb65010ab549c9791e82580c
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495376"
---
# <a name="what-is-polybase"></a>PolyBase란?

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017 || >= aps-pdw-2016 || = azure-sqldw-latest"

PolyBase를 통해 SQL Server 2016 인스턴스는 Hadoop에서 데이터를 읽는 Transact-SQL 쿼리를 처리할 수 있습니다. 동일한 쿼리는 SQL Server의 관계형 테이블에 액세스할 수도 있습니다. 또한 PolyBase는 동일한 쿼리가 Hadoop과 SQL Server의 데이터를 조인할 수 있도록 합니다. SQL Server에서 [외부 테이블](../../t-sql/statements/create-external-table-transact-sql.md) 또는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)은 Hadoop에 대한 연결을 제공합니다.

![PolyBase 논리](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")

PolyBase는 Hadoop 노드로 몇몇 계산을 푸시하여 전체 쿼리를 최적화합니다. 그러나 PolyBase 외부 액세스는 Hadoop으로 제한되지 않습니다. 구분된 텍스트 파일 등 기타 비구조적 비관계형 테이블도 지원됩니다.

> [!TIP]
> SQL Server 2019 CTP 2.0에는 SQL Server, Oracle, Teradata 및 MongoDB를 포함하여 PolyBase를 위한 새 커넥터가 도입되었습니다. 자세한 내용은 [SQL Server 2019 CTP 2.0에 대한 PolyBase 설명서](polybase-guide.md?view=sql-server-ver15)를 참조하세요.

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

PolyBase를 통해 SQL Server 인스턴스는 외부 데이터 원본에서 데이터를 읽는 Transact-SQL 쿼리를 처리할 수 있습니다. SQL Server 2016 이상에서는 Hadoop 및 Azure Blob Storage의 외부 데이터에 액세스할 수 있습니다. SQL Server 2019 CTP 2.0부터 이제 PolyBase를 사용하여 [SQL Server](polybase-configure-sql-server.md), [Oracle](polybase-configure-oracle.md), [Teradata](polybase-configure-teradata.md) 및 [MongoDB](polybase-configure-mongodb.md)의 외부 데이터에 액세스할 수 있습니다.

외부 데이터에 액세스하는 것과 동일한 쿼리가 SQL Server 인스턴스의 관계형 테이블을 대상으로 할 수도 있습니다. 따라서 외부 원본의 데이터를 데이터베이스 중요한 관계형 데이터와 결합할 수 있습니다. SQL Server에서 [외부 테이블](../../t-sql/statements/create-external-table-transact-sql.md) 또는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)은 Hadoop에 대한 연결을 제공합니다.

PolyBase는 Hadoop 노드로 몇몇 계산을 푸시하여 전체 쿼리를 최적화합니다. 그러나 PolyBase 외부 액세스는 Hadoop으로 제한되지 않습니다. 구분된 텍스트 파일 등 기타 비구조적 비관계형 테이블도 지원됩니다.

::: moniker-end

### <a name="supported-sql-products-and-services"></a>지원되는 SQL 제품 및 서비스

PolyBase는 Microsoft의 다음 SQL 제품에 대해 동일한 이 기능을 제공합니다.

- SQL Server 2016 이상 버전(Windows만 해당)
- 분석 플랫폼 시스템(이전의 병렬 데이터 웨어하우스)
- Azure SQL 데이터 웨어하우스

### <a name="azure-integration"></a>Azure 통합

PolyBase의 기본 지원을 통해 T-SQL 쿼리도 Azure Blob Storage에서 데이터를 가져오고 내보낼 수 있습니다. 또한 PolyBase는 Azure SQL Data Warehouse가 Azure Data Lake Store 및 Azure Blob Storage에서 데이터를 가져오고 내보낼 수 있도록 합니다.

## <a name="why-use-polybase"></a>PolyBase를 사용하는 이유는?

이전에는 SQL Server 데이터를 외부 데이터와 조인하기가 더 어려웠습니다. 다음과 같은 두 가지 불편한 옵션이 있었습니다.

- 모든 데이터가 한 형식이거나 다른 형식이도록 데이터 절반을 전송합니다.
- 데이터의 소스를 둘 다 쿼리하고 사용자 지정 쿼리 논리를 작성하여 클라이언트 수준에서 데이터를 조인하고 통합합니다.

PolyBase는 데이터를 조인하기 위해 T-SQL을 사용하여 이러한 불편한 옵션을 방지합니다.

PolyBase는 Hadoop 환경에 추가 소프트웨어를 설치할 필요 없이 간단히 사용할 수 있습니다. 데이터베이스 테이블을 쿼리하는 데 사용한 동일한 T-SQL 구문을 사용하여 외부 데이터를 쿼리합니다. PolyBase에서 실행되는 지원 작업은 모두 투명하게 일어납니다. 쿼리 작성자는 Hadoop에 대한 정보가 필요하지 않습니다.

### <a name="polybase-uses"></a>PolyBase 사용

PolyBase를 사용할 경우 SQL Server에서 다음 시나리오가 가능합니다.

- **SQL Server 또는 PDW에서 Hadoop에 저장된 데이터 쿼리.** 사용자는 Hadoop과 같이 비용 효율적으로 분산되고 확장 가능한 시스템에 데이터 집합을 저장하고 있습니다. PolyBase를 사용하면 쉽게 T-SQL을 사용하여 데이터를 쿼리할 수 있습니다.

- **Azure Blob Storage에 저장된 데이터 쿼리.** Azure blob 스토리지는 Azure 서비스에서 사용 하기 위해 데이터를 저장하는 편리한 장소입니다.  PolyBase는 T-SQL을 사용하여 쉽게 데이터에 액세스할 수 있습니다.

- **Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에서 데이터 가져오기** Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에서 가져온 데이터를 관계형 테이블로 가져와 Microsoft SQLss columnstore 기술 및 분석 기능의 속도를 활용합니다. 별도 ETL 또는 가져오기 도구에 대한 요구 사항이 없습니다.

- **Hadoop, Azure Blob Storage 또는 Azure Data Lake Store로 데이터 내보내기** Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에 데이터를 보관하여 비용 효율적인 스토리지를 구현하고 손쉽게 액세스할 수 있도록 온라인 상태로 유지합니다.

- **BI 도구와 통합.** Microsoft의 비즈니스 인텔리전스 및 분석 스택과 함께 PolyBase를 사용하거나 SQL Server와 호환되는 타사 도구를 사용합니다.

## <a name="performance"></a>성능

- **Hadoop에 계산을 푸시합니다.** 쿼리 최적화 프로그램은 비용 기반 결정을 내려 Hadoop에 계산을 푸시하며 이를 통해 쿼리 성능이 향상됩니다.  외부 테이블의 통계를 사용하여 비용 기반 결정을 내립니다. 계산을 푸시하는 데는 MapReduce 작업을 만들고 Hadoop의 분산된 계산 리소스를 활용합니다.

- **컴퓨팅 리소스 크기 조정.** 쿼리 성능을 향상시키기 위해 SQL Server [PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 사용할 수 있습니다. 이를 통해 Hadoop 노드와 SQL Server 인스턴스 간에 병렬 데이터 전송이 가능하며 외부 데이터에서 작동하기 위한 컴퓨팅 리소스를 추가합니다.

<!--SQL Server 2016/2017-->
::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="next-steps"></a>다음 단계

PolyBase를 사용하기 전에 [PolyBase 기능을 설치](polybase-installation.md)해야 합니다. 그런 다음, 데이터 원본에 따라 다음 구성 가이드를 참조하세요.

- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15||>= sql-server-ver15||=sqlallproducts-allversions"

## <a name="next-steps"></a>다음 단계

PolyBase를 사용하기 전에 [PolyBase 기능을 설치](polybase-installation.md)해야 합니다. 그런 다음, 데이터 원본에 따라 다음 구성 가이드를 참조하세요.
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [ODBC 제네릭 형식](polybase-configure-odbc-generic.md)

::: moniker-end
