---
title: CREATE EXTERNAL FILE FORMAT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 2/20/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 790c3bdce51c2359a9cc34aad4a51b4b2f199fd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-external-file-format-transact-sql"></a>CREATE EXTERNAL FILE FORMAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Hadoop, Azure Blob Storage, 또는 Azure Data Lake Store에 저장된 외부 데이터를 정의하는 외부 파일 형식 개체를 만듭니다. 외부 파일 형식 만들기는 외부 테이블을 만들기 위한 필수 구성 요소입니다. 외부 파일 형식을 만들어 외부 테이블에서 참조하는 데이터의 실제 레이아웃을 지정하게 됩니다.  
  
 PolyBase는 다음 파일 형식을 지원합니다.
  
-   구분 기호로 분리된 텍스트  
  
-   Hive RCFile  
  
-   Hive ORC
  
-   Parquet  
  
외부 테이블을 만들려면 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)을 참조하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문
  
```
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter 
    | First_Row = integer -- ONLY AVAILABLE SQL DW
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>인수  
 *file_format_name*  
 외부 파일 형식의 이름을 지정합니다.
  
 FORMAT_TYPE = [ PARQUET | ORC | RCFILE | PARQUET] 외부 데이터 형식을 지정합니다.
  
   -   PARQUET Parquet 형식을 지정합니다.
  
   -   ORC  
   ORC(최적화된 행 열 형식) 형식을 지정합니다. 이 옵션에는 버전 이상 0.11 외부 Hadoop 클러스터에서 하이브가 필요합니다. Hadoop에서는 ORC 파일 형식이RCFILE 파일 형식보다 압축과 성능이 더 낫습니다.

   -   RCFILE(SERDE_METHOD = *SERDE_method*와 함께) RcFile(Record Columnar file) 형식을 지정합니다. 이 옵션을 사용하려면 Hive 직렬 변환기와 역직렬화 변환기(SerDe) 메서드를 지정해야 합니다. Hadoop에서 Hive/HiveQL을 사용하여 RC 파일을 쿼리할 때도 요구 사항은 같습니다. SerDe 메서드는 대소문자를 구분합니다.

   PolyBase가 지원하는 두 SerDe 메서드를 사용하여 RCFile을 지정하는 예제입니다.

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'

   -   DELIMITEDTEXT 필드 종결자라고도 하는 열 구분 기호가 있는 텍스트 형식을 만듭니다. 
  
 FIELD_TERMINATOR = *field_terminator*  
구분 기호로 분리된 텍스트 파일에만 적용됩니다. 필드 종결자는 구분 기호로 분리된 텍스트 파일의 각 필드(열)의 끝을 표시하는 하나 이상의 문자를 지정합니다. 기본값은 파이프 문자 |입니다. 지원 보장을 위해 하나 이상의 ASCII 문자를 사용하는 것이 좋습니다.
  
  
 예:  
  
-   FIELD_TERMINATOR = '|'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = \t  
  
-   FIELD_TERMINATOR = '~|~'  
  
 STRING_DELIMITER = *string_delimiter*  
구분 기호로 분리된 텍스트 파일에 형식 문자열의 데이터에 대한 필드 종결자를 지정합니다. 문자열 구분 기호는 길이가 한 자 이상이며 작은따옴표로 묶입니다. 기본값은 빈 문자열 ""입니다. 지원 보장을 위해 하나 이상의 ASCII 문자를 사용하는 것이 좋습니다.
 
  
 예:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22' -- 큰따옴표의 16진수
  
-   STRING_DELIMITER = '*'  
  
-   STRING_DELIMITER = ,  
  
-   STRING_DELIMITER = '0x7E0x7E'  -- 물결표 두 개(예: ~~)
 
 FIRST_ROW = *First_row_int*  
PolyBase 로드 중에 모든 파일에서 첫 번째로 읽을 행 번호를 지정합니다. 이 매개 변수 값은 1-15를 사용할 수 있습니다. 값이 2로 설정되면 데이터를 로드할 때 모든 파일의 첫 행(헤더 행)을 건너뜁니다. 행은 행 종결자(/r/n, /r, /n)의 존재를 기준으로 건너뜁니다. 내보내기에 대해 이 옵션을 사용하면 데이터 손실 없이 파일을 읽을 수 있도록 하기 위해 데이터 행이 추가됩니다. 2 미만으로 값을 설정하면 내보낸 첫 행이 외부 테이블의 열 이름이 됩니다.

 DATE\_FORMAT = *datetime_format*  
구분 기호로 분리된 텍스트 파일에 표시될 수 있는 모든 날짜 및 시간 데이터에 대한 사용자 지정 형식을 지정합니다. 원본 파일이 기본 날짜/시간 형식을 사용할 경우 이 옵션이 필요하지 않습니다. 파일당 하나의 사용자 지정 날짜/시간 형식이 허용됩니다. 한 파일에 대해 여러 사용자 지정 날짜/시간 형식을 지정할 수 없습니다. 그러나 외부 테이블 정의에서 각각의 형식이 해당 데이터 형식에 대한 기본 형식인 경우 여러 날짜/시간 형식을 사용할 수 있습니다.

PolyBase는 데이터를 가져오기 위해서만 사용자 지정 날짜 형식을 사용합니다. 외부 파일에 데이터를 쓰는 데는 사용자 지정 형식을 사용하지 않습니다.

 DATE_FORMAT을 지정하지 않았거나 빈 문자열인 경우 PolyBase는 다음 기본 형식을 사용합니다.
  
-   DateTime: 'yyyy-MM-dd HH:mm:ss'  
  
-   SmallDateTime: 'yyyy-MM-dd HH:mm'  
  
-   Date: 'yyyy-MM-dd'  
  
-   DateTime2: 'yyyy-MM-dd HH:mm:ss'  
  
-   DateTimeOffset: 'yyyy-MM-dd HH:mm:ss'  
  
-   Time: 'HH:mm:ss'  
  
**날짜 형식 예**는 다음 표에 있습니다.
  
테이블 관련 참고 사항  
  
-   연도, 월, 일의 형식과 순서는 다양합니다. 이 표는 **ymd** 형식만 나타냅니다. 월은 1-2자리 숫자 또는 3자 문자가 될 수 있습니다. 일은 1-2자리 숫자가 될 수 있습니다. 연도는 2-4자리 숫자가 될 수 있습니다.
  
-   밀리초(fffffff)는 필요하지 않습니다.
  
-   Am, pm(tt)은 필요하지 않습니다. 기본값은 AM입니다.
  
|날짜 형식|예제|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fff'|이 날짜 형식은 연도, 월, 일 외에도 00-24시간, 00-59분, 00-59초, 3자리 밀리초를 포함합니다.|  
|DateTime|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffftt'|이 날짜 형식은 연도, 월, 일 외에도 00-12시간, 00-59분, 00-59초, 3자리 밀리초와, AM, am, PM, 또는 pm을 포함합니다. |  
|SmallDateTime|DATE_FORMAT =  'yyyy-MM-dd HH:mm'|이 날짜 형식은 연도, 월, 일 외에도 00-23시간, 00-59분을 포함합니다.|  
|SmallDateTime|DATE_FORMAT =  'yyyy-MM-dd hh:mmtt'|이 날짜 형식은 연도, 월, 일 외에도 00-11시간 및 00-59분(초 없음)과, AM, am, PM 또는 pm을 포함합니다.|  
|date|DATE_FORMAT =  'yyyy-MM-dd'|연도, 월, 일. 시간 요소가 포함되지 않습니다.|  
|date|DATE_FORMAT = 'yyyy-MMM-dd'|연도, 월, 일. 월을 3 M으로 지정하면 입력 값은 Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov 또는 Dec 문자열 중 하나입니다.|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff'|이 날짜 형식은 연도, 월, 일 외에도 00-23시간, 00-59분, 00-59초, 7자리 밀리초를 포함합니다.|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffffffftt'|이 날짜 형식은 연도, 월, 일 외에도 00-11시간, 00-59분, 00-59초, 7자리 밀리초와, AM, am, PM, 또는 pm을 포함합니다.|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff zzz'|이 날짜 형식은 연도, 월, 일 외에도 00-23시간, 00-59분, 00-59초, 7자리 밀리초와, 입력 파일에 `{+&#124;-}HH:ss`로 입력한 시간대 오프셋을 포함합니다.  예를 들어, 일광절약시간이 적용되지 않은 로스엔젤레스는 UTC보다 8시간 늦으므로 입력 파일에서 -08:00 값으로 로스엔젤레스의 시간대를 지정합니다.|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffffffftt zzz'|이 날짜 형식은 연도, 월, 일 외에도 00-11시간, 00-59분, 00-59초, 7자리 밀리초, (AM, am, PM, 또는 pm) 및 시간대 오프셋을 포함합니다. 이전 행의 설명을 참조하세요.|  
|Time|DATE_FORMAT = 'HH:mm:ss'|날짜 값이 없고 00-23시간, 00-59분, 00-59초만 있습니다.|  
  
 지원되는 모든 날짜 형식:
  
|DATETIME|smalldatetime|날짜|Datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 상세 정보:  
  
-   월, 일 및 연도 값을 구분하기 위해 '-', '/' 또는 '.'를 사용할 수 있습니다. 간단히 하기 위해 테이 표에서는 '-' 구분 기호만 사용합니다.
  
-   월을 텍스트로 지정하려면 3자 이상의 문자를 사용합니다. 한두 자로 지정한 문자는 숫자로 해석합니다.
  
-   시간 값을 구분하기 위해 ':' 기호를 사용합니다.
  
-   대괄호 안에 있는 문자는 선택 사항입니다.
  
-   'tt' 문자는 [AM|PM|am|pm]을 지정합니다. 기본값은 AM입니다. 'tt'를 지정한 경우 시간 값(hh)은 0-12 범위여야 합니다.
  
-   'zzz' 문자는 {+|-}HH:ss] 형식으로 시스템의 현재 시간대에 대한 시간대 오프셋을 지정합니다.
  
 USE_TYPE_DEFAULT = { TRUE | **FALSE** }  
 PolyBase는 구분 기호로 분리된 텍스트 파일에서 데이터를 검색 하는 경우 분리 된 텍스트 파일에서 누락 값을 처리 하는 방법을 지정 합니다.
  
 TRUE  
 텍스트 파일에서 데이터를 검색할 때 외부 테이블 정의에서 해당하는 열의 데이터 형식에 대한 기본값을 사용하여 누락된 각 값을 저장합니다. 예를 들어, 누락된 값을 다음으로 바꿉니다.  
  
