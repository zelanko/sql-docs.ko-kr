---
title: "데이터 검색 | Microsoft Docs"
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
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6cee44ce2e24055285b56b7889902166d460f1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data"></a>데이터 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목 및 이 섹션의 항목에서는 데이터를 검색하는 방법을 설명합니다.  
  
## <a name="sqlsrv-driver"></a>SQLSRV 드라이버  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 SQLSRV 드라이버는 결과 집합에서 데이터를 검색하기 위한 다음 옵션을 제공합니다.  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> 위에서 언급한 함수를 사용하는 경우 루프 종료 조건으로 null 비교를 사용하지 않습니다. 오류가 발생하면 **sqlsrv** 함수가 false를 반환하기 때문에 다음 코드는 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)에서 오류가 발생할 때 무한 루프를 발생시킬 수 있습니다.  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
쿼리가 둘 이상의 결과 집합을 검색하는 경우 [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)로 다음 결과 집합으로 이동할 수 있습니다.  
  
버전 1.1부터는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용할 수 있습니다 [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) 결과 집합 행에 있는지 확인 합니다.  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버  
PDO_SQLSRV 드라이버는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 결과 집합에서 데이터를 검색 하기 위한 다음 옵션을 제공 합니다.  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
쿼리가 둘 이상의 결과 집합을 검색하는 경우 [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md)로 다음 결과 집합으로 이동할 수 있습니다.  
  
스크롤 가능한 커서를 지정하고 [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md)를 호출하면 결과 집합에 얼마나 많은 행이 있는지 확인할 수 있습니다.  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) 를 통해 커서 유형을 지정할 수 있습니다. 그런 다음 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 를 사용하여 행을 선택할 수 있습니다. 샘플 및 자세한 내용은 [PDO::prepare](../../connect/php/pdo-prepare.md) 를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|---------|---------------|  
|[데이터를 스트림으로 검색](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|서버에서 데이터를 스트리밍하는 방법의 개요를 제공하고 특정 사용 사례에 대한 링크를 제공합니다.|  
|[방향 매개 변수 사용](../../connect/php/using-directional-parameters.md)|저장 프로시저를 호출할 때 방향 매개 변수를 사용하는 방법을 설명합니다.|  
|[커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|SQLSRV 드라이버를 사용하는 경우에 순서에 관계없이 액세스할 수 있는 행으로 결과 집합을 만드는 방법을 보여 줍니다.|  
|[방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|날짜 및 시간 형식을 문자열로 검색하는 방법을 설명합니다.|  
  
## <a name="related-sections"></a>관련 단원  
[방법: PHP 데이터 형식 지정](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[데이터 검색](../../connect/php/retrieving-data.md)  
  

