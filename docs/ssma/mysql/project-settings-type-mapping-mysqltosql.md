---
title: 프로젝트 설정 (형식 매핑) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e0a11a0b49589c3763b5af67623c9e819038c217
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713251"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>프로젝트 설정(형식 매핑)(MySQLToSQL)
형식 매핑 프로젝트 설정 SSMA 프로젝트에 대 한 기본 형식 매핑을 설정할 수 있습니다.  

형식 매핑은 프로젝트 설정 및 기본 프로젝트 설정 대화 상자에서 제공 됩니다.  
  
-   현재 프로젝트에 대 한 구성 옵션을 설정 하 여 프로젝트 설정 대화 상자를 사용 합니다. 형식 매핑을 설정 도구 메뉴에 액세스 하려면 프로젝트 설정을 선택 하 고 왼쪽된 창에서 형식 매핑 클릭 합니다.  
  
-   모든 프로젝트에 대 한 구성 옵션을 설정 하 여 기본 프로젝트 설정 대화 상자를 사용 합니다. 유형 매핑에 액세스 하려면 도구 메뉴에서 설정을 선택 기본 프로젝트 설정 선택 마이그레이션 프로젝트 형식은 설정을 볼 /에서 변경 하는 데 필요한 **마이그레이션 대상 버전** 드롭다운 하 고 누른 다음 유형 왼쪽된 창에서 매핑입니다.  
  
## <a name="options"></a>변수  
  
##### <a name="source-type"></a>원본 유형  
대상 데이터베이스의 데이터 형식에 매핑될 수 있는 MySQL 데이터 형식,입니다.  
  
##### <a name="target-type"></a>대상 유형  
대상 데이터베이스 데이터 형식 지정된 된 MySQL 데이터 형식입니다.  
  
##### <a name="add"></a>추가  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
##### <a name="edit"></a>편집  
매핑 목록에서 선택한 데이터 형식을 편집 하려면 클릭 합니다.  
  
##### <a name="remove"></a>제거  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
##### <a name="reset-to-default"></a>기본값으로 다시 설정  
형식 매핑 목록 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="type-mappings"></a>형식 매핑  
다음 표에서 원본 및 대상 데이터 형식 간의 기본 매핑을 보여 줍니다.  
  
