---
title: Microsoft Connector for Oracle 데이터 형식 지원 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c28efd8106056ea900fef0cd57791837cf79e21a
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553233"
---
# <a name="microsoft-connector-for-oracle-data-type-support"></a>Microsoft Connector for Oracle 데이터 형식 지원

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Oracle용 SSIS 구성 요소가 모든 Oracle 데이터 형식을 지원하는 것은 아닙니다. 지원되지 않는 데이터 형식이 있는 열은 SSDT에서 패키지를 디자인할 때 경고를 발생하며 매핑 열에서 삭제됩니다. 지원되지 않는 데이터 형식의 열에는 데이터를 로드할 수 없습니다.

## <a name="data-type-mapping"></a>데이터 형식 매핑

다음 표에서는 Oracle 데이터베이스 데이터 형식과 SSIS 데이터 형식에 대한 기본 매핑을 보여 줍니다. 또한 지원되지 않는 Oracle 데이터 형식도 나와 있습니다.

|Oracle 데이터베이스 데이터 형식|SSIS 데이터 형식|주석|
|:-|:-|:-|
|VARCHAR2|DT_STR||
|NVARCHAR2|DT_WSTR||
|CHAR|DT_STR||
|NUMBER|DT_R8|특정 전체 자릿수 및 소수 자릿수를 사용하여 DT_NUMERIC으로 변경할 수 있습니다. 전체 자릿수와 소수 자릿수는 필요에 따라 사용자가 정의합니다. 출력의 열 데이터는 고정 전체 자릿수 및 소수 자릿수를 갖는 숫자로 표시됩니다.|
|NUMBER(P, S)| 소수 자릿수가 0이면 전체 자릿수(P)에 따라 다음과 같이 지정됩니다. <li> DT_I1 <Li> DT_I2 <Li> DT_I4 <Li> DT_NUMBERIC(P,0)||
||DT_NUMERIC(P,S)||
|DATE|DT_DBTIMESTAMP||
|<li>timestamp <li>TIMESTAMP WITH TIME ZONE <li>INTERVAL YEAR TO MONTH <li>INTERVAL DAY TO SECOND <li>TIMESTAMP WITH LOCAL TIME ZONE|DT_STR||
|RAW|DT_BYTES||
|CLOB|DT_TEXT|CLOB, NCLOB 및 BLOB 데이터 형식은 배열 모드에서만 지원되고 빠른 로드 모드에서는 지원되지 않습니다.|
|NCLOB|DT_NTEXT||
|BLOB|DT_IMAGE||
|UROWID|지원되지 않음||
|REF|지원되지 않음||
|BFILE|지원되지 않음||
|LONG|지원되지 않음||
|LONG RAW|지원되지 않음||
|ROWID|지원되지 않음||
|사용자 정의 형식(개체 형식, VARRAY, 중첩 테이블)|지원되지 않음||

## <a name="next-steps"></a>다음 단계

- [Oracle 연결 관리자](oracle-connection-manager.md)를 구성합니다.
- [Oracle 원본](oracle-source.md)을 구성합니다.
- [Oracle 대상](oracle-destination.md)을 구성합니다.
- 질문이 있는 경우 [TechCommunity](https://aka.ms/AA5u35j)을 방문하세요.
