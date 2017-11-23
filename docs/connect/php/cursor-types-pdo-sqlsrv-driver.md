---
title: "커서 유형 (PDO_SQLSRV 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d9757631940208f0f3ded1fe90eec8fbfd1b061
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="cursor-types-pdosqlsrv-driver"></a>커서 유형 (PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 드라이버를 사용 하면 여러 커서 중 하나로 스크롤 가능한 결과 집합을 만들 수 있습니다.  
  
PDO_SQLSRV 드라이버를 사용 하 여 커서를 지정 하는 방법에 대 한 내용은 및 코드 샘플에 대 한 참조 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다.  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 및 서버 쪽 커서  
버전 3.0 이전의 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], PDO_SQLSRV 드라이버를 사용할 수 있는 서버 쪽 앞 으로만 이동 가능한 또는 정적 커서 결과 집합을 만들 수 있습니다. 버전 3.0부터는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 키 집합 및 동적 커서를 사용할 수도 있습니다.  
  
Pdo:: prepare 또는 pdostatement:: Setattribute를 사용 하 여 커서 유형 중 하나를 선택 하 여 서버 쪽 커서 유형을 나타낼 수 있습니다.  
  
-   PDO:: ATTR_CURSOR = > PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = > PDO:: CURSOR_SCROLL  
  
Pdo:: ATTR_CURSOR를 지정 하 여 키 집합 또는 동적 커서를 요청할 수 = > pdo:: CURSOR_SCROLL 및 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 적절 한 값 전달 합니다. Pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 전달할 수 있는 가능한 값은 같습니다.  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 및 클라이언트 쪽 커서  
클라이언트 쪽 커서의 버전 3.0에서에서 추가 된는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 을 전체 결과 집합을 메모리를 캐시할 수 있습니다. 이점은 행 수를 사용할 수는 쿼리를 실행 한 후입니다.  
  
소규모-결과 집합에 대 한 클라이언트 쪽 커서를 사용 해야 합니다. 큰 결과 집합이 서버 커서를 사용 해야 합니다.  
  
쿼리는 버퍼를 설정 클라이언트 쪽 커서를 사용 하는 경우 전체 결과 보유할 만큼 크지 없으면 false를 반환 합니다. 최대 PHP 메모리 제한의 버퍼 크기를 늘릴 수 있습니다.  
  
결과 집합의 PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE 특성을 보유 하는 버퍼의 크기를 구성할 수 있습니다 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) 또는 [pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)합니다. Pdo_sqlsrv.client_buffer_max_kb_size와 php.ini 파일에서 최대 버퍼 크기를 설정할 수도 있습니다 (예를 들어 pdo_sqlsrv.client_buffer_max_kb_size = 1024)입니다.  
  
Pdo:: prepare 또는 pdostatement:: Setattribute를 사용 하 여 클라이언트 쪽 커서를 원하는 고 하는 pdo:: ATTR_CURSOR 나타낼 = > pdo:: CURSOR_SCROLL 커서 유형입니다.  그런 다음 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE 지정 = > PDO::SQLSRV_CURSOR_BUFFERED 합니다.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));  
$stmt->execute();  
print $stmt->rowCount();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
