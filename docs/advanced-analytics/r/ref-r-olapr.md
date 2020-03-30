---
title: olapR R 함수 라이브러리
description: SQL Server 2016 R Services 및 SQL Server Machine Learning Services(R 포함)의 olapR 함수 라이브러리를 소개합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68715002"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR(SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR**은 SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 R 함수의 Microsoft 라이브러리입니다. 함수는 일부 MDX 작업을 지원하지 않지만 차원에서 조각화, 분석, 드릴다운, 롤업 및 피벗을 수행하는 쿼리를 작성할 수 있습니다. 

이 패키지는 R 세션으로 미리 로드되지 않습니다. 다음 명령을 실행하여 라이브러리를 로드합니다.

```R
library(olapR)
```

지원되는 모든 SQL Server 버전에서 Analysis Services OLAP 큐브에 연결하는 데 이 라이브러리를 사용할 수 있습니다. 현재, 테이블 형식 모델에는 연결할 수 없습니다.

## <a name="package-version"></a>패키지 버전

현재 버전은 라이브리를 제공하는 모든 Windows 전용 제품 및 다운로드에서 1.0.0입니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**olapr** 라이브러리는 여러 Microsoft 제품에 배포되지만, SQL Server에서 라이브러리를 가져오든, 다른 제품에서 라이브러리를 가져오든, 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 sqlrutils 함수에 대한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)는 Microsoft Machine Learning Server에 대한 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

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

<sup>1</sup> R 통합은 SQL Server에서 선택 사항입니다. VM을 구성하는 동안 Machine Learning 또는 R 기능을 추가하면 olapR 라이브러리가 설치됩니다.


## <a name="see-also"></a>참고 항목

[olapR을 사용하여 MDX 쿼리를 만드는 방법](how-to-create-mdx-queries-using-olapr.md)
