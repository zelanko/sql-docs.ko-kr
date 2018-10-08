---
title: PolyBase 가이드 | Microsoft 문서
ms.date: 05/31/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: quickstart
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c31f9538f3429ff4ae1182ee0cd974996cc705a6
ms.sourcegitcommit: 82bb56269faf3fb5dd1420418e32a0a6476780cc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43694726"
---
# <a name="polybase-guide"></a>PolyBase 가이드

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

PolyBase를 통해 SQL Server 2016 인스턴스는 Hadoop에서 데이터를 읽는 Transact-SQL 쿼리를 처리할 수 있습니다. 동일한 쿼리는 SQL Server의 관계형 테이블에 액세스할 수도 있습니다. 또한 PolyBase는 동일한 쿼리가 Hadoop과 SQL Server의 데이터를 조인할 수 있도록 합니다. SQL Server에서 [외부 테이블](../../t-sql/statements/create-external-table-transact-sql.md) 또는 [외부 데이터 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)은 Hadoop에 대한 연결을 제공합니다.

PolyBase는 Microsoft의 다음 SQL 제품에 대해 동일한 이 기능을 제공합니다.

- SQL Server 2016 이상 버전
- 분석 플랫폼 시스템(이전의 병렬 데이터 웨어하우스)
- Azure SQL 데이터 웨어하우스

PolyBase는 Hadoop 노드로 몇몇 계산을 푸시하여 전체 쿼리를 최적화합니다. 그러나 PolyBase 외부 액세스는 Hadoop으로 제한되지 않습니다. 구분된 텍스트 파일 등 기타 비구조적 비관계형 테이블도 지원됩니다.

#### <a name="data-import-and-export"></a>데이터 가져오기 및 내보내기

PolyBase의 기본 지원을 통해 T-SQL 쿼리도 Azure Blob Storage에서 데이터를 가져오고 내보낼 수 있습니다. 또한 PolyBase는 Azure SQL Data Warehouse가 Azure Data Lake Store 및 Azure Blob Storage에서 데이터를 가져오고 내보낼 수 있도록 합니다.

PolyBase를 사용하려면 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.
  
![PolyBase 논리](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")

## <a name="why-use-polybase"></a>PolyBase를 사용하는 이유는?

이전에는 SQL Server 데이터를 외부 데이터와 조인하기가 더 어려웠습니다. 다음과 같은 두 가지 불편한 옵션이 있었습니다.

- 모든 데이터가 한 형식이거나 다른 형식이도록 데이터 절반을 전송합니다.
- 데이터의 소스를 둘 다 쿼리하고 사용자 지정 쿼리 논리를 작성하여 클라이언트 수준에서 데이터를 조인하고 통합합니다.

PolyBase는 데이터를 조인하기 위해 T-SQL을 사용하여 이러한 불편한 옵션을 방지합니다.

PolyBase는 Hadoop 환경에 추가 소프트웨어를 설치할 필요 없이 간단히 사용할 수 있습니다. 데이터베이스 테이블을 쿼리하는 데 사용한 동일한 T-SQL 구문을 사용하여 외부 데이터를 쿼리합니다. PolyBase에서 실행되는 지원 작업은 모두 투명하게 일어납니다. 쿼리 작성자는 Hadoop에 대한 정보가 필요하지 않습니다.

PolyBase는 다음 작업을 수행할 수 있습니다.

- **SQL Server 또는 PDW에서 Hadoop에 저장된 데이터 쿼리.** 사용자는 Hadoop과 같이 비용 효율적으로 분산되고 확장 가능한 시스템에 데이터 집합을 저장하고 있습니다. PolyBase를 사용하면 쉽게 T-SQL을 사용하여 데이터를 쿼리할 수 있습니다.

- **Azure Blob Storage에 저장된 데이터 쿼리.** Azure blob 저장소는 Azure 서비스에서 사용 하기 위해 데이터를 저장하는 편리한 장소입니다.  PolyBase는 T-SQL을 사용하여 쉽게 데이터에 액세스할 수 있습니다.

- **Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에서 데이터 가져오기** Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에서 가져온 데이터를 관계형 테이블로 가져와 Microsoft SQLss columnstore 기술 및 분석 기능의 속도를 활용합니다. 별도 ETL 또는 가져오기 도구에 대한 요구 사항이 없습니다.

- **Hadoop, Azure Blob Storage 또는 Azure Data Lake Store로 데이터 내보내기** Hadoop, Azure Blob Storage 또는 Azure Data Lake Store에 데이터를 보관하여 비용 효율적인 저장소를 구현하고 손쉽게 액세스할 수 있도록 온라인 상태로 유지합니다.

- **BI 도구와 통합.** Microsoft의 비즈니스 인텔리전스 및 분석 스택과 함께 PolyBase를 사용하거나 SQL Server와 호환되는 타사 도구를 사용합니다.

## <a name="performance"></a>성능

- **Hadoop에 계산을 푸시합니다.** 쿼리 최적화 프로그램은 비용 기반 결정을 내려 Hadoop에 계산을 푸시하며 이를 통해 쿼리 성능이 향상됩니다.  외부 테이블의 통계를 사용하여 비용 기반 결정을 내립니다. 계산을 푸시하는 데는 MapReduce 작업을 만들고 Hadoop의 분산된 계산 리소스를 활용합니다.

- **계산 리소스 크기 조정.** 쿼리 성능을 향상시키기 위해 SQL Server [PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 사용할 수 있습니다. 이를 통해 Hadoop 노드와 SQL Server 인스턴스 간에 병렬 데이터 전송이 가능하며 외부 데이터에서 작동하기 위한 계산 리소스를 추가합니다.

## <a name="polybase-guide-topics"></a>PolyBase 가이드 항목

이 가이드에는 효율적이고 효과적으로 PolyBase를 사용하는 항목이 포함되어 있습니다.

|||
|-|-|
|**항목**|**설명**|
|[PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)|PolyBase를 설치하고 구성하는 기본 단계입니다. Hadoop 또는 Azure blob 저장소의 데이터를 가리키는 외부 개체를 만드는 방법을 보여 주며 쿼리 예제를 제공합니다.|
|[PolyBase 버전 기능 요약](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|SQL Server, SQL 데이터베이스 및 SQL 데이터 웨어하우스에서 지원되는 PolyBase 기능을 설명합니다.|
|[PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)|SQL Server 스케일 아웃 그룹을 사용하여 SQL Server 및 Hadoop 간에 병렬 처리를 확장합니다.|
|[PolyBase 설치](../../relational-databases/polybase/polybase-installation.md)|설치 마법사 또는 명령줄 도구를 사용하여 PolyBase를 설치하기 위한 단계 및 참조 사항입니다.|
|[PolyBase 구성](../../relational-databases/polybase/polybase-configuration.md)|PolyBase용 SQL Server 설정을 구성합니다.  예를 들어 계산 푸시다운 및 kerberos 보안을 구성합니다.|
|[PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)|PolyBase가 외부 데이터를 정의하고 액세스하는 데 사용하는 T-SQL 개체를 만듭니다.|
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|T-SQL 문을 사용하여 외부 데이터를 쿼리, 가져오기 또는 내보냅니다.|
|[PolyBase 문제 해결](../../relational-databases/polybase/polybase-troubleshooting.md)|PolyBase 쿼리를 관리하는 기술입니다. DMV(동적 관리 뷰)를 사용하여 PolyBase 쿼리를 모니터링하고 PolyBase 쿼리 계획을 확인하여 성능 병목 현상을 찾아내는 방법을 알아봅니다.|
| &nbsp; | &nbsp; |
  
