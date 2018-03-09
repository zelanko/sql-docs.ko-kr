---
title: "프로젝트 설정 (형식 매핑) (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ab07bb5ad3932c45dacb7aa1b359083f05ec9bf
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="project-settings-type-mapping-db2tosql"></a>프로젝트 설정 (형식 매핑) (DB2ToSQL)
형식 매핑 페이지는 **프로젝트 설정** 대화 상자 SSMA DB2 데이터 형식으로 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다.  
  
형식 매핑 페이지는에서 사용할 수는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자.  
  
-   에 모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 클릭 **기본 프로젝트 설정**, 설정을 보거나에서 변경 하는 데 필요한는 마이그레이션 프로젝트 형식을 선택 **마이그레이션 대상 버전** 드롭다운 하 고 클릭 **유형 매핑** 왼쪽 창의 맨 아래에 합니다.  
  
-   에 현재 프로젝트에 대 한 설정을 지정 하려면는 **도구** 메뉴 클릭 **프로젝트 설정**, 클릭 하 고 **유형 매핑** 왼쪽 창의 맨 아래에 있습니다.  
  
현재 개체 또는 개체의 클래스에 대 한 설정을 지정 하려면는 **유형 매핑** 기본 SSMA 창에서 탭 합니다.  
  
## <a name="options"></a>옵션  
다음 표는 **유형 매핑** 탭 옵션:  
  
**원본 형식**  
매핑된 DB2 데이터 형식입니다.  
  
대상 유형  
대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 지정된 된 DB2 데이터 형식에 대 한 데이터 형식입니다.  
  
DB2 형식 매핑에 대 한 기본 SSMA 한 다음 섹션의 표를 참조 하십시오.  
  
**추가**  
데이터 형식 매핑 목록에 추가 하려면 클릭 합니다.  
  
**편집**  
선택한 데이터 형식 매핑 목록에서 편집 하려면 클릭 합니다.  
  
**제거**  
매핑 목록에서 선택한 데이터 형식 매핑을 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
형식 매핑 목록 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="default-type-mappings"></a>기본 형식 매핑  
SSMA for d b 2 인수, 열, 지역 변수 및 반환 값에 대 한 사용자 지정 형식 매핑을 설정할 수 있습니다. 인수 및 반환 형식에 대 한 기본 매핑을 거의 동일 합니다.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>기본 인수 형식 및 반환 값 형식 매핑  
다음 표에서 인수 및 반환 값에 대 한 기본 데이터 형식 매핑을 보여 줍니다.  
  
