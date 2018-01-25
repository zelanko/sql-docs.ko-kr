---
title: "외부 파일 형식 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab389a5c811f915ff497057a5daf12374f1cedb7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-file-format-transact-sql"></a>외부 파일 형식 (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Hadoop, Azure blob 저장소 또는 Azure 데이터 레이크 저장소에 저장 된 외부 데이터용 PolyBase 외부 파일 형식 정을 만듭니다. 외부 파일 형식 만들기 PolyBase 외부 테이블을 만들기 위한 필수 구성 요소입니다. 외부 파일 형식을 만들어서 여 외부 테이블이 참조 하는 데이터의 실제 레이아웃을 지정 합니다.  
  
 PolyBase는 다음 파일 형식을 지원합니다.
  
-   구분 기호로 분리 된 텍스트  
  
-   하이브 RCFile  
  
-   ORC 하이브
  
-   Parquet  
  
 외부 테이블을 만들려면 참조 [외부 테이블 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-table-transact-sql.md).
  
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
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>인수  
 *file_format_name*  
 외부 파일 형식에 대 한 이름을 지정합니다.
  
 FORMAT_TYPE 외부 데이터의 형식을 지정합니다.
  
 PARQUET은 Parquet 형식을 지정합니다.
  
 ORC  
 최적화 된 행 열 형식 (ORC) 형식을 지정합니다. 이 옵션에는 버전 이상 0.11 외부 Hadoop 클러스터에서 하이브가 필요합니다. Hadoop, ORC 파일 형식에서는 RCFILE 파일 형식 보다 더 나은 성능과 압축을 제공합니다.
  
 RCFILE (SERDE_METHOD 함께에서 = *SERDE_method*)를 레코드 열 파일 형식 (RcFile)를 지정 합니다. 이 옵션을 사용 하면 Serializer 하이브 및 (SerDe) 역직렬 변환기 메서드를 지정 해야 합니다. RC 파일을 쿼리할 Hadoop에서 하이브/HiveQL을 사용 하는 경우이 요구 사항은 같습니다. SerDe method는 대/소문자 구분 합니다.
  
 PolyBase는 두 SerDe 메서드를 사용 하 여 RCFile 지정의 예제입니다.
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'
  
 에서는 DELIMITEDTEXT 지정, 열 구분 기호를 사용 하는 텍스트 형식 라고도 필드 종결자입니다.
  
 FIELD_TERMINATOR = *field_terminator* 구분 기호로 분리 된 텍스트 파일에만 적용 됩니다. 에 필드 종결자가 오는 텍스트 구분 파일의 각 필드 (열)의 끝을 표시 하는 하나 이상의 문자를 지정 합니다. 기본값은 파이프 문자 ꞌ | ꞌ 합니다. 보장 된 지원에 대 한 하나 이상의 ascii 문자를 사용 하는 것이 좋습니다.
  
  
 예:  
  
-   FIELD_TERMINATOR = ' |'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR ꞌ\tꞌ =  
  
-   FIELD_TERMINATOR = '~|~'  
  
 STRING_DELIMITER = *string_delimiter*  
 텍스트 구분 파일에 형식 문자열의 데이터에 대 한 필드 종결자를 지정합니다. 문자열 구분 기호 길이에 하나 이상의 문자 이며 작은따옴표로 묶여 있습니다. 기본값은 빈 문자열 ""입니다. 보장 된 지원에 대 한 하나 이상의 ascii 문자를 사용 하는 것이 좋습니다.
 
  
 예:  

-   STRING_DELIMITER = ' "'

-   STRING_DELIMITER 큰따옴표 16 진수 ' 0x22' =
  
-   STRING_DELIMITER = ' *'  
  
-   STRING_DELIMITER = ꞌ,ꞌ  
  
-   STRING_DELIMITER 두 물결표 ' 0x7E0x7E'-= (예를 들어 ~ ~)
  
 날짜\_형식 = *datetime_format* 구분 기호로 분리 된 텍스트 파일에 표시 될 수 있는 모든 날짜 및 시간 데이터에 대 한 사용자 지정 형식을 지정 합니다. 기본 날짜/시간 형식을 사용 하는 소스 파일,이 옵션은 필요 하지 않습니다. 파일 당 하나의 사용자 지정 날짜/시간 형식이 허용 됩니다. 각 파일에 대해 여러 사용자 지정 날짜/시간 형식을 지정할 수 없습니다. 그러나 각 값은 외부 테이블 정의 각 데이터 형식에 대 한 기본 형식 하는 경우 여러 가지 날짜/시간 형식으로 사용할 수 있습니다.

PolyBase는 데이터를 가져오기 위한 사용자 지정 날짜 형식을 사용 합니다. 외부 파일에 데이터를 쓰기 위한 사용자 지정 형식을 사용 하지 않습니다.

 DATE_FORMAT 지정 하지 않으면 이거나 빈 문자열인 경우 PolyBase 다음과 같은 기본 형식을 사용 합니다.
  
-   날짜/시간: ' yyyy-월-일 h:mm: ss '  
  
-   SmallDateTime: ' yyyy-월-일 hh: mm '  
  
-   날짜: ' yyyy-월-일 '  
  
-   DateTime2: ' yyyy-월-일 h:mm: ss '  
  
-   DateTimeOffset: 'yyyy-MM-dd HH:mm:ss'  
  
-   시간: ' h:mm: ss '  
  
 **날짜 형식 예** 다음 테이블에 있습니다.  
  
 테이블에 대 한 참고 사항:  
  
-   연도, 월 및 일에 다양 한 형식 및 orders를 가질 수 있습니다. 이 표에는 **ymd** 형식입니다. 월 숫자 1, 2 또는 3 자에 있을 수 있습니다. 하루 1 개 또는 2 자리를 가질 수 있습니다. 연도 2 또는 4 자리를 가질 수 있습니다.
  
-   밀리초 (fffffff) 필요 하지 않습니다.
  
-   Am, pm (tt) 필요 하지 않습니다. 기본값은 오전입니다.
  
|날짜 형식|예제|Description|  
|---------------|-------------|-----------------|  
|과 같이 지원되는|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fff'|년, 월, 일, 외에도이 날짜 형식 포함 00-24 시간, 00-59 00-59 분 초 및 밀리초에 대 한 3 자리 숫자입니다.|  
|과 같이 지원되는|DATE_FORMAT 'yyyy-월-일 hh:mm:ss.ffftt' =|년, 월, 일, 외에도이 날짜 형식 포함 00-12 00-59 시간 동안 00-59 분 초, 밀리초 및 AM, 3 자리 숫자 am, PM, 또는 pm입니다. |  
|SmallDateTime|DATE_FORMAT ' yyyy-월-일 hh: mm ' =|연도, 월 및 일, 외에도이 날짜 형식 포함 00-23 시간, 00-59 분입니다.|  
|SmallDateTime|DATE_FORMAT 'yyyy-월-일 hh:mmtt' =|연도, 월 및 일, 외에도이 날짜 형식에 00-11 포함 시간, 00-59 분 없습니다 초 및 AM, am, PM, 또는 pm입니다.|  
|날짜|DATE_FORMAT =  'yyyy-MM-dd'|연도, 월 및 일 합니다. 시간 요소가 포함 됩니다.|  
|날짜|DATE_FORMAT = 'yyyy-MMM-dd'|연도, 월 및 일 합니다. 월을 3 분으로 지정 하는 경우 한 개 또는 1 월, 2 월, 3 월, 일, 년 5 월, 6 월, 년 7 월, 년 9 월, 년 10 월, 년 11 월, 또는 년 12 월 8 문자열 입력된 값이 있습니다.|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff'|연도, 월 및 일, 외에도이 날짜 형식 포함 00-23 시간, 00-59 00-59 분 초 및 밀리초에 대 한 7 자리입니다.|  
|datetime2|DATE_FORMAT 'yyyy-월-일 hh:mm:ss.ffffffftt' =|연도, 월 및 일, 외에도이 날짜 형식에 00-11 포함 00-59 시간 동안 00-59 분 초, 밀리초 및 AM에 대 한 7 자리 am, PM, 또는 pm입니다.|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff zzz'|연도, 월 및 일, 외에도이 날짜 형식 포함 00-23 시간, 00-59 00-59 분 초와 밀리초 및 표준 시간대 오프셋으로 입력된 파일에 배치할 수 있는 대 한 7 자리 `{+&#124;-}HH:ss`합니다. 예를 들어-08의 값을 UTC 보다 8 시간은 절약 일광 없이 로스앤젤레스 시간 이후: 입력된 파일에 00 로스앤젤레스에 대 한 표준 시간대를 지정 합니다.|  
|DateTimeOffset|DATE_FORMAT 'yyyy-월-일 hh:mm:ss.ffffffftt zzz' =|연도, 월 및 일, 이외에이 날짜 형식에는 00-11이 포함 되어 00-59 시간 동안 분 00-59 초, 밀리초, (AM, 오전, 오후 또는 pm)에 대 한 7 개의 자릿수 및 표준 시간대 오프셋 합니다. 이전 행의 설명을 참조 하십시오.|  
|Time|DATE_FORMAT = 'HH:mm:ss'|값이 없는 날짜만 00-23 시간, 00-59 분 및 00-59 초입니다.|  
  
 모든 지원 되는 날짜 형식:
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
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
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 상세 정보:  
  
-   월, 일 및 연도 값을 구분 하려면 사용할 수 있습니다 '-', '/' 또는 '. '. 간단히 하기 위해 테이블만 '-' 구분 기호를 사용합니다.
  
-   월 텍스트를 지정 하려면 3 개 이상의 문자를 사용 합니다. 달은 1 또는 2 바이트 문자를 숫자로 해석 됩니다.
  
-   시간 값을 구분 하려면 사용 된 ': ' 기호입니다.
  
-   대괄호로 묶인 문자는 선택 사항입니다.
  
-   문자 'tt' 지정 [AM | 오후 | am | pm]. AM 값이 기본값입니다. 'Tt'를 지정 시간 (hh) 값 0 ~ 12의 범위에 있어야 합니다.
  
-   문자 'zzz' 지정할 형식에서 시스템의 현재 표준 시간대에 대 한 표준 시간대 오프셋 {+ |-} HH:ss].
  
 USE_TYPE_DEFAULT = {TRUE | **FALSE** } PolyBase 텍스트 파일에서 데이터를 검색 하는 경우 분리 된 텍스트 파일에서 누락 값을 처리 하는 방법을 지정 합니다.
  
 외부 테이블 정의에 있는 해당 열의 데이터 형식에 대 한 기본값을 사용 하 여 각 누락 값을 저장 하는 텍스트 파일에서 데이터를 검색 하는 경우 TRUE입니다. 예를 들어, 누락 된 값을으로 바꿉니다.  
  
