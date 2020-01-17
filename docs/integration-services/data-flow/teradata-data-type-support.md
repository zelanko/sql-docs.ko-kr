---
title: Teradata 데이터 형식 지원 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f83f028772a93dbd2104d9f449fcd7aa3b1be0d8
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543011"
---
# <a name="data-type-support"></a>데이터 형식 지원

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

SSIS 구성 요소는 TPT API(Teradata Parallel Transporter API)를 사용하여 Teradata 데이터베이스와 사이에서 데이터를 로드하고 전송하므로 SSIS에서 TPT API 지원 데이터 형식만 사용할 수 있습니다.

> [!NOTE]
>
> Teradata의 TIME, TIMESTAMP 및 INTERVAL 데이터 형식은 TPT API에서 고정 크기의 문자열로 처리됩니다. 이는 Teradata용 SSIS 구성 요소에서 문자열로 처리됩니다.

## <a name="data-type-mapping"></a>데이터 형식 매핑

다음 표에서는 Teradata 데이터베이스 데이터 형식과 SSIS 데이터 형식에 대한 기본 매핑을 보여 줍니다. 또한 지원되지 않는 Teradata 데이터 형식도 나와 있습니다.

|SQL 데이터 형식|SSIS 데이터 형식|
|:-|:-|
|DECIMAL/NUMERIC|DT_NUMERIC|
|BYTEINT|DT_I1|
|SMALLINT|DT_I2|
|INTEGER|DT_I4|
|FLOAT/REAL/DOUBLE PRECISION|DT_R8|
|DATE|DT_DBDATE|
|TIME<br>TIME(n)|DT_STR|
|timestamp<br>TIMESTAMP (n)|DT_STR|
|TIME WITH TIMEZONE<br>TIME(n) WITH TIMEZONE|DT_STR|
|TIMESTAMP WITH TIMEZONE<br>TIMESTAMP(n) WITH TIMEZONE|DT_STR|
|INTERVAL YEAR<br>INTERVAL YEAR (n)|DT_STR|
|INTERVAL YEAR TO MONTH<br>INTERVAL YEAR (n) TO MONTH|DT_STR|
|INTERVAL MONTH<br>INTERVAL MONTH (n)|DT_STR|
|INTERVAL DAY<br>INTERVAL DAY (n)|DT_STR|
|INTERVAL DAY TO HOUR<br>INTERVAL DAY (n) TO HOUR|DT_STR|
|INTERVAL DAY TO MINUTE<br>INTERVAL DAY (n) TO MINUTE|DT_STR|
|INTERVAL DAY TO SECOND<br>INTERVAL DAY (n) TO SECOND<br>INTERVAL DAY TO SECOND (m)<br>INTERVAL DAY (n) TO SECOND (m)|DT_STR|
|INTERVAL HOUR<br>INTERVAL HOUR (n)|DT_STR|
|INTERVAL HOUR TO MINUTE<br>INTERVAL HOUR (n) TO MINUTE|DT_STR
|INTERVAL HOUR TO SECOND<br>INTERVAL HOUR (n) TO SECOND<br>INTERVAL HOUR TO SECOND (m)<br>INTERVAL HOUR (n) TO SECOND (m)|DT_STR|
|INTERVAL MINUTE<br>INTERVAL MINUTE (n)|DT_STR|
|INTERVAL MINUTE TO SECOND<br>INTERVAL MINUTE (n) TO SECOND<br>INTERVAL MINUTE TO SECOND (m)<br>INTERVAL MINUTE (n) TO SECOND (m)|DT_STR|
|INTERVAL SECOND<br>INTERVAL SECOND (n)<br>INTERVAL SECOND (n,m)|DT_STR|
|PERIOD(DATE)|DT_STR|
|PERIOD(TIME)|DT_STR|
|NUMBER|DT_STR|
|CHARACTER|DT_STR|
|VARCHAR|DT_STR(유니코드 문자 집합의 경우 DT_WSTR)<br>**참고**:<br> 지원되는 VARCHAR의 최대 길이는 32,000자입니다. <br> DT_STR의 최대 허용 길이는 8,000자이고, DT_WSTR의 최대 허용 길이는 4,000자입니다. 초과하면 데이터가 잘립니다.|
|LONG VARCHAR|지원되지 않음|
|CLOB|지원되지 않음|
|BYTE|DT_BYTES<br>**참고**: 최대 허용 길이는 8,000바이트입니다. 초과하면 데이터가 잘립니다.|
|VARBYTE|DT_BYTES<br>**참고**: 최대 허용 길이는 8,000바이트입니다. 초과하면 데이터가 잘립니다.|
|BLOB|지원되지 않음|

## <a name="next-steps"></a>다음 단계

- [Teradata 연결 관리자](teradata-connection-manager.md) 구성
- [Teradata 원본](teradata-source.md) 구성
- [Teradata 대상](teradata-destination.md) 구성
- 질문이 있으면 [Tech Community](https://aka.ms/AA6iwdw)를 방문하세요.
