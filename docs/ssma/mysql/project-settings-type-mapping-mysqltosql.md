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
ms.openlocfilehash: beb82f2fd894af71bb6f291dcc6f86a995f8dd85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138334"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>프로젝트 설정(형식 매핑)(MySQLToSQL)
형식 매핑 프로젝트 설정을 사용 하 여 SSMA 프로젝트에 대 한 기본 형식 매핑을 설정할 수 있습니다.  

형식 매핑은 프로젝트 설정 및 기본 프로젝트 설정 대화 상자에서 사용할 수 있습니다.  
  
-   프로젝트 설정 대화 상자를 사용 하 여 현재 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 형식 매핑 설정에 액세스 하려면 도구 메뉴에서 프로젝트 설정을 선택한 다음 왼쪽 창에서 형식 매핑을 클릭 합니다.  
  
-   기본 프로젝트 설정 대화 상자를 사용 하 여 모든 프로젝트에 대 한 구성 옵션을 설정할 수 있습니다. 형식 매핑 설정에 액세스 하려면 도구 메뉴에서 기본 프로젝트 설정을 선택 하 고 마이그레이션 **대상 버전** 드롭다운 메뉴에서 설정을 확인 해야 하는 마이그레이션 프로젝트 형식을 선택한 다음 왼쪽 창에서 형식 매핑을 클릭 합니다.  
  
## <a name="options"></a>옵션  
  
##### <a name="source-type"></a>원본 유형  
대상 데이터베이스 데이터 형식에 매핑되어야 하는 MySQL 데이터 형식입니다.  
  
##### <a name="target-type"></a>대상 유형  
지정 된 MySQL 데이터 형식에 대 한 대상 데이터베이스 데이터 형식입니다.  
  
##### <a name="add"></a>추가  
매핑 목록에 데이터 형식을 추가 하려면 클릭 합니다.  
  
##### <a name="edit"></a>편집  
매핑 목록에서 선택한 데이터 형식을 편집 하려면 클릭 합니다.  
  
##### <a name="remove"></a>제거  
선택한 데이터 형식 매핑을 매핑 목록에서 제거 하려면 클릭 합니다.  
  
##### <a name="reset-to-default"></a>기본값으로 다시 설정  
형식 매핑 목록을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
## <a name="type-mappings"></a>형식 매핑  
다음 표에서는 원본 및 대상 데이터 형식 간의 기본 매핑을 보여 줍니다.  
  