-   열이 숫자 열로 정의되었으면 0
  
-   열이 문자열이면 빈 문자열 "" 
  
-   열이 날짜 열이면 1900-01-01
  
 FALSE  
 모든 누락 값을 NULL로 저장합니다. 구분 기호로 분리된 텍스트 파일에서 NULL이라는 단어를 사용하여 저장된 모든 NULL 값은 문자열 'NULL'로 가져옵니다.
  
   Encoding = {'UTF8' | 'UTF16'}  
 Azure SQL Data Warehouse에서 PolyBase은 UTF8 및 UTF16-LE로 인코딩된 구분 기호로 분리된 텍스트 파일을 읽을 수 있습니다. SQL Server 및 PDW에서는 PolyBase가 UTF16 인코딩 파일 읽기를 지원하지 않습니다.
  
 DATA_COMPRESSION = *data_compression_method*  
 외부 파일의 데이터에 대한 데이터 압축 메서드를 지정합니다. DATA_COMPRESSION을 지정하지 않은 경우 압축되지 않는 데이터가 기본값입니다.
 제대로 작동하려면 Gzip 압축 파일에 ".gz" 파일 확장명이 있어야 합니다.
 
 DELIMITEDTEXT 형식 유형은 다음과 같은 압축 메서드를 지원합니다.
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 RCFILE 형식 유형은 다음 압축 메서드를 지원합니다.
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 ORC 파일 형식 유형은 다음 압축 메서드를 지원합니다.
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 PARQUET 파일 형식 유형은 다음 압축 메서드를 지원합니다.
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY EXTERNAL FILE FORMAT 권한이 필요합니다.
  
