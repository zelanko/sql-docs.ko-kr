---
title: Python 및 SQL 데이터 형식 변환
description: 데이터 과학 및 기계 학습 솔루션에서 Python과 SQL Server 간의 암시적 데이터 및 명시적 데이터 형식 변환을 검토합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f22f838bc78d4791e73a1d107cd253aae314d205
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727521"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python과 SQL Server 간의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Machine Learning Services의 Python 통합 기능에서 실행되는 Python 솔루션의 경우 Python과 SQL Server 간에 데이터가 전달될 때 암시적으로 수행될 수 있는 지원되지 않는 데이터 형식 및 데이터 형식 변환의 목록을 검토합니다.

## <a name="python-version"></a>Python 버전

RevoScaleR 기능의 하위 집합(rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees 등)은 새 Python 패키지 **revoscalepy**를 사용하여 Python API를 통해 제공됩니다. 이 패키지를 사용하여 Pandas 데이터 프레임, XDF 파일 또는 SQL 데이터 쿼리를 통해 데이터 작업을 수행할 수 있습니다.

자세한 내용은 [SQL Server의 revoscalepy 모듈](ref-py-revoscalepy.md) 및 [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)를 참조하세요.

Python은 SQL Server에 비해 제한된 수의 데이터 형식을 지원합니다. 결과적으로 Python 스크립트에서 SQL Server의 데이터를 사용할 때마다 데이터는 암시적으로 호환되는 데이터 형식으로 변환될 수 있습니다. 그러나 정확한 변환이 자동으로 수행되지 않고 오류가 반환되는 경우가 많습니다.

## <a name="python-and-sql-data-types"></a>Python 및 SQL Data 형식

이 표에는 제공되는 암시적 변환이 나열되어 있습니다. 다른 데이터 유형은 지원되지 않습니다.

|SQLtype|Python 형식|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|
