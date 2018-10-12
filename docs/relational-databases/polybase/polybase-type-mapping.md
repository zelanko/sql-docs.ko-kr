---
title: PolyBase를 사용한 형식 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9839c46f477fe31d29214eed10dce0d673c9fd00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732611"
---
# <a name="type-mapping-with-polybase"></a>PolyBase를 사용한 형식 매핑

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 PolyBase 외부 데이터 원본 및 SQL Server 간 매핑을 설명합니다. 이 정보를 사용하여 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) Transact-SQL 명령을 사용하여 외부 테이블을 올바르게 정의할 수 있습니다.

## <a name="overview"></a>개요

PolyBase로 외부 테이블을 만들 때 데이터 형식 및 열 수를 포함하는 열 정의가 외부 파일의 데이터와 일치해야 합니다. 불일치가 있는 경우 실제 데이터를 쿼리할 때 파일 행이 거부됩니다.  
  
외부 데이터 원본의 파일을 참조하는 외부 테이블의 경우 열 및 형식 정의는 외부 파일의 정확한 스키마에 매핑해야 합니다. Hadoop/Hive에 저장된 데이터를 참조하는 데이터 형식을 정의하는 경우 SQL과 Hive 데이터 형식 간에 다음 매핑을 사용하고 그로부터 선택할 때 형식을 SQL 데이터 형식으로 캐스팅합니다. 형식은 달리 명시하지 않은 한 Hive의 모든 버전을 포함합니다.

> [!NOTE]  
> SQL Server는 어떤 변환에서도 Hive *무한대* 데이터 값을 지원하지 않습니다. PolyBase는 데이터 형식 변환 오류가 있으면 실패합니다.

## <a name="hadoop-type-mapping-reference"></a>Hadoop 형식 매핑 참조

| SQL 데이터 형식 | .NET 데이터 형식            | Hive 데이터 형식 | Hadoop/Java 데이터 형식 | 주석                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| TINYINT       | Byte                      | TINYINT        | ByteWritable          | 부호 없는 숫자의 경우만.     |
| SMALLINT      | Int16                     | SMALLINT       | ShortWritable         |
| ssNoversion           | Int32                     | ssNoversion            | IntWritable           |
| BIGINT        | Int64                     | BIGINT         | LongWritable          |
| bit           | Boolean                   | boolean        | BooleanWritable       |
| FLOAT         | Double                    | double         | DoubleWritable        |
| REAL          | 단일                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | String<br /><br /> Char[] | string         | text                  |
| NVARCHAR      | String<br /><br /> Char[] | string         | 텍스트 모드                  |
| char          | String<br /><br /> Char[] | string         | 텍스트 모드                  |
| varchar       | String<br /><br /> Char[] | string         | 텍스트 모드                  |
| BINARY        | Byte[]                    | BINARY         | BytesWritable         | Hive 0.8 이상에 적용됩니다. |
| varbinary     | Byte[]                    | BINARY         | BytesWritable         | Hive 0.8 이상에 적용됩니다. |
| 날짜          | DateTime                  | TIMESTAMP      | TimestampWritable     |
| smalldatetime | DateTime                  | TIMESTAMP      | TimestampWritable     |
| Datetime2     | DateTime                  | TIMESTAMP      | TimestampWritable     |
| DATETIME      | DateTime                  | TIMESTAMP      | TimestampWritable     |
| Time          | TimeSpan                  | TIMESTAMP      | TimestampWritable     |
| Decimal       | Decimal                   | Decimal        | BigDecimalWritable    | Hive 0.11 이상에 적용됩니다. |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Oracle 형식 매핑 참조

| Oracle 데이터 형식              | SQL Server 형식 |
| ----------------------------- | --------------- |
| float                         | float           |
| Decimal                       | Decimal         |
| 정수                           | 정수             |
| Long                          | Ntext           |
| Binary Float                  | Real            |
| Char                          | Nchar           |
| Varchar2                      | nvarchar        |
| Raw                           | Varbinary       |
| Long Raw                      | image           |
| Bfile                         | image           |
| Blob                          | image           |
| Clob                          | image           |
| Rowid                         | Varchar         |
| date                          | Datetime2       |
| 타임스탬프                     | Datetime2       |
| 로컬 표준 시간대가 적용되는 타임스탬프 | Datetime2       |

### <a name="type-mismatch-float"></a>형식 불일치(Float)