|||  
|-|-|  
|**MySQL 데이터 형식**|**SQL Server 데이터 형식**|  
|BIGINT|BIGINT|  
|bigint[*..255]|BIGINT|  
|BINARY|binary[1]|  
|이진 [0..1]|binary[1]|  
|이진 [2..255]|binary[*]|  
|bit|binary[1]|  
|비트 [0..8]|binary[1]|  
|bit[17..24]|이진 파일 [3]|  
|비트 [25..32]|binary[4]|  
|bit[33..40]|binary[5]|  
|bit[41..48]|binary[6]|  
|bit[49..56]|binary[7]|  
|bit[57..64]|binary[8]|  
|비트 [9..16]|binary[2]|  
|blob|varbinary(max)|  
|blob [0..1]|varbinary[1]|  
|blob [2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar[1]|  
|char 바이트|binary[1]|  
|바이트 [0..1] char|binary[1]|  
|바이트 [2..255] char|binary[*]|  
|char [0..1]|nchar[1]|  
|char[2..255]|nchar[*]|  
|character|nchar[1]|  
|[0..1] 다양 한 문자|nvarchar[1]|  
|다양 한 [2..255] 문자|NVARCHAR|  
|문자 [0..1]|nchar[1]|  
|문자 [2..255]|nchar[*]|  
|날짜|날짜|  
|DATETIME|datetime2[0]|  
|dec|Decimal|  
|dec [*... 65]|decimal[*][0]|  
|dec[*..65][\*..30]|decimal[*][\*]|  
|Decimal|Decimal|  
|decimal [*... 65]|decimal[*][0]|  
|decimal[*..65][\*..30]|decimal[*][\*]|  
|double|float[53]|  
|배정밀도|float[53]|  
|배정밀도 [*... 255] [\*... 30]|numeric[*][\*]|  
|double [*... 255] [\*... 30]|numeric[*][\*]|  
|고정|NUMERIC|  
|고정 [*... 65] [\*... 30]|numeric[*][\*]|  
|FLOAT|float[24]|  
|float [*... 255] [\*... 30]|numeric[*][\*]|  
|float [*... 53]|float[53]|  
|ssNoversion|ssNoversion|  
|int[*..255]|ssNoversion|  
|integer|ssNoversion|  
|integer[*..255]|ssNoversion|  
|longblob|varbinary(max)|  
|longtext|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|ssNoversion|  
|mediumint [*... 255]|ssNoversion|  
|mediumtext|nvarchar(max)|  
|national char|nchar[1]|  
|national char [0..1]|nchar[1]|  
|national char [2..255]|nchar[*]|  
|국가별 문자|nchar[1]|  
|국가별 문자 변경|nvarchar[1]|  
|[0..1] 다양 한 국가별 문자|nvarchar[1]|  
|[2..4000] 다양 한 국가별 문자|nvarchar[*]|  
|다양 한 국가별 문자 [4001.. *]|nvarchar(max)|  
|국가별 문자 [0..1]|nchar[1]|  
|국가별 문자 [2..255]|nchar[*]|  
|national varchar|nvarchar[1]|  
|national varchar [0..1]|nvarchar[1]|  
|national varchar [2..4000]|nvarchar[*]|  
|national varchar [4001.. *]|nvarchar(max)|  
|NCHAR|nchar[1]|  
|nchar varchar|nvarchar[1]|  
|nchar varchar [0..1]|nvarchar[1]|  
|nchar varchar [2..4000]|nvarchar[*]|  
|nchar varchar [4001.. *]|nvarchar(max)|  
|nchar [0..1]|nchar[1]|  
|nchar[2..255]|nchar[*]|  
|NUMERIC|NUMERIC|  
|숫자 [*... 65]|numeric[*][0]|  
|숫자 [*... 65] [\*... 30]|numeric[*][\*]|  
|NVARCHAR|nvarchar[1]|  
|nvarchar [0..1]|nvarchar[1]|  
|nvarchar[2..4000]|nvarchar[*]|  
|nvarchar[4001..*]|nvarchar(max)|  
|REAL|float[53]|  
|실제 [*... 255] [\*... 30]|numeric[*][\*]|  
|직렬|BIGINT|  
|SMALLINT|SMALLINT|  
|smallint[*..255]|SMALLINT|  
|text|nvarchar(max)|  
|텍스트 [0..1]|nvarchar[1]|  
|텍스트 [2..4000]|nvarchar[*]|  
|text[4001..*]|nvarchar(max)|  
|Time|Time|  
|TIMESTAMP|DATETIME|  
|tinyblob|varbinary[255]|  
|TINYINT|SMALLINT|  
|tinyint[*..255]|SMALLINT|  
|tinytext|nvarchar[255]|  
|서명 되지 않은 bigint|BIGINT|  
|서명 되지 않은 bigint [*... 255]|BIGINT|  
|부호 없는 10 진수|Decimal|  
|부호 없는 dec [*... 65]|decimal[*][0]|  
|부호 없는 dec [*... 65] [\*... 30]|decimal[*][\*]|  
|부호 없는 십진수|Decimal|  
|부호 없는 십진수 [*... 65]|decimal[*][0]|  
|부호 없는 십진수 [*... 65] [\*... 30]|decimal[*][\*]|  
|부호 없는 이중|float[53]|  
|부호 없는 배정밀도|float[53]|  
|배정밀도 서명 되지 않은 [*... 255] [\*... 30]|numeric[*][\*]|  
|double 서명 되지 않은 [*... 255] [\*... 30]|numeric[*][\*]|  
|서명 되지 않은 고정|NUMERIC|  
|서명 되지 않은 고정 [*... 65] [\*... 30]|numeric[*][\*]|  
|부호 없는 float|float[24]|  
|부호 없는 float [*... 255] [\*... 30]|numeric[*][\*]|  
|부호 없는 float [*... 53]|float[53]|  
|부호 없는 정수|BIGINT|  
|부호 없는 int [*... 255]|BIGINT|  
|부호 없는 정수|BIGINT|  
|부호 없는 정수 [*... 255]|BIGINT|  
|부호 없는 mediumint|ssNoversion|  
|부호 없는 mediumint [*... 255]|ssNoversion|  
|부호 없는 숫자|NUMERIC|  
|부호 없는 숫자 [*... 65]|numeric[*][0]|  
|부호 없는 숫자 [*... 65] [\*... 30]|numeric[*][\*]|  
|부호 없는 실제|float[53]|  
|실제 서명 되지 않은 [*... 255 [[\*... 30]|numeric[*][\*]|  
|부호 없는 smallint|ssNoversion|  
|부호 없는 smallint [*... 255]|ssNoversion|  
|부호 없는 tinyint|TINYINT|  
|부호 없는 tinyint [*... 255]|TINYINT|  
|varbinary [0..1]|varbinary[1]|  
|varbinary [2..8000]|varbinary[*]|  
|varbinary[8001..*]|varbinary(max)|  
|varchar [0..1]|nvarchar[1]|  
|varchar[2..4000]|nvarchar[*]|  
|varchar[4001..*]|nvarchar(max)|  
|year|SMALLINT|  
|연도 [2..2]|SMALLINT|  
|연도 [4..4]|SMALLINT|  
  
##### <a name="add"></a>추가  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
##### <a name="edit"></a>편집  
매핑 목록에 있는 데이터 형식을 편집 하려면 클릭 합니다.  
  
##### <a name="remove"></a>제거  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
##### <a name="reset-to-default"></a>기본값으로 다시 설정  
모든 데이터 형식 매핑을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
