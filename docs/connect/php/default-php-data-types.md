---
title: "기본 PHP 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2db2186adfe8fc12a80c1459a0e5b768dfd9fe45
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="default-php-data-types"></a>기본 PHP 데이터 형식
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

서버에서 데이터를 검색할 때 사용자가 PHP 데이터 형식을 지정하지 않은 경우 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 데이터를 기본 PHP 데이터 형식으로 변환합니다.  
  
PDO_SQLSRV 드라이버를 사용하여 데이터가 반환되는 경우 데이터 형식은 정수 또는 문자열입니다.  
  
이 항목의 나머지 부분에서는 SQLSRV 드라이버를 사용하는 기본 데이터 형식을 설명합니다.  
  
다음 표에서는 SQL Server 데이터 형식(서버에서 검색 중인 데이터 형식), 기본 PHP 데이터 형식(데이터를 변환할 대상 데이터 형식) 및 스트림과 문자열에 대한 기본 인코딩을 보여 줍니다. 서버에서 데이터를 검색할 때 데이터 형식을 지정하는 방법에 대한 자세한 내용은 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)을 참조하세요.  
  
|SQL Server 형식|기본 PHP 형식|기본 인코딩|  
|-------------------|--------------------|--------------------|  
|bigint|문자열|8 비트 문자<sup>1</sup>|  
|binary|스트림<sup>2</sup>|이진<sup>3</sup>|  
|bit|정수|8 비트 문자<sup>1</sup>|  
|char|문자열|8 비트 문자<sup>1</sup>|  
|date<sup>4</sup>|날짜/시간|해당 사항 없음|  
|날짜/시간<sup>4</sup>|날짜/시간|해당 사항 없음|  
|datetime2<sup>4</sup>|날짜/시간|해당 사항 없음|  
|datetimeoffset<sup>4</sup>|날짜/시간|해당 사항 없음|  
|decimal|문자열|8 비트 문자<sup>1</sup>|  
|float|부동|8 비트 문자<sup>1</sup>|  
|geography|스트림|이진<sup>3</sup>|  
|geometry|스트림|이진<sup>3</sup>|  
|이미지<sup>5</sup>|스트림<sup>2</sup>|이진<sup>3</sup>|  
|int|정수|8 비트 문자<sup>1</sup>|  
|money|문자열|8 비트 문자<sup>1</sup>|  
|nchar|문자열|8 비트 문자<sup>1</sup>|  
|numeric|문자열|8 비트 문자<sup>1</sup>|  
|nvarchar|문자열|8 비트 문자<sup>1</sup>|  
|nvarchar(MAX)|스트림<sup>2</sup>|8 비트 문자<sup>1</sup>|  
|ntext<sup>6</sup>|스트림<sup>2</sup>|8 비트 문자<sup>1</sup>|  
|real|부동|8 비트 문자<sup>1</sup>|  
|smalldatetime|날짜/시간|8 비트 문자<sup>1</sup>|  
|smallint|정수|8 비트 문자<sup>1</sup>|  
|smallmoney|문자열|8 비트 문자<sup>1</sup>|  
|sql_variant<sup>7</sup>|문자열|8 비트 문자<sup>1</sup>|  
|텍스트<sup>8</sup>|스트림<sup>2</sup>|8 비트 문자<sup>1</sup>|  
|time<sup>4</sup>|날짜/시간|해당 사항 없음|  
|timestamp|문자열|8 비트 문자<sup>1</sup>|  
|tinyint|정수|8 비트 문자<sup>1</sup>|  
|UDT|스트림<sup>2</sup>|이진<sup>3</sup>|  
|uniqueidentifier|문자열<sup>9</sup>|8 비트 문자<sup>1</sup>|  
|varbinary|스트림<sup>2</sup>|이진<sup>3</sup>|  
|varbinary(MAX)|스트림<sup>2</sup>|이진<sup>3</sup>|  
|varchar|문자열|8 비트 문자<sup>1</sup>|  
|varchar(MAX)|스트림<sup>2</sup>|8 비트 문자<sup>1</sup>|
|xml|스트림<sup>2</sup>|8 비트 문자<sup>1</sup>|  
  

1.  데이터는 시스템에 설정된 Windows 로캘의 코드 페이지에 지정된 8비트 문자로 반환됩니다. 모든 멀티바이트 문자 또는 이 코드 페이지에 매핑되지 않는 문자는 싱글바이트 물음표(?) 문자로 대체됩니다.  
  
2.  [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) 또는 [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) 를 사용하여 스트림의 기본 PHP 형식이 지정된 데이터를 검색하는 경우 스트림과 인코딩이 동일한 문자열로 데이터가 반환됩니다. 예를 들어 **sqlsrv_fetch_array**를 사용하여 SQL Server 이진 형식을 검색하는 경우 기본 반환 형식은 이진 문자열입니다.  
  
3.  데이터는 인코딩 또는 변환을 수행하지 않은 원시 바이트 스트림으로 서버에서 반환됩니다.  

4.  날짜 및 시간 형식을 문자열로 가져올 수 있습니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)을 참조하세요.  

5.  varbinary(max) 형식에 매핑되는 레거시 형식입니다.

6. nvarchar(max) 형식에 매핑되는 레거시 형식입니다.

7.  sql_variant은 양방향 또는 출력 매개 변수에서 지원 되지 않습니다.

8.  varchar(max) 형식에 매핑되는 레거시 형식입니다.  
  
9.  UNIQUEIDENTIFIER는 다음 정규식을 나타내는 GUID입니다.  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>기타 새로운 SQL Server 2008 데이터 형식 및 기능  
SQL Server 2008의 새로운 않은 열 (예: 테이블 반환 매개 변수)의 외부에 존재 하는 데이터 형식에서 지원 되지 않습니다는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. 다음 표에는 새로운 SQL Server 2008 기능에 대한 PHP 지원이 요약되어 있습니다.  
  
|기능|PHP 지원|  
|-----------|---------------|  
|테이블 반환 매개 변수|아니요|  
|스파스 열|부분|  
|Null 비트 압축|예|  
|큰 CLR UDT(사용자 정의 형식)|예|  
|서비스 사용자 이름|아니요|  
|MERGE|예|  
|FILESTREAM|부분|  
  
부분 형식 지원이란 열 형식에 대해 프로그래밍 방식으로 쿼리할 수 없다는 의미입니다.  
  
## <a name="see-also"></a>참고 항목  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Converting Data Types](../../connect/php/converting-data-types.md)  
[PHP 형식](http://go.microsoft.com/fwlink/?LinkId=109071)  
[데이터 형식 (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=109068)  
[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  