Oracle은 SQL Server가 지원하는 정밀도(53)보다 낮은 126의 부동 소수점 정밀도를 지원합니다. 따라서 **Float (1-53)** 을 직접 매핑할 수 있지만 정밀도가 이보다 큰 경우 잘림으로 인해 데이터가 손실될 수 있습니다.

### <a name="type-mismatch-character-types"></a>형식 불일치(문자 형식)

형식(예: **Long** 및 **Bfile**의 경우 Oracle은 4GB의 데이터 형식 크기를 지원합니다. SQL Server는 2GB 크기를 지원합니다. 마찬가지로, Oracle 데이터 형식 **Blob** 및 **clob**의 경우, Oracle은 최대 128TB를 지원할 수 있지만, SQL Server **LONGVARBINARY** 또는 **WLONGVARBINARY**는 2GB보다 큰 데이터를 지원할 수 없습니다. 2GB보다 큰 데이터 형식 크기를 매핑하면 데이터가 잘릴 수 있습니다.  

### <a name="type-mismatch-timestamp"></a>형식 불일치(타임스탬프)

Oracle의 **Timestamp** 및 **Timestamp with local timezone**은 소수 자릿수 9의 정밀도를 지원합니다. SQL Server DateTime2는 소수 자릿수 7의 정밀도를 지원합니다.

또한 Simba는 **Date**, **Timestamp** 및 **Timestamp with local zone**을 ODBC 형식 **SQL_TIMESTAMP**, 결과적으로는 SQL Server 형식 **Timestamp**에 매핑합니다. **Timestamp**는 자동으로 생성되는 고유 행 ID입니다. 이상적으로 **SQL_TIMESTAMP**는 SQL Server 형식 **DateTime/DateTime2** 또는 Oracle 형식 **Date**, **Timestamp** 및 **Timestamp with local zone**은 ODBC 형식 **SQL_TYPE_TIMESTAMP**에 매핑되어야 합니다.

### <a name="driver-configuration-option"></a>드라이버 구성 옵션

**Long/LOB** 열의 기본 버퍼 크기는 1,024KB(구성 가능)입니다.

## <a name="mongo-type-mapping-reference"></a>Mongo 형식 매핑 참조

| BSON 데이터 형식     | SQL Server 형식 |
| ------------------ | --------------- |
| Double             | float           |
| String             | nvarchar        |
| Object             |
| Array              |
| 이진 데이터        | nvarchar        |
| 개체 ID입니다.          | nvarchar        |
| Boolean            | bit             |
| date               | Datetime2       |
| 32비트 정수     | 정수             |
| 타임스탬프          | nvarchar        |
| 64비트 정수     | BigInt          |
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| 최대 키            | nvarchar        |
| 최소 키            | nvarchar        |
| 기호             | nvarchar        |
| 정규식 | nvarchar        |
| 미정의/NULL     | nvarchar        |

### <a name="javascript-with-scope"></a>Javascript(범위)

드라이버는 "범위가 있는 지원되지 않는 Javascript"를 포함하는 문자열로 값을 반환합니다.

### <a name="type-mismatch-string"></a>형식 불일치(문자열)

MongoDB 문자열은 기본 열 크기 255를 사용하여 **SQL_WVARCHAR** 형식으로 변환됩니다. 이 열 크기는 드라이버 구성의 일부로 조정 가능합니다. 구성 기능이 있지만, **SQL_WVARCHAR** 또는 SQL Server 형식 **Varchar**는 최대 2GB만 지원하고, MongoDB는 최대 4GB의 데이터를 포함할 수 있습니다. 이로 인해 데이터가 잘릴 수 있습니다.

### <a name="mongodb-driver-options"></a>MongoDB 드라이버 옵션

- **이중 버퍼링 사용**: 기본적으로 선택되어 있습니다.
- **블록당 가져올 문서 수**: 기본값은 4096입니다.
- **SQL_WVARCHAR로 문자열 공개**: 기본적으로 선택되어 있습니다. 이 옵션을 선택 취소하면 문자열은 SQL_VARCHAR로 공개됩니다.
- **문자열 열 크기**: 기본값은 255입니다.
- **SQL_LONGVARBINARY로 바이너리 공개**: 기본적으로 선택되어 있습니다. 이 옵션을 선택 취소하면 바이너리는 SQL_VARBINARY로 공개됩니다.
- **바이너리 열 크기**: 기본값은 32767입니다.
- **실행 사용**: 기본적으로 선택되어 있습니다.

### <a name="schema-related-driver-configurations"></a>스키마 관련 드라이버 구성

- **LoadMetadataTable**: 데이터베이스에서 기본값입니다. 드라이버에 지정된 JSON 파일에서 스키마 정의를 로드하도록 요청합니다.
- **LocalMetadataFile**: 파일에서 읽는 경우 전체 경로를 지정해야 합니다.
- **샘플링 방법**:  
  - **기본 앞으로**: 드라이버는 첫 번째 레코드부터 데이터를 샘플링합니다.
  - **뒤로**: 드라이버는 마지막 레코드부터 데이터를 샘플링합니다.
- **SamplingLimit**: 기본값은 100입니다(드라이버가 임시 스키마 정의를 생성하기 위해 샘플링할 수 있는 최대 레코드 수). 0으로 설정하는 경우 드라이버는 모든 문서를 샘플링합니다.
- **SamplingStepSize**: 기본값은 1입니다(임시 스키마 정의를 생성하기 위해 데이터베이스를 검색할 때 드라이버가 레코드를 샘플링하는 간격). 예를 들어, 2로 설정하면 데이터베이스의 레코드를 하나 걸러 샘플링합니다.

## <a name="teradata-type-mapping-reference"></a>Teradata 형식 매핑 참조

| Teradata 데이터 형식               | SQL Server 형식 |
| -------------------------------- | --------------- |
| 정수                              | 정수             |
| Small Int                        | SmallInt        |
| Big Int                          | BigInt          |
| Byte Int                         | TinyInt         |
| Decimal                          | Decimal         |
| float                            | float           |
| Byte                             | 이진          |
| Varbyte                          | Varbinary       |
| Blob                             | image           |
| Char                             | Nchar           |
| Clob                             | Ntext           |
| Varchar                          | nvarchar        |
| Graphic                          | Nchar           |
| JSON                             | Ntext           |
| Vargraphic                       | nvarchar        |
| date                             | date            |
| Time                             | Time            |
| Time with Time Zone              | Time            |
| 타임스탬프                        | Datetime2       |
| Interval Year                    |
| Interval year to month           |
| Interval Month                   |
| Interval Day                     |
| Interval Day to Hour             |
| Interval Day to Minute           |
| Interval Day to Second           |
| Interval Hour                    |
| Interval Hour to Minute          |
| Interval Hour to Second          |
| Interval Minute                  |
| Interval Minute to Second        |
| Interval Second                  |
| Period (DATE)                    |
| Period (TIME)                    |
| Period (TIME with Timezone)      |
| Period (Timestamp)               |
| Period (Timestamp with Timezone) |

### <a name="period-data-type"></a>Period data type

**Period** 데이터 형식은 시작 바인딩과 끝 바인딩으로 표시되는 기간을 나타냅니다. 기본적으로 튜플입니다. **Period**에 해당하는 SQL Server의 형식은 없습니다.

### <a name="time-with-time-zone-and-timestamp"></a>Time with Time Zone 및 Timestamp

**Time with Time Zone** 및 **Time with Timestamp**는 표준 시간대 오프셋을 포함합니다. 오프셋은 변환 중에 유실됩니다. **Time/DateTime2** 대신 **datetimeoffset**의 **SQL_Type_Time/SQL_Type_Timestamp**에 매핑하면 수정될 수 있습니다.

### <a name="byteint"></a>ByteInt

Simba는 0-255 사이의 값을 포함할 수 있는 Teradata 형식 **ByteInt**를 -127 ~ 127 사이의 값을 포함할 수 있는 **TinyInt**로 매핑합니다. 이로 인해 잘림이 발생할 수 있습니다.  

### <a name="clob"></a>CLOB

**LATIN** 문자 집합을 갖는 **CLOB** 데이터 형식은 2097088000자를 수락할 수 있어야 합니다. 그러나 1073741823을 초과하면 버퍼 크기가 음수가 됩니다.  

### <a name="driver-configuration-options"></a>드라이버 구성 옵션

- **TIMESTAMP** 매개 변수에 **DATE** 데이터를 사용합니다.
- 2.X 응용 프로그램에 대해 사용자 지정 카탈로그 모드를 사용하도록 설정합니다.
- **SQL_TIMESTAMP**의 **CREATE_PARAMS** 열에서 빈 문자열을 반환합니다.
- Max. **CHAR/VARCHAR** 길이를 32K로 반환합니다.

::: moniker-end

## <a name="next-steps"></a>다음 단계

이 항목의 사용 방법에 대한 자세한 내용은 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)의 Transact-SQL 참조 문서를 참조하세요.
