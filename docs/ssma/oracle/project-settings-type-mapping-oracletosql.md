---
title: 프로젝트 설정 (형식 매핑) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 4551181da22af1244f8083f6df5ea00f63e00e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266579"
---
# <a name="project-settings-type-mapping-oracletosql"></a>프로젝트 설정(형식 매핑)(OracleToSQL)
**프로젝트 설정** 대화 상자의 형식 매핑 페이지에는 Ssma에서 Oracle 데이터 형식을 데이터 형식으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 하는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다.  
  
형식 매핑 페이지는 **프로젝트 설정** 및 **기본 프로젝트 설정** 대화 상자에서 사용할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 하 고 마이그레이션 **대상 버전** 드롭다운에서 설정 하거나 변경 해야 하는 설정에 대 한 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창의 맨 아래에 있는 **형식 매핑** 을 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 클릭 한 다음 왼쪽 창의 맨 아래에 있는 **형식 매핑** 을 클릭 합니다.  
  
현재 개체 또는 개체 클래스에 대 한 설정을 지정 하려면 기본 SSMA 창의 **형식 매핑** 탭을 사용 합니다.  
  
## <a name="options"></a>옵션  
다음 표에서는 **형식 매핑** 탭 옵션을 보여 줍니다.  
  
**원본 형식**  
매핑된 Oracle 데이터 형식입니다.  
  
**대상 유형**  
지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 데이터 형식에 대 한 대상 데이터 형식입니다.  
  
기본 SSMA for Oracle 형식 매핑에 대 한 다음 섹션의 표를 참조 하세요.  
  
**추가**  
매핑 목록에 데이터 형식을 추가 하려면 클릭 합니다.  
  
**편집**  
매핑 목록에서 선택한 데이터 형식을 편집 하려면 클릭 합니다.  
  
**제거**  
선택한 데이터 형식 매핑을 매핑 목록에서 제거 하려면 클릭 합니다.  
  
**기본값으로 다시 설정**  
형식 매핑 목록을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="default-type-mappings"></a>기본 형식 매핑  
Oracle 용 SSMA에서 인수, 열, 지역 변수 및 반환 값에 대 한 사용자 지정 형식 매핑을 설정할 수 있습니다. 인수 및 반환 형식에 대 한 기본 매핑은 거의 동일 합니다.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>기본 인수 형식 및 반환 값 형식 매핑  
다음 표에서는 인수 및 반환 값에 대 한 기본 데이터 형식 매핑을 포함 합니다.  
  
|Oracle 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|  
|--------------------|-------------------------------------------------------------------------|  
|목록은|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|Blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|decimal|float [53]|  
|double precision|float [53]|  
|float|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|긴 원시|varbinary(max)|  
|long raw [\*.. 8000]<sup>*</sup>|varbinary [*]|  
|long raw [8001\*]<sup>*</sup>|varbinary(max)|  
|국가별 문자|nvarchar(max)|  
|국가별 문자 변경|nvarchar(max)|  
|국가별 문자|nvarchar(max)|  
|국가별 문자 변경<sup>**</sup>|nvarchar(max)|  
|국가별 문자 변경<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|rowid|uniqueidentifier|  
|signtype|smallint|  
|smallint|smallint|  
|문자열|varchar(max)|  
|timestamp|datetime2|  
|현지 표준 시간대를 사용 하는 타임 스탬프|datetimeoffset|  
|표준 시간대가 있는 타임 스탬프|datetimeoffset|  
|urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|Xml|  
  
<sup>*</sup>반환 값 형식 매핑에만 적용 됩니다.  
  
<sup>**</sup>인수 형식 매핑에만 적용 됩니다.  
  
### <a name="default-column-type-mapping"></a>기본 열 유형 매핑  
다음 표에서는 열에 대 한 기본 형식 매핑을 포함 합니다.  
  