-   열이 숫자 열으로 정의 하는 경우 0입니다.
  
-   빈 문자열 "" 열은 문자열 열이 있습니다.
  
-   1900-01-01 열 날짜 열이 있습니다.
  
 NULL로 값이 누락 된 모든 FALSE 저장 합니다. 'NULL' 문자열로 구분 된 텍스트 파일에 단어 NULL을 사용 하 여 저장 되어 있는 모든 NULL 값을 가져옵니다.
  
   인코딩 = {'UTF8' | 'UTF16'}에서 Azure SQL 데이터 웨어하우스, PolyBase UTF8 및 UTF16 LE 인코딩된 구분 된 텍스트 파일을 읽을 수 있습니다. SQL Server 및 PDW의 PolyBase 지원 하지 않습니다 UTF16 읽는 파일 인코딩.
  
 DATA_COMPRESSION = *data_compression_method* 외부 데이터에 대 한 데이터 압축 방법을 지정 합니다. DATA_COMPRESSION을 지정 하지 않으면 기본값은 압축 되지 않은 데이터입니다.
 제대로 작동 하려면, Gzip 압축 파일에는 ".gz" 파일 확장명이 있어야 합니다.
 
 에서는 DELIMITEDTEXT 형식 유형 이러한 압축 메서드를 지원합니다.
  
