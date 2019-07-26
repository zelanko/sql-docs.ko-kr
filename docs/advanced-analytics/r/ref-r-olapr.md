---
title: olapR R 함수 라이브러리
description: SQL Server 2016 R Services에서 olapR 함수 라이브러리를 소개 하 고 R을 사용 하 여 SQL Server 2017 Machine Learning Services를 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 674e4ed4d1967452093e81e7bb4f5518d9237cf6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469972"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Olapr** 는 SQL Server Analysis Services OLAP 큐브에 대해 MDX 쿼리에 사용 되는 R 함수의 Microsoft 라이브러리입니다. 함수는 일부 MDX 작업을 지원 하지 않지만 차원에서 조각화, 분석, 드릴 다운, 롤업 및 피벗 하는 쿼리를 작성할 수 있습니다. 

이 패키지는 R 세션으로 미리 로드 되지 않습니다. 다음 명령을 실행 하 여 라이브러리를 로드 합니다.

```R
library(olapR)
```

지원 되는 모든 SQL Server 버전의 Analysis Services OLAP 큐브에 대 한 연결에서이 라이브러리를 사용할 수 있습니다. 테이블 형식 모델에 대 한 연결은 지금은 지원 되지 않습니다.

## <a name="package-version"></a>패키지 버전

현재 버전은 모든 Windows 전용 제품에서 1.0.0 이며 라이브러리를 제공 하는 다운로드입니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**Olapr** 라이브러리는 여러 Microsoft 제품에 배포 되지만, SQL Server 또는 다른 제품에 라이브러리를 가져올 때 사용 됩니다. 함수는 동일 하기 때문에 [개별 sqlrutils 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) 는 Microsoft Machine Learning Server에 대 한 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 의 한 위치에만 게시 됩니다. 제품별 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시 됩니다.

## <a name="availability-and-location"></a>가용성 및 위치

이 패키지는 다음 제품 뿐만 아니라 Azure의 여러 가상 머신 이미지에도 제공 됩니다. 패키지 위치는 그에 따라 다릅니다.

Product | 위치 |
--------|----------|
SQL Server 2017 Machine Learning Services (R 통합 포함) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Azure에서 SQL Server 가상 컴퓨터 <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 통합은 SQL Server에서 선택 사항입니다. VM을 구성 하는 동안 Machine Learning 또는 R 기능을 추가 하면 olapR 라이브러리가 설치 됩니다.


## <a name="see-also"></a>참조

[OlapR을 사용 하 여 MDX 쿼리를 만드는 방법](how-to-create-mdx-queries-using-olapr.md)
