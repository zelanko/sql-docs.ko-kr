---
title: Python-SQL 데이터 형식 변환
description: Python과 데이터 과학 및 기계 학습 솔루션의 SQL Server 간 암시적 및 명시적 데이터 형식 변환을 검토 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 690126098bbbd3ab26add51a0484f735120351de
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715779"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python과 SQL Server 간의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Machine Learning Services의 Python 통합 기능에서 실행 되는 Python 솔루션의 경우 지원 되지 않는 데이터 형식 목록과 Python과 SQL Server 간에 데이터가 전달 될 때 암시적으로 수행 될 수 있는 데이터 형식 변환의 목록을 검토 합니다.

## <a name="python-version"></a>Python Version

새 Python 패키지 **revoscalepy**를 사용 하 여 python api를 통해 RevoScaleR 기능 (RxLinMod, rxLogit, rxPredict, RxDTrees, rxBTrees)의 하위 집합을 제공 합니다. 이 패키지를 사용 하 여 Pandas 데이터 프레임, XDF 파일 또는 SQL 데이터 쿼리를 사용 하 여 데이터 작업을 수행할 수 있습니다.

자세한 내용은 SQL Server 및 [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) [의 revoscalepy 모듈](ref-py-revoscalepy.md) 을 참조 하세요.

Python은 SQL Server 비교 하 여 제한 된 수의 데이터 형식을 지원 합니다. 결과적으로 Python 스크립트에서 SQL Server 데이터를 사용할 때마다 데이터를 호환 되는 데이터 형식으로 암시적으로 변환할 수 있습니다. 그러나 종종 정확한 변환은 자동으로 수행 될 수 없으며 오류가 반환 됩니다.

## <a name="python-and-sql-data-types"></a>Python 및 SQL 데이터 형식

다음 표에서는 제공 되는 암시적 변환을 보여 줍니다. 다른 데이터 형식은 지원 되지 않습니다.

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