-   데이터 압축 'org.apache.hadoop.io.compress.DefaultCodec' =
  
-   데이터 압축 'org.apache.hadoop.io.compress.GzipCodec' =

 RCFILE 형식 유형은이 압축 메서드를 지원합니다.
  
-   데이터 압축 'org.apache.hadoop.io.compress.DefaultCodec' =
  
 ORC 파일 형식 유형 이러한 압축 메서드를 지원합니다.
  
-   데이터 압축 'org.apache.hadoop.io.compress.DefaultCodec' =
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 PARQUET 파일 형식 유형에서는 다음 압축 방법을 지원합니다.
  
-   데이터 압축 'org.apache.hadoop.io.compress.GzipCodec' =
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>Permissions  
 ANY EXTERNAL FILE FORMAT ALTER 권한이 필요합니다.
  
## <a name="general-remarks"></a>일반적인 주의 사항
 외부 파일 형식은 데이터베이스 범위에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. 서버 범위에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
 형식 옵션은 모두 선택적 항목 및 구분 기호로 분리 된 텍스트 파일에만 적용 합니다.  
  
 데이터는 압축 된 형식 중 하나에 저장 되어, PolyBase 데이터 레코드를 반환 하기 전에 데이터의 먼저 압축 합니다.
  
## <a name="limitations-and-restrictions"></a>제한 사항
  
 구분 된 텍스트 파일에서 행 구분 기호는 Hadoop의 LineRecordReader에서 지원 되어야 합니다. 즉, '\r', '\n' 또는 '\r\n' 이어야 합니다. 이러한 구분 기호는 사용자가 구성할 수 없습니다.
  
 RCFiles, 포함 SerDe 메서드를 지원 되는 조합 및 지원 되는 데이터 압축 방법은이 문서의 이전에 나열 됩니다. 모든 조합은 사용할 수 있습니다.
  
 최대 동시 PolyBase 쿼리는 32입니다. 32 동시 쿼리를 실행 하는 각 쿼리 33,000 파일의 최대는 외부 파일 위치에서 읽을 수 있습니다. 루트 폴더 및 각 하위 폴더는 파일으로 계산 합니다. 동시성 수준을 32 보다 작은 경우, 외부 파일 위치 33,000 개 이상의 파일을 포함할 수 있습니다.
  
 외부 테이블에 있는 파일의 수에 제한 때문에 루트 및 외부 파일 위치의 하위 폴더에 30, 000 보다 작은 파일을 저장 하는 것이 좋습니다. 또한 적은 수의 루트 디렉터리의 하위 폴더의 수를 유지 하는 것이 좋습니다. 너무 많은 파일 참조 되는 Java 가상 컴퓨터 메모리 부족 예외가 발생할 수 있습니다.
  
  Hadoop 또는 PolyBase에서 데이터에 대해서만 통해 Azure Blob 저장소로 데이터 내보내기를 내보낼, CREATE EXTERNAL TABLE이 명령에 정의 된 대로 열 names(metadata) 없습니다.