|DB2 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|decimal|float[53]|  
|배정밀도|float[53]|  
|float|float[53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|긴 원시|varbinary(max)|  
|긴 원시 [\*... 8000]<sup>*</sup>|varbinary[*]|  
|긴 원시 [8001..\*]<sup>*</sup>|varbinary(max)|  
|국가별 문자|nvarchar(max)|  
|다양 한 국가별 문자|nvarchar(max)|  
|국가별 문자|nvarchar(max)|  
|다양 한 국가별 문자<sup>**</sup>|nvarchar(max)|  
|다양 한 국가별 문자<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|number|float[53]|  
|numeric|float[53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float[53]|  
|Rowid|uniqueidentifier|  
|signtype|smallint|  
|smallint|smallint|  
|string|varchar(max)|  
|timestamp|datetime2|  
|현지 표준 시간대 포함 된 타임 스탬프|datetimeoffset|  
|표준 시간대와 타임 스탬프|datetimeoffset|  
|Urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>*</sup> 값 형식 매핑만 반환에 적용 됩니다.  
  
<sup>**</sup> 인수 형식 매핑만에 적용 됩니다.  
  
### <a name="default-column-type-mapping"></a>기본 열 형식 매핑  
다음 표에서 열에 대 한 기본 형식 매핑을 보여 줍니다.  
  
|DB2 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|다양 한 char [*... \*]|varchar[*]|  
|char[*..\*]|char[*]|  
|character|char|  
|다양 한 문자 [*... \*]|varchar[*]|  
|character[*..\*]|char[*]|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[*..\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|배정밀도|float[53]|  
|float|float[53]|  
|float[*..53]|float[*]|  
|float[54..*]|float[53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|긴 원시|varbinary(max)|  
|긴 원시 [*... 8000]|varbinary[*]|  
|긴 원시 [8001.. *]|varbinary(max)|  
|long varchar|varchar(max)|  
|긴 [*... 8000]|varchar[*]|  
|long[8001..*]|varchar(max)|  
|국가별 문자|NCHAR|  
|다양 한 national char [*... \*]|nvarchar[*]|  
|national char [*... \*]|nchar[*]|  
|국가별 문자|NCHAR|  
|다양 한 국가별 문자 [*... \*]|nvarchar[*]|  
|국가별 문자 [*... \*]|nchar[*]|  
|NCHAR|NCHAR|  
|nchar[*]|nchar[*]|  
|Nclob|nvarchar(max)|  
|number|float[53]|  
|number[*..\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|numeric|numeric|  
|numeric[*..\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..\*]|nvarchar[*]|  
|raw[*..\*]|varbinary[*]|  
|real|float[53]|  
|Rowid|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|현지 표준 시간대 포함 된 타임 스탬프|datetimeoffset|  
|현지 표준 시간대 포함 된 타임 스탬프 [*... \*]|datetimeoffset[*]|  
|표준 시간대와 타임 스탬프|datetimeoffset|  
|타임 스탬프와 표준 시간대 [*... \*]|datetimeoffset[*]|  
|timestamp[*..\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid[*..\*]|uniqueidentifier|  
|varchar[*..\*]|varchar[*]|  
|varchar2[*..\*]|varchar[*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>기본 지역 변수 형식 매핑  
다음 표에서 지역 변수에 대 한 기본 형식 매핑을 보여 줍니다.  
  
|DB2 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|다양 한 char [*... 8000]|varchar[*]|  
|다양 한 char [8001.. *]|varchar(max)|  
|char[*..8000]|char[*]|  
|char[8001..*]|varchar(max)|  
|문자|char|  
|다양 한 문자 [*... 8000]|varchar[*]|  
|다양 한 문자 [8001.. *]|varchar(max)|  
|character[*..8000]|char[*]|  
|character[8001..*]|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2[0]|  
|dec|dec[38][0]|  
|dec[*..\*]|dec[*][0]|  
|dec[*..\*][\*..\*]|dec[*][\*]|  
|decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal[*..\*][\*..\*]|decimal[*][\*]|  
|배정밀도|float[53]|  
|부동|float[53]|  
|float[*..53]|float[*]|  
|float[54..*]|float[53]|  
|int|int|  
|정수|int|  
|integer[*..\*]|numeric[*][0]|  
|Long|varchar(max)|  
|긴 원시|varbinary(max)|  
|긴 원시 [*... 8000]|varbinary[*]|  
|긴 원시 [8001.. *]|varbinary(max)|  
|국가별 문자|NCHAR|  
|다양 한 national char [*... 4000]|nvarchar[*]|  
|다양 한 national char [4001.. *]|nvarchar(max)|  
|national char [*... 4000]|nchar[*]|  
|national char [4001.. *]|nvarchar(max)|  
|국가별 문자|NCHAR|  
|국가별 문자 [*... 4000]|nvarchar[*]|  
|국가별 문자 [4001.. *]|nvarchar(max)|  
|다양 한 국가별 문자 [*... 4000]|nvarchar[*]|  
|다양 한 국가별 문자 [4001.. *]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[*..4000]|nchar[*]|  
|nchar[4001..*]|nvarchar(max)|  
|nchar 다양 한 [*... 4000]|nvarchar[*]|  
|nchar 다양 한 [4001.. *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float[53]|  
|number[*..\*]|numeric[*]|  
|number[*..\*][\*..\*]|numeric[*][\*]|  
|숫자|numeric[38][0]|  
|numeric[*..\*]|numeric[*]|  
|numeric[*..\*][\*..\*]|numeric[*][\*]|  
|nvarchar2[*..4000]|nvarchar[*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|int|  
|raw[*..8000]|varbinary[*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float[53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|string[*..8000]|varchar[*]|  
|string[8001..*]|varchar(max)|  
|timestamp|datetime2|  
|현지 표준 시간대 포함 된 타임 스탬프|datetimeoffset|  
|표준 시간대와 타임 스탬프|datetimeoffset|  
|현지 표준 시간대 포함 된 타임 스탬프 [*... \*]|datetimeoffset[*]|  
|타임 스탬프와 표준 시간대 [*... \*]|datetimeoffset[*]|  
|timestamp[*..\*]|datetime2[*]|  
|Urowid|uniqueidentifier|  
|urowid[*..\*]|uniqueidentifier|  
|varchar[*..8000]|varchar[*]|  
|varchar[8001..*]|varchar(max)|  
|varchar2[*..8000]|varchar[*]|  
|varchar2[8001..*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 참조 &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
