---
title: olapR R 함수 라이브러리-SQL Server Machine Learning 서비스
description: SQL Server 2016 R Services 및 SQL Server 2017 Machine Learning Services R. 사용 하 여 olapR 함수 라이브러리 소개
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1426871c70eb905a0defda206d1a331662e3155c
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645152"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR** SQL Server Analysis Services OLAP 큐브에 대해 MDX 쿼리에 사용 되는 R 함수의 Microsoft 라이브러리입니다. 함수는 MDX의 모든 작업을 지원 하지 않습니다 하지만 쿼리 조각, 분석, 드릴 다운, 롤업, 피벗 차원으로 빌드할 수 있습니다. 

이 패키지는 R 세션에 미리 로드 되지 않은 합니다. 라이브러리를 로드 하려면 다음 명령을 실행 합니다.

```R
library(olapR)
```

모든 지원 되는 버전의 SQL Server에서 Analysis Services OLAP 큐브에 연결에서이 라이브러리를 사용할 수 있습니다. 이 이번에는 테이블 형식 모델에 대 한 연결을 사용할 수 없습니다.

## <a name="package-version"></a>패키지 버전

현재 버전 1.0.0 모든 Windows 전용 제품에서 이며 제공 라이브러리를 다운로드 합니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **olapr** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 sqlrutils 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) 아래에 있는 하나의 위치에 게시 되는 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="availability-and-location"></a>가용성 및 위치

이 패키지는 Azure에서 여러 가상 머신 이미지 뿐만 아니라 다음 제품에 제공 됩니다. 패키지 위치에 따라 달라 집니다.

Product | 위치 |
--------|----------|
SQL Server 2017 Machine Learning Services (R 통합) | C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13입니다. MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
(Azure)에서 데이터 과학 Virtual Machine | C:\Program Files\Microsoft\R Client\R_SERVER\library |
(Azure)에서 SQL Server Virtual Machine <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 통합 SQL Server에서는 선택 사항입니다. VM 구성 하는 동안 Machine Learning 또는 R 기능을 추가 하면 olapR 라이브러리 설치 됩니다.


## <a name="see-also"></a>참고자료

[OlapR을 사용 하 여 MDX 쿼리를 만드는 방법](how-to-create-mdx-queries-using-olapr.md)
