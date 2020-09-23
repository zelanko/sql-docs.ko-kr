---
title: 기본 PHP 데이터 형식
description: 이 항목에는 Microsoft SQLSRV Driver for PHP for SQL Server를 사용할 때 모든 기본 PHP 데이터 형식과 해당 SQL Server 데이터 형식이 나열되어 있습니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1e1cf91baf80fd6298eaaca9c9e12a0b5858d9f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680794"
---
# <a name="default-php-data-types"></a>기본 PHP 데이터 형식
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

서버에서 데이터를 검색할 때 사용자가 PHP 데이터 형식을 지정하지 않은 경우 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 데이터를 기본 PHP 데이터 형식으로 변환합니다.  
  
PDO_SQLSRV 드라이버를 사용하여 데이터가 반환되는 경우 데이터 형식은 정수 또는 문자열입니다.  
  
이 항목의 나머지 부분에서는 SQLSRV 드라이버를 사용하는 기본 데이터 형식을 설명합니다.  
  
다음 표에서는 SQL Server 데이터 형식(서버에서 검색 중인 데이터 형식), 기본 PHP 데이터 형식(데이터를 변환할 대상 데이터 형식) 및 스트림과 문자열에 대한 기본 인코딩을 보여 줍니다. 서버에서 데이터를 검색할 때 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
|SQL Server 형식|기본 PHP 형식|기본 인코딩|  
|-------------------|--------------------|--------------------|  
|bigint|String|8비트 문자<sup>1</sup>|  
|binary|스트림<sup>2</sup>|이진<sup>3</sup>|  
|bit|정수|8비트 문자<sup>1</sup>|  
|char|String|8비트 문자<sup>1</sup>|  
|date<sup>4</sup>|DateTime|해당 없음|  
|datetime<sup>4</sup>|DateTime|해당 없음|  
|datetime2<sup>4</sup>|DateTime|해당 없음|  
|datetimeoffset<sup>4</sup>|DateTime|해당 없음|  
|decimal|String|8비트 문자<sup>1</sup>|  
|float|Float|8비트 문자<sup>1</sup>|  
|geography|스트림|이진<sup>3</sup>|  
|geometry|스트림|이진<sup>3</sup>|  
|image<sup>5</sup>|스트림<sup>2</sup>|이진<sup>3</sup>|  
|int|정수|8비트 문자<sup>1</sup>|  
|money|String|8비트 문자<sup>1</sup>|  
|nchar|String|8비트 문자<sup>1</sup>|  
|numeric|String|8비트 문자<sup>1</sup>|  
|nvarchar|String|8비트 문자<sup>1</sup>|  
|nvarchar(MAX)|스트림<sup>2</sup>|8비트 문자<sup>1</sup>|  
|ntext<sup>6</sup>|스트림<sup>2</sup>|8비트 문자<sup>1</sup>|  
|real|Float|8비트 문자<sup>1</sup>|  
|smalldatetime|DateTime|8비트 문자<sup>1</sup>|  
|smallint|정수|8비트 문자<sup>1</sup>|  
|smallmoney|String|8비트 문자<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|8비트 문자<sup>1</sup>|  
|text<sup>8</sup>|스트림<sup>2</sup>|8비트 문자<sup>1</sup>|  
|time<sup>4</sup>|DateTime|해당 없음|  
|timestamp|String|8비트 문자<sup>1</sup>|  
|tinyint|정수|8비트 문자<sup>1</sup>|  
|UDT|스트림<sup>2</sup>|이진<sup>3</sup>|  
|uniqueidentifier|String<sup>9</sup>|8비트 문자<sup>1</sup>|  
|varbinary|스트림<sup>2</sup>|이진<sup>3</sup>|  
|varbinary(MAX)|스트림<sup>2</sup>|이진<sup>3</sup>|  
|varchar|String|8비트 문자<sup>1</sup>|  
|varchar(MAX)|스트림<sup>2</sup>|8비트 문자<sup>1</sup>|
|Xml|스트림<sup>2</sup>|8비트 문자<sup>1</sup>|  
  

1.  데이터는 시스템에 설정된 Windows 로캘의 코드 페이지에 지정된 8비트 문자로 반환됩니다. 모든 멀티바이트 문자 또는 이 코드 페이지에 매핑되지 않는 문자는 싱글바이트 물음표(?) 문자로 대체됩니다.  
  
2.  [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) 또는 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)를 사용하여 스트림의 기본 PHP 형식이 지정된 데이터를 검색하는 경우 스트림과 인코딩이 동일한 문자열로 데이터가 반환됩니다. 예를 들어 **sqlsrv_fetch_array**를 사용하여 SQL Server 이진 형식을 검색하는 경우 기본 반환 형식은 이진 문자열입니다.  
  
3.  데이터는 인코딩 또는 변환을 수행하지 않은 원시 바이트 스트림으로 서버에서 반환됩니다.  

4.  날짜 및 시간 형식을 문자열로 가져올 수 있습니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)을 참조하세요.  

5.  varbinary(max) 형식에 매핑되는 레거시 형식입니다.

6. nvarchar(max) 형식에 매핑되는 레거시 형식입니다.

7.  sql_variant는 양방향 또는 출력 매개 변수에서 지원되지 않습니다.

8.  varchar(max) 형식에 매핑되는 레거시 형식입니다.  
  
9.  UNIQUEIDENTIFIER는 다음 정규식을 나타내는 GUID입니다.  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>기타 새로운 SQL Server 2008 데이터 형식 및 기능  
SQL Server 2008에 새로 추가되었지만 열에 포함되지 않은 데이터 형식(예: 테이블 반환 매개 변수)은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 지원되지 않습니다. 다음 표에는 새로운 SQL Server 2008 기능에 대한 PHP 지원이 요약되어 있습니다.  
  
|기능|PHP 지원|  
|-----------|---------------|  
|테이블 반환 매개 변수|아니요|  
|스파스 열|Partial|  
|Null 비트 압축|예|  
|큰 CLR UDT(사용자 정의 형식)|예|  
|서비스 사용자 이름|아니요|  
|MERGE|예|  
|FILESTREAM|Partial|  
  
부분 형식 지원이란 열 형식에 대해 프로그래밍 방식으로 쿼리할 수 없다는 의미입니다.  
  
## <a name="see-also"></a>참고 항목  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[데이터 형식 변환](../../connect/php/converting-data-types.md)

[PHP 형식](https://php.net/manual/en/language.types.php)

[데이터 형식(Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