|Oracle 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|  
|--------------------|-------------------------------------------------------------------------|  
|목록은|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|Blob|varbinary(max)|  
|char|char|  
|문자 변경 [*.. \*]|varchar [*]|  
|char [*.. \*]|char [*]|  
|character|char|  
|문자 변경 [*.. \*]|varchar [*]|  
|문자 [*.. \*]|char [*]|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*.. \*]|dec [*] [0]|  
|dec [*.. \*][\*.. \*]|dec [*] [\*]|  
|decimal|decimal [38] [0]|  
|decimal [*.. \*]|decimal [*] [0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|double precision|float [53]|  
|float|float [53]|  
|float [*.. 53]|float [*]|  
|float [54 ... *]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|긴 원시|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001 *]|varbinary(max)|  
|long varchar|varchar(max)|  
|long [*.. 8000]|varchar [*]|  
|long [8001 *]|varchar(max)|  
|국가별 문자|nchar|  
|국가별 문자는 다양 한 [*.. \*]|nvarchar [*]|  
|국가별 문자 [*.. \*]|nchar [*]|  
|국가별 문자|nchar|  
|국가별 문자는 다양 한 [*.. \*]|nvarchar [*]|  
|국가별 문자 [*.. \*]|nchar [*]|  
|nchar|nchar|  
|nchar [*]|nchar [*]|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|숫자 [*.. \*]|숫자 [*]|  
|숫자 [*.. \*][\*.. \*]|숫자 [*] [\*]|  
|numeric|numeric|  
|숫자 [*.. \*]|숫자 [*]|  
|숫자 [*.. \*][\*.. \*]|숫자 [*] [\*]|  
|nvarchar2[*.. \*]|nvarchar [*]|  
|raw [*.. \*]|varbinary [*]|  
|real|float [53]|  
|rowid|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|현지 표준 시간대를 사용 하는 타임 스탬프|datetimeoffset|  
|현지 표준 시간대를 포함 하는 타임 스탬프 [*... \*]|datetimeoffset [*]|  
|표준 시간대가 있는 타임 스탬프|datetimeoffset|  
|표준 시간대가 있는 타임 스탬프 [*... \*]|datetimeoffset [*]|  
|timestamp [*.. \*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar [*.. \*]|varchar [*]|  
|varchar2[*.. \*]|varchar [*]|  
|Xmltype|Xml|  
  
### <a name="default-local-variable-type-mapping"></a>기본 지역 변수 형식 매핑  
다음 표에서는 지역 변수에 대 한 기본 형식 매핑을 포함 합니다.  
  
|Oracle 데이터 형식|기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|부울|bit|  
|Char|char|  
|문자 변경 [*.. 8000]|varchar [*]|  
|문자 변경 [8001 *]|varchar(max)|  
|char [*.. 8000]|char [*]|  
|char [8001 *]|varchar(max)|  
|문자|char|  
|문자 변경 [*.. 8000]|varchar [*]|  
|문자 변경 [8001 *]|varchar(max)|  
|문자 [*.. 8000]|char [*]|  
|문자 [8001 *]|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*.. \*]|dec [*] [0]|  
|dec [*.. \*][\*.. \*]|dec [*] [\*]|  
|decimal|decimal [38] [0]|  
|decimal [*.. \*]|decimal [*] [0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|double precision|float [53]|  
|Float|float [53]|  
|float [*.. 53]|float [*]|  
|float [54 ... *]|float [53]|  
|Int|int|  
|정수|int|  
|정수 [*.. \*]|숫자 [*] [0]|  
|long|varchar(max)|  
|긴 원시|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001 *]|varbinary(max)|  
|국가별 문자|nchar|  
|국가별 문자는 다양 한 [*.. 4000]|nvarchar [*]|  
|국가별 문자 변경 [4001 *]|nvarchar(max)|  
|국가별 문자 [*.. 4000]|nchar [*]|  
|국가별 문자 [4001 *]|nvarchar(max)|  
|국가별 문자|nchar|  
|국가별 문자 [*.. 4000]|nvarchar [*]|  
|국가별 문자 [4001 *]|nvarchar(max)|  
|국가별 문자는 다양 한 [*.. 4000]|nvarchar [*]|  
|국가별 문자는 다양 한 [4001.. *]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [*.. 4000]|nchar [*]|  
|nchar [4001 *]|nvarchar(max)|  
|nchar 변경 [*.. 4000]|nvarchar [*]|  
|nchar 변경 [4001.. *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|숫자 [*.. \*]|숫자 [*]|  
|숫자 [*.. \*][\*.. \*]|숫자 [*] [\*]|  
|숫자|숫자 [38] [0]|  
|숫자 [*.. \*]|숫자 [*]|  
|숫자 [*.. \*][\*.. \*]|숫자 [*] [\*]|  
|nvarchar2[*.. 4000]|nvarchar [*]|  
|nvarchar2 [4001 *]|nvarchar(max)|  
|pls_integer|int|  
|raw [*.. 8000]|varbinary [*]|  
|raw [8001 *]|varbinary(max)|  
|Real|float [53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|문자열 [*.. 8000]|varchar [*]|  
|문자열 [8001 *]|varchar(max)|  
|timestamp|datetime2|  
|현지 표준 시간대를 사용 하는 타임 스탬프|datetimeoffset|  
|표준 시간대가 있는 타임 스탬프|datetimeoffset|  
|현지 표준 시간대를 포함 하는 타임 스탬프 [*... \*]|datetimeoffset [*]|  
|표준 시간대가 있는 타임 스탬프 [*... \*]|datetimeoffset [*]|  
|timestamp [*.. \*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar [*.. 8000]|varchar [*]|  
|varchar [8001 *]|varchar(max)|  
|varchar2[*.. 8000]|varchar [*]|  
|varchar2 [8001 *]|varcha (max)|  
|Xmltype|Xml|  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;사용자 인터페이스 참조](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
