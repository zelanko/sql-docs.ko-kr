---
title: "SQLSRV 드라이버 API 참조 | Microsoft Docs"
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
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bd1cf731f49119e54fb9e5a548a8988af1ef9fc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrv-driver-api-reference"></a>SQLSRV 드라이버 API 참조
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 SQLSRV 드라이버 API 이름은 **sqlsrv**입니다. 모든 **sqlsrv** 함수 시작 **sqlsrv_** 동사 또는 명사가 옵니다 뒤에 야 합니다. 뒤에 동사가 오는 함수가 일부 작업을 수행하고 뒤에 명사가 오는 함수는 특정 형식의 메타데이터를 반환합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
SQLSRV 드라이버에는 다음과 같은 함수가 포함되어 있습니다.  
  
|함수|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|트랜잭션을 시작합니다.|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|문을 취소하고 문에 대한 모든 보류 중인 결과를 삭제합니다.|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|클라이언트에 대한 정보를 제공합니다.|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|연결을 닫습니다. 연결과 관련된 모든 리소스를 해제합니다.|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|트랜잭션을 커밋합니다.|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|오류 처리 및 로깅 구성을 변경합니다.|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|연결을 만들고 엽니다.|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|마지막 작업에 대한 오류 및/또는 경고 정보를 반환합니다.|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|준비된 문을 실행합니다.|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|데이터의 다음 행을 읽을 수 있도록 만듭니다.|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|데이터의 다음 행을 숫자로 인덱싱된 배열, 결합형 배열 또는 둘 다로 검색합니다.|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|데이터의 다음 행을 개체로 검색합니다.|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|필드 메타데이터를 반환합니다.|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|문을 닫습니다. 문과 관련된 모든 리소스를 해제합니다.|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|지정된 구성 설정의 값을 반환합니다.|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|현재 행의 필드를 인덱스로 검색합니다. PHP 반환 형식을 지정할 수 있습니다.|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|결과 집합에 하나 이상의 행이 있는지 검색합니다.|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|다음 결과를 처리할 수 있도록 만듭니다.|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|결과 집합의 행 수를 보고합니다.|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|활성 결과 집합의 필드 수를 검색합니다.|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|Transact-SQL 쿼리를 실행하지 않고 준비합니다. 암시적으로 매개 변수를 바인딩합니다.|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|Transact-SQL 쿼리를 준비하고 실행합니다.|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|트랜잭션을 롤백합니다.|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|수정된 행 수를 반환합니다.|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|함수를 호출할 때마다 서버에 최대 8KB의 데이터를 보냅니다.|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|서버에 대한 정보를 제공합니다.|  
  
## <a name="reference"></a>참조  
[PHP 매뉴얼](http://go.microsoft.com/fwlink/?LinkId=105500)  
  
## <a name="see-also"></a>관련 항목:  
[PHP SQL 드라이버 개요](../../connect/php/overview-of-the-php-sql-driver.md)
[상수 &#40; Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[PHP SQL 드라이버 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)
  

