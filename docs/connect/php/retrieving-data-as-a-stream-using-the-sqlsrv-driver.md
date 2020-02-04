---
title: SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b83188359489759f50b2929de769721d627c15d8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992904"
---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>SQLSRV 드라이버를 사용하여 스트림으로 데이터 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

스트림으로 데이터 검색은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 SQLSRV 드라이버에서만 사용 가능하고 PDO_SQLSRV 드라이버에서는 사용할 수 없습니다.  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 스트림을 활용하여 대량의 데이터를 검색합니다. 이 섹션의 항목에서는 스트림으로 데이터를 검색하는 방법에 대한 자세한 내용을 제공합니다.  
  
다음 단계는 스트림으로 데이터를 검색하는 방법을 요약합니다.  
  
1.  [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 조합을 사용하여 Transact-SQL 쿼리를 준비하고 실행합니다.  
  
2.  [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) 를 사용하여 결과 집합의 다음 행으로 이동합니다.  
  
3.  [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) 를 사용하여 행에서 필드를 검색합니다. 함수 호출에서 세 번째 매개 변수로 **SQLSRV_PHPTYPE_STREAM(<encoding>)** 을 사용하여 데이터를 스트림으로 검색하도록 지정합니다. 다음 표에서는 인코딩과 해당 설명을 지정하는 데 사용되는 상수를 나열합니다.  
  
    |SQLSRV 상수|Description|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|데이터는 인코딩 또는 변환을 수행하지 않은 원시 바이트 스트림으로 서버에서 반환됩니다.|  
    |SQLSRV_ENC_CHAR|데이터는 시스템에 설정된 Windows 로캘의 코드 페이지에 지정된 8비트 문자로 반환됩니다. 모든 멀티바이트 문자 또는 이 코드 페이지에 매핑되지 않는 문자는 싱글바이트 물음표(?) 문자로 대체됩니다.|  
  
> [!NOTE]  
> 일부 데이터 형식은 기본적으로 스트림으로 반환됩니다. 자세한 내용은 [Default PHP Data Types](../../connect/php/default-php-data-types.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|---------|---------------|  
|[SQLSRV 드라이버를 사용하여 스트림으로 데이터 형식 지원](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|스트림으로 검색할 수 있는 SQL Server 데이터 유형을 나열합니다.|  
|[방법: SQLSRV 드라이버를 사용하여 스트림으로 문자 데이터 검색](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|스트림으로 문자 데이터를 검색하는 방법을 보여 줍니다.|  
|[방법: SQLSRV 드라이버를 사용하여 스트림으로 이진 데이터 검색](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|스트림으로 이진 데이터를 검색하는 방법을 보여 줍니다.|  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)

[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
