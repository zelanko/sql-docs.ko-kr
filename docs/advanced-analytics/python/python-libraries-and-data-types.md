---
title: SQL Server 기계 학습에서 Python 라이브러리 및 데이터 형식 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8dfa7f343a3a179b05b624a083238e08011c4a5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="python-libraries-and-data-types"></a>Python 라이브러리 및 데이터 형식
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 컴퓨터 학습 Services (In-database) 및 (독립 실행형) 설치에 포함 된 Python 라이브러리를 설명 합니다.

이 문서에는 또한 지원 되지 않는 데이터 형식을 나열 하 고 목록에서 데이터 형식 변환 Python 및 SQL Server 간에 데이터를 전달 하는 경우 암시적으로 수행할 수 있는 합니다.

## <a name="python-version"></a>Python 버전

SQL Server 2017 CTP 2.0 Anaconda 배포 및 Python 3.6의 일부를 포함합니다.

RevoScaleR 기능의 하위 집합 (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, 어쩌면 몇 가지 다른) 새 Python 패키지를 사용 하 여 Python Api를 사용 하 여 제공 됩니다 **revoscalepy**합니다. 팬더 데이터 프레임, XDF 파일 또는 SQL 데이터 쿼리를 사용 하 여 데이터를 작성 하려면이 패키지를 사용할 수 있습니다.

자세한 내용은 참조 [revoscalepy 란?](what-is-revoscalepy.md)합니다.

## <a name="python-and-sql-data-types"></a>Python 및 SQL 데이터 형식

Python에는 제한 된 수의 SQL Server에 비해 데이터 형식 지원합니다.

결과적으로, 데이터를 사용할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Python 스크립트에서 변환 될 수 있습니다 암시적으로 호환 되는 데이터 형식으로. 그러나 정확한 변환을 자동으로 수행할 수 없는 경우가 있으며 오류가 반환 됩니다.

이 표에서 제공 되는 암시적 변환을 보여 줍니다. 다른 데이터 형식은 지원 되지 않습니다.

|SQLtype|Python 유형|
|-|-|
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



