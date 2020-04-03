---
title: PolyBase를 사용한 형식 매핑 | Microsoft Docs
description: 여기에 나와 있는 표에서 PolyBase 외부 데이터 원본과 SQL Server 사이의 매핑을 참조하세요. Transact-SQL CREATE EXTERNAL TABLE을 사용하여 외부 테이블 정의
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 9d4dd55daf26c9f927e23c0f269a084c711d0481
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80215750"
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
| tinyint       | Byte                      | tinyint        | ByteWritable          | 부호 없는 숫자의 경우만.     |
| smallint      | Int16                     | smallint       | ShortWritable         |
| int           | Int32                     | int            | IntWritable           |
| bigint        | Int64                     | bigint         | LongWritable          |
| bit           | 부울                   | boolean        | BooleanWritable       |
| float         | Double                    | double         | DoubleWritable        |
| real          | Single                    | float          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| smallmoney    | Decimal                   | double         | DoubleWritable        |
| nchar         | String<br /><br /> Char[] | 문자열         | Varchar               |
| nvarchar      | String<br /><br /> Char[] | 문자열         | Varchar               |
| char          | String<br /><br /> Char[] | 문자열         | Varchar               |
| varchar       | String<br /><br /> Char[] | 문자열         | Varchar               |
| binary        | Byte[]                    | binary         | BytesWritable         | Hive 0.8 이상에 적용됩니다. |
| varbinary     | Byte[]                    | binary         | BytesWritable         | Hive 0.8 이상에 적용됩니다. |
| date          | DateTime                  | timestamp      | TimestampWritable     |
| smalldatetime | DateTime                  | timestamp      | TimestampWritable     |
| datetime2     | DateTime                  | timestamp      | TimestampWritable     |
| Datetime      | DateTime                  | timestamp      | TimestampWritable     |
| time          | TimeSpan                  | timestamp      | TimestampWritable     |
| decimal       | Decimal                   | decimal        | BigDecimalWritable    | Hive 0.11 이상에 적용됩니다. |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Oracle 형식 매핑 참조

| Oracle 데이터 형식 | SQL Server 형식 | 
| -------------    | --------------- |
|Float             |Float            |
|NUMBER            |Decimal          |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |Float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

**형식 불일치** 

**Float:** Oracle은 SQL Server가 지원하는 정밀도(53)보다 낮은 126의 부동 소수점 정밀도를 지원합니다. 따라서 **Float (1-53)** 을 직접 매핑할 수 있지만 정밀도가 이보다 큰 경우 잘림으로 인해 데이터가 손실될 수 있습니다.

**타임스탬프:** Oracle의 Timestamp 및 로컬 표준 시간대가 적용되는 Timestamp는 소수 자릿수 초의 정밀도 9를 지원하지만 SQL Server DateTime2는 소수 자릿수 초의 정밀도 7만 지원합니다. 




## <a name="mongodb-type-mapping"></a>MongoDB 형식 매핑

| BSON 데이터 형식     | SQL Server 형식 |
| ------------------ | --------------- |
| Double             | Float           |
| String             | nvarchar        |
| 이진 데이터        | nvarchar        |
| 개체 ID입니다.          | nvarchar        |
| 부울            | bit             |
| Date               | Datetime2       |
| 32비트 정수     | Int             |
| 타임스탬프          | nvarchar        |
| 64비트 정수     | BigInt          |
|10진수 128         | Decimal         | 
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| 최대 키            | nvarchar        |
| 최소 키            | nvarchar        |
| 기호             | nvarchar        |
| 정규식 | nvarchar        |
| 미정의/NULL     | nvarchar        |


MongoDB는 BSON 문서를 사용하여 데이터 레코드를 저장합니다. 이전 시나리오와 달리 BSON은 스키마가 없으며 다른 문서 내에 문서와 배열 포함을 지원합니다. 이는 사용자에게 유연성을 제공합니다. 


## <a name="teradata-type-mapping-reference"></a>Teradata 형식 매핑 참조

| Teradata 데이터 형식 | SQL Server 형식 | 
| -------------      | -------------   |
|INTEGER             |Int              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |이진           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |Date             |
|timestamp           |Datetime2        |
|TIME                |Time             |
|TIME WITH TIME ZONE |Time             |
|TIMESTAMP WITH TIME ZONE|Time         |

::: moniker-end

## <a name="next-steps"></a>다음 단계

이 항목의 사용 방법에 대한 자세한 내용은 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)의 Transact-SQL 참조 문서를 참조하세요.