## <a name="general-remarks"></a>일반적인 주의 사항
 외부 파일 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 데이터베이스 범위입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서는 서버 범위입니다.  
  
 형식 옵션은 모두 선택 사항이며 구분 기호로 분리된 텍스트 파일에만 적용됩니다.  
  
 데이터가 압축된 형식 중 하나로 저장될 때 PolyBase는 데이터 레코드를 반환하기 전에 먼저 데이터의 압축을 풉니다.
  
## <a name="limitations-and-restrictions"></a>제한 사항
  
 구분 기호로 분리된 텍스트 파일의 행 구분 기호는 Hadoop의 LineRecordReader에서 지원되어야 합니다. 즉 '\r', '\n' 또는 '\r\n'이어야 합니다. 이러한 구분 기호는 사용자가 구성할 수 없습니다.
  
 지원되는 SerDe 메서드와 RCFile 조합 및 지원되는 데이터 압축 메서드 목록은 이 문서의 앞 부분에 있습니다. 일부 조합은 지원되지 않습니다.
  
 동시 PolyBase 쿼리의 최대 수는 32개입니다. 32개 쿼리가 동시에 실행되면 각 쿼리가 외부 파일 위치에서 최대 33,000개의 파일을 읽을 수 있습니다. 루트 폴더 및 각 하위 폴더도 한 파일로 계산됩니다. 동시성 수준이 32 미만이면 외부 파일 위치에 33,000개 이상의 파일이 있을 수 있습니다.
  
 외부 테이블의 파일 수 제한 때문에 외부 파일 위치의 루트 및 하위 폴더에는 30,000개 미만의 파일을 저장하는 것이 좋습니다. 또한 루트 디렉터리 하의 하위 폴더 수는 적게 유지하는 것이 좋습니다. 너무 많은 파일이 참조되면 Java Virtual Machine 메모리 부족 예외가 발생할 수 있습니다.
  
  PolyBase를 통해 데이터를 Hadoop 또는 Azure Blob Storage로 내보낼 때 CREATE EXTERNAL TABLE 명령에서 정의된 열 이름(메타데이터)이 아닌 데이터만 내보내집니다.

