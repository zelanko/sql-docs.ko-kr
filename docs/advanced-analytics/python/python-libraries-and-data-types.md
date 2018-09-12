---
title: SQL Server Machine Learning에서 Python 라이브러리 및 데이터 형식 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 384c8c94bdef65e41af999848c9bac63fc0c8d40
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888369"
---
# <a name="python-libraries-and-data-types"></a>Python 라이브러리 및 데이터 형식
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server Machine Learning Services (In-database) 및 (독립 실행형) 설치에 포함 된 Python 라이브러리를 설명 합니다.

이 문서는 지원 되지 않는 데이터 형식에도 나열 및 목록 데이터 형식 변환이 Python 및 SQL Server 간에 데이터를 전달 하는 경우 암시적으로 수행할 수 있는 합니다.

## <a name="python-version"></a>Python 버전

SQL Server 2017 Anaconda 4.2 배포 및 Python 3.6입니다.

RevoScaleR 기능의 하위 집합 (rxLinMod를 rxLogit rxPredict, rxDTrees, rxBTrees, 아마도 몇몇 다른) 새 Python 패키지를 사용 하 여 Python Api를 사용 하 여 제공 됩니다 **revoscalepy**합니다. Pandas 데이터 프레임, XDF 파일 또는 SQL 데이터 쿼리를 사용 하 여 데이터를 사용 하려면이 패키지를 사용할 수 있습니다.

자세한 내용은 [revoscalepy 란?](what-is-revoscalepy.md)합니다.

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