## <a name="locking"></a>잠금  
 외부 파일 형식 개체에 대 한 공유 잠금을 사용합니다.
  
## <a name="performance"></a>성능
 압축 된 파일을 사용 하면 항상 적은 양의 데이터를 압축 하 여 데이터 압축을 풀 CPU 사용량을 증가 시키는 동시 외부 데이터 원본 및 SQL Server 간 전송 사이 적절히 조정 함께 제공 됩니다.
  
 Gzip 압축 된 텍스트 파일 분할 가능한 되지 않습니다. Gzip 압축 된 텍스트 파일에 대 한 성능 향상을 위해 외부 데이터 원본 내에서 동일한 디렉터리에 저장 된 여러 개의 파일을 생성 하는 것이 좋습니다. 따라서 PolyBase를 읽고 여러 판독기 및 압축 풀기 프로세스를 사용 하 여 더 빠른 데이터 압축을 풀 수 있습니다. 압축 된 파일의 이상적인 수는 계산 노드 당 데이터 판독기 프로세스의 최대 수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 데이터 판독기 프로세스의 최대 수는 현재 릴리스에서 노드당 8입니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 노드당 데이터 판독기 프로세스의 최대 수 SLO에 따라 다릅니다. 참조 [패턴 및 전략을 로드 하는 Azure SQL 데이터 웨어하우스](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) 대 한 자세한 내용은 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>1. 에서는 DELIMITEDTEXT 외부 파일 형식 만들기  
 이 예제에서는 명명 된 외부 파일 형식 *textdelimited1* 텍스트 구분 파일에 대 한 합니다. 형식에 대 한 이러한 옵션은 나열\_옵션 지정을 파일의 필드 구분 하도록 파이프 문자를 사용 하 여 ' |'입니다. 텍스트 파일은 또한 Gzip 코덱을 사용 하 여 압축 됩니다. 하는 경우 데이터\_압축을 지정 하지 않으면, 텍스트 파일을 압축 합니다.
  
 구분 기호로 분리 된 텍스트 파일에 대 한 데이터 압축 방법을 수 기본 코덱, 'org.apache.hadoop.io.compress.DefaultCodec' 또는 Gzip 코덱 'org.apache.hadoop.io.compress.GzipCodec'.
  
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
 이 예제에서는 serialization/deserialization 메서드 org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe를 사용 하는 RCFile 외부 파일 형식 또한 데이터 압축 방법에 대 한 기본 코덱을 사용 하도록 지정 합니다. DATA_COMPRESSION을 지정 하지 않으면 기본값은 압축 되지 않습니다.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>3. ORC 외부 파일 형식 만들기  
 이 예제 데이터 사용 하 여 org.apache.io.compress.SnappyCodec 압축 데이터를 압축 하는 ORC 파일에 대 한 외부 파일 형식을 만듭니다. DATA_COMPRESSION을 지정 하지 않으면 기본값은 압축 되지 않습니다.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>4. PARQUET 외부 파일 형식 만들기  
 이 예제 데이터 사용 하 여 org.apache.io.compress.SnappyCodec 압축 데이터를 압축 하는 Parquet 파일에 대 한 외부 파일 형식을 만듭니다. DATA_COMPRESSION을 지정 하지 않으면 기본값은 압축 되지 않습니다.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>관련 항목:
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [외부 TABLE AS SELECT &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [TABLE AS SELECT &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
