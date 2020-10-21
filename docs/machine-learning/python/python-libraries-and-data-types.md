---
title: Python 및 SQL 데이터 형식 변환
description: 데이터 과학 및 기계 학습 솔루션에서 Python과 SQL Server 간의 암시적 데이터 및 명시적 데이터 형식 변환을 검토합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: da92713dbf514e2500d0d5f8eb3e776523830041
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891353"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python과 SQL Server 간의 데이터 형식 매핑
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

이 문서에는 SQL Server Machine Learning Services의 Python 통합 기능을 사용할 때 지원되는 데이터 형식 및 수행되는 데이터 형식 변환이 나와 있습니다.

Python은 SQL Server에 비해 제한된 수의 데이터 형식을 지원합니다. 결과적으로 Python 스크립트에서 SQL Server의 데이터를 사용할 때마다 SQL 데이터는 암시적으로 호환되는 Python 데이터 형식으로 변환될 수 있습니다. 그러나 정확한 변환이 자동으로 수행되지 않고 오류가 반환되는 경우가 많습니다.

## <a name="python-and-sql-data-types"></a>Python 및 SQL Data 형식

이 표에는 제공되는 암시적 변환이 나열되어 있습니다. 다른 데이터 유형은 지원되지 않습니다.

| SQL 유형             | Python 형식 | Description |
|----------------------|-------------|-------------|
| **bigint**           | `float64`   |
| **binary**           | `bytes`     |
| **bit**              | `bool`      |
| **char**             | `str`       |
| **date**             | `datetime`  |
| **datetime**         |`datetime`   | SQL Server 2017 CU6 이상에서 지원됩니다(**NumPy** 배열 `datetime.datetime` 형식 또는 **Pandas** `pandas.Timestamp` 사용). `sp_execute_external_script`가 이제 소수 자릿수 초의 `datetime` 형식을 지원합니다.|
| **float**            | `float64`   |
| **nchar**            | `str`       |
| **nvarchar**         | `str`       |
| **nvarchar(max)**    | `str`       |
| **real**             | `float64`   |
| **smalldatetime**    | `datetime`  |
| **smallint**         | `int32`     |
| **tinyint**          | `int32`     |
| **uniqueidentifier** | `str`       |
| **varbinary**        | `bytes`     |
| **varbinary(max)**   | `bytes`     |
| **varchar(n)**       | `str`       |
| **varchar(max)**     | `str`       |

## <a name="see-also"></a>추가 정보

+ [R과 SQL Server 간의 데이터 형식 매핑](../r/r-libraries-and-data-types.md)