|||  
|-|-|  
|**MySQL 데이터 형식**|**SQL Server 데이터 형식**|  
|bigint|bigint|  
|bigint [*.. 255]|bigint|  
|binary|이진 [1]|  
|binary [0 ..1]|이진 [1]|  
|binary [2.. 255]|binary [*]|  
|bit|이진 [1]|  
|bit [0 ... 8]|이진 [1]|  
|비트 [17.. 24]|binary [3]|  
|bit [25 ... 32]|이진 [4]|  
|비트 [33 ... 40]|이진 [5]|  
|비트 [41.48]|이진 [6]|  
|비트 [49 ... 56]|binary [7]|  
|bit [57 ... 64]|이진 [8]|  
|bit [9 ... 16]|이진 [2]|  
|Blob|varbinary(max)|  
|blob [0 ..1]|varbinary [1]|  
|blob [2.8000]|varbinary [*]|  
|blob [8001 *]|varbinary(max)|  
|부울|bit|  
|boolean|bit|  
|char|nchar [1]|  
|char 바이트|이진 [1]|  
|char byte [0 ..1]|이진 [1]|  
|char byte [2.. 255]|binary [*]|  
|char [0 ..1]|nchar [1]|  
|char [2.255]|nchar [*]|  
|character|nchar [1]|  
|문자 변경 [0 ..1]|nvarchar [1]|  
|문자 변경 [2.255]|nvarchar|  
|문자 [0 ..1]|nchar [1]|  
|[2.255] 문자|nchar [*]|  
|date|date|  
|Datetime|datetime2 [0]|  
|dec|decimal|  
|dec [*.. 65]|decimal [*] [0]|  
|dec [*.. 65] [\*.. 인치|decimal [*] [\*]|  
|decimal|decimal|  
|decimal [*.. 65]|decimal [*] [0]|  
|decimal [*.. 65] [\*.. 인치|decimal [*] [\*]|  
|double|float [53]|  
|double precision|float [53]|  
|배정밀도 [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|double [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|고정|numeric|  
|수정 됨 [*.. 65] [\*.. 인치|숫자 [*] [\*]|  
|float|float [24]|  
|float [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|float [*.. 53]|float [53]|  
|int|int|  
|int [*.. 255]|int|  
|integer|int|  
|정수 [*.. 255]|int|  
|longblob|varbinary(max)|  
|longtext|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint [*.. 255]|int|  
|mediumtext|nvarchar(max)|  
|국가별 문자|nchar [1]|  
|국가별 문자 [0 ..1]|nchar [1]|  
|국가별 문자 [2.255]|nchar [*]|  
|국가별 문자|nchar [1]|  
|국가별 문자 변경|nvarchar [1]|  
|국가 문자 변경 [0 ..1]|nvarchar [1]|  
|국가별 문자는 다양 한 [2 ... 4000]|nvarchar [*]|  
|국가별 문자 변경 [4001 *]|nvarchar(max)|  
|국가 문자 [0 ..1]|nchar [1]|  
|국가별 문자 [2.255]|nchar [*]|  
|국가별 varchar|nvarchar [1]|  
|국가별 varchar [0 ..1]|nvarchar [1]|  
|국가별 varchar [2 ... 4000]|nvarchar [*]|  
|국가별 varchar [4001 *]|nvarchar(max)|  
|nchar|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0 ..1]|nvarchar [1]|  
|nchar varchar [2 ... 4000]|nvarchar [*]|  
|nchar varchar [4001 *]|nvarchar(max)|  
|nchar [0 ..1]|nchar [1]|  
|nchar [2.255]|nchar [*]|  
|numeric|numeric|  
|숫자 [*.. 65]|숫자 [*] [0]|  
|숫자 [*.. 65] [\*.. 인치|숫자 [*] [\*]|  
|nvarchar|nvarchar [1]|  
|nvarchar [0 ..1]|nvarchar [1]|  
|nvarchar [2 ... 4000]|nvarchar [*]|  
|nvarchar [4001 *]|nvarchar(max)|  
|real|float [53]|  
|real [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|serial|bigint|  
|smallint|smallint|  
|smallint [*.. 255]|smallint|  
|text|nvarchar(max)|  
|텍스트 [0 ..1]|nvarchar [1]|  
|텍스트 [2 ... 4000]|nvarchar [*]|  
|텍스트 [4001 *]|nvarchar(max)|  
|time|time|  
|timestamp|Datetime|  
|tinyblob|varbinary [255]|  
|tinyint|smallint|  
|tinyint [*.. 255]|smallint|  
|tinytext|nvarchar [255]|  
|부호 없는 bigint|bigint|  
|unsigned bigint [*.. 255]|bigint|  
|unsigned dec|decimal|  
|unsigned dec [*.. 65]|decimal [*] [0]|  
|unsigned dec [*.. 65] [\*.. 인치|decimal [*] [\*]|  
|부호 없는 10 진수|decimal|  
|unsigned decimal [*.. 65]|decimal [*] [0]|  
|unsigned decimal [*.. 65] [\*.. 인치|decimal [*] [\*]|  
|부호 없는 double|float [53]|  
|부호 없는 배정밀도|float [53]|  
|부호 없는 배정밀도 [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|unsigned double [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|부호 없는 고정|numeric|  
|부호 없는 고정 [*.. 65] [\*.. 인치|숫자 [*] [\*]|  
|부호 없는 부동 소수점|float [24]|  
|unsigned float [*.. 255] [\*.. 인치|숫자 [*] [\*]|  
|unsigned float [*.. 53]|float [53]|  
|부호 없는 정수|bigint|  
|unsigned int [*.. 255]|bigint|  
|부호 없는 정수|bigint|  
|부호 없는 정수 [*.. 255]|bigint|  
|unsigned mediumint|int|  
|unsigned mediumint [*.. 255]|int|  
|부호 없는 숫자|numeric|  
|부호 없는 숫자 [*.. 65]|숫자 [*] [0]|  
|부호 없는 숫자 [*.. 65] [\*.. 인치|숫자 [*] [\*]|  
|서명 되지 않은 실수|float [53]|  
|부호 없는 실수 [*.. 255 [[\*.. 인치|숫자 [*] [\*]|  
|unsigned smallint|int|  
|unsigned smallint [*.. 255]|int|  
|unsigned tinyint|tinyint|  
|unsigned tinyint [*.. 255]|tinyint|  
|varbinary [0 ..1]|varbinary [1]|  
|varbinary [2.8000]|varbinary [*]|  
|varbinary [8001 *]|varbinary(max)|  
|varchar [0 ..1]|nvarchar [1]|  
|varchar [2 ... 4000]|nvarchar [*]|  
|varchar [4001 *]|nvarchar(max)|  
|year|smallint|  
|year [2 ... 2]|smallint|  
|year [4.4.4]|smallint|  
  
##### <a name="add"></a>추가  
매핑 목록에 데이터 형식을 추가 하려면 클릭 합니다.  
  
##### <a name="edit"></a>편집  
매핑 목록에서 데이터 형식을 편집 하려면 클릭 합니다.  
  
##### <a name="remove"></a>제거  
선택한 데이터 형식 매핑을 매핑 목록에서 제거 하려면 클릭 합니다.  
  
##### <a name="reset-to-default"></a>기본값으로 다시 설정  
모든 데이터 형식 매핑을 SSMA 기본값으로 다시 설정 하려면 클릭 합니다.  
  
