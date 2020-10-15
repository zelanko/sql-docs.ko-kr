---
title: olapR R 패키지
description: olapR은 SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 Microsoft의 R 패키지입니다. 함수는 일부 MDX 작업을 지원하지 않지만 차원에서 조각화, 분석, 드릴다운, 롤업 및 피벗을 수행하는 쿼리를 작성할 수 있습니다. 이 패키지는 SQL Server Machine Learning Services 및 SQL Server 2016 R Services에 포함되어 있습니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f34a6d26e48c1a77d7e289b197495d707bb9fd12
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956874"
---
# <a name="olapr-r-package-in-sql-server-machine-learning-services"></a>olapR(SQL Server Machine Learning Services의 R 패키지)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**olapR**은 SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 Microsoft의 R 패키지입니다. 함수는 일부 MDX 작업을 지원하지 않지만 차원에서 조각화, 분석, 드릴다운, 롤업 및 피벗을 수행하는 쿼리를 작성할 수 있습니다. 이 패키지는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 및 [SQL Server 2016 R Services](sql-server-r-services.md)에 포함되어 있습니다.

지원되는 모든 SQL Server 버전에서 Analysis Services OLAP 큐브에 연결하는 데 이 패키지를 사용할 수 있습니다. 현재, 테이블 형식 모델에는 연결할 수 없습니다.

## <a name="load-package"></a>패키지 로드

**olapR** 패키지는 R 세션으로 미리 로드되지 않습니다. 다음 명령을 실행하여 패키지를 로드합니다.

```R
library(olapR)
```

## <a name="package-version"></a>패키지 버전

현재 버전은 패키지를 제공하는 모든 Windows 전용 제품 및 다운로드에서 1.0.0입니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**olapr** 패키지는 여러 Microsoft 제품에 배포되지만, 패키지를 SQL Server에서 가져오든 다른 제품에서 가져오든 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 sqlrutils 함수에 대한 설명서](/machine-learning-server/r-reference/olapr/olapr)는 Microsoft Machine Learning Server에 대한 [R 참조](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

## <a name="availability-and-location"></a>가용성 및 위치

이 패키지는 다음 제품 뿐만 아니라 Azure의 여러 가상 머신 이미지에도 제공됩니다. 패키지 위치는 그에 따라 다릅니다.

Product | 위치 |
--------|----------|
SQL Server Machine Learning Services(R 통합 포함) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server(R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
데이터 과학 가상 머신(Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server 가상 머신(Azure)<sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 통합은 SQL Server에서 선택 사항입니다. VM을 구성하는 동안 Machine Learning 또는 R 기능을 추가하면 olapR 패키지가 설치됩니다.


## <a name="see-also"></a>참고 항목

[olapR을 사용하여 MDX 쿼리를 만드는 방법](how-to-create-mdx-queries-using-olapr.md)