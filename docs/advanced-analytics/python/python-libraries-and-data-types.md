---
title: Python SQL 데이터 형식 변환-SQL Server Machine Learning
description: 데이터 과학 및 기계 학습 솔루션에 Python과 SQL Server 간 암시적 및 명시적 데이터 형식 converstions를 검토 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6a7cb7e8f93489bb52c1457fbf25bf7206026914
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642751"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python과 SQL Server 간 데이터 형식 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Machine Learning Services의 Python 통합 기능은에서 실행 되는 Python 솔루션에 대 한 지원 되지 않는 데이터 형식 및 Python과 SQL Server 간에 데이터를 전달 하는 경우 암시적으로 수행할 수 있는 데이터 형식 변환의 목록을 검토 합니다.

## <a name="python-version"></a>Python Version

SQL Server 2017 Anaconda 4.2 배포 및 Python 3.6입니다.

RevoScaleR 기능의 하위 집합 (rxLinMod를 rxLogit rxPredict, rxDTrees, rxBTrees, 아마도 몇몇 다른) 새 Python 패키지를 사용 하 여 Python Api를 사용 하 여 제공 됩니다 **revoscalepy**합니다. Pandas 데이터 프레임, XDF 파일 또는 SQL 데이터 쿼리를 사용 하 여 데이터를 사용 하려면이 패키지를 사용할 수 있습니다.

자세한 내용은 [SQL Server에서 revoscalepy 모듈](ref-py-revoscalepy.md) 하 고 [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python은 SQL Server에 비해 데이터 형식의 제한 된 수를 지원합니다. 결과적으로, Python 스크립트에서 SQL Server에서 데이터를 사용할 때마다 데이터 변환 될 수 있습니다 암시적으로 호환 되는 데이터 형식입니다. 그러나는 정확한 변환을 자동으로 수행할 수 없는 경우가 많습니다 하 고 오류가 반환 됩니다.

## <a name="python-and-sql-data-types"></a>Python 및 SQL 데이터 형식

이 표에서 제공 되는 암시적 변환을 보여 줍니다. 다른 데이터 형식은 지원 되지 않습니다.

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

## <a name="see-also"></a>참고자료