## <a name="locking"></a>잠금  
 EXTERNAL FILE FORMAT 개체에 대해 공유 잠금을 적용합니다.
  
## <a name="performance"></a>성능
 압축 파일을 사용할 때는 항상 외부 데이터 원본과 SQL Server 간에 전송되는 데이터가 더 적다는 점과, 데이터 압축 및 압축 풀기를 위한 CPU 사용량이 증대한다는 점 사이의 상호 절충이 따릅니다.
  
 Gzip 압축 텍스트 파일은 분할할 수 없습니다. Gzip 압축 텍스트 파일의 성능을 높이기 위해 외부 데이터 원본 내에서 모두 동일한 디렉터리에 저장되는 여러 파일을 생성하는 ㄱ서이 좋습니다. 이 파일 구조를 통해 PolyBase가 여러 Reader 및 압축 풀기 프로세스를 사용하여 데이터를 더 빠르게 읽고 압축을 풀 수 있습니다. 이상적인 압축 파일의 수는 계산 노드당 최대 데이터 Reader 프로세스 수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 현재 릴리스의 데이터 Reader 프로세스의 최대 수는 노드당 8개입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 노드당 최대 데이터 Reader 프로세서 수는 SLO마다 다릅니다. 자세한 내용은 [Azure SQL Data Warehouse 로드 패턴 및 전략](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>1. DELIMITEDTEXT 외부 파일 형식 만들기  
 이 예제에서는 구분 기호로 분리된 텍스트 파일에 대해 이름이 *textdelimited1*인 외부 파일 형식을 만듭니다. FORMAT\_OPTIONS에 대해 나열된 옵션은 파일의 필드가 파이프 문자 '|'를 사용하여 구분되어야 함을 지정합니다. 또한 텍스트 파일은 Gzip 코덱을 사용하여 압축됩니다. DATA\_COMPRESSION을 지정하지 않은 경우 텍스트 파일이 압축되지 않습니다.
  
 구분 기호로 분리된 텍스트 파일의 경우 데이터 압축 메서드는 기본 코덱 'org.apache.hadoop.io.compress.DefaultCodec’ 또는 Gzip 코덱 'org.apache.hadoop.io.compress.GzipCodec'이 될 수 있습니다.
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>2. RCFile 외부 파일 형식 만들기  
 이 예제에서는 직렬화/역직렬화 메서드org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe를 사용하는 RCFile에 대한 외부 파일 형식을 만듭니다. 데이터 압축 메서드에 기본 코덱을 사용하도록 지정합니다. DATA_COMPRESSION을 지정하지 않은 경우 압축되지 않는 것이 기본값입니다.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>3. ORC 외부 파일 형식 만들기  
 이 예제에서는 org.apache.io.compress.SnappyCodec 압축 메서드를 사용하여 데이터를 압축하는 ORC 파일에 대한 외부 파일 형식을 만듭니다. DATA_COMPRESSION을 지정하지 않은 경우 압축되지 않는 것이 기본값입니다.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>4. PARQUET 외부 파일 형식 만들기  
 이 예제에서는 org.apache.io.compress.SnappyCodec 압축 메서드를 사용하여 데이터를 압축하는 Parquet 파일에 대한 외부 파일 형식을 만듭니다. DATA_COMPRESSION을 지정하지 않은 경우 압축되지 않는 것이 기본값입니다.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
### <a name="e-create-a-delimited-text-file-skipping-header-row-azure-sql-dw-only"></a>5. 헤더 행을 건너뛰는 구분 기호로 분리된 텍스트 파일 만들기(Azure SQL DW만 해당)
 이 예제에서는 단일 헤더 행이 있는 CSV 파일에 대한 외부 파일 형식을 만듭니다. 
  
```  
CREATE EXTERNAL FILE FORMAT skipHeader_CSV
WITH (FORMAT_TYPE = DELIMITEDTEXT,
      FORMAT_OPTIONS(
          FIELD_TERMINATOR = ',',
          STRING_DELIMITER = '"',
          FIRST_ROW = 2, 
          USE_TYPE_DEFAULT = True)
)
```   

## <a name="see-also"></a>참고 항목
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT&#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
