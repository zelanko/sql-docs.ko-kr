---
title: 커서 유형 (PDO_SQLSRV 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72cf83b4c4903c7df0b6a857746937e848fccf80
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062360"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>커서 유형(PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 드라이버를 사용 하면 여러 커서 중 하나를 사용 하 여 스크롤 가능한 결과 집합을 만들 수 있습니다.  
  
PDO_SQLSRV 드라이버를 사용 하 여 커서를 지정 하는 방법에 대 한 정보 및 코드 샘플을 참조 하세요 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다.  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 및 서버 쪽 커서  
버전 3.0의 이전을 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], PDO_SQLSRV 드라이버를 사용할 수 있는 서버 쪽 앞 으로만 이동 가능한 또는 정적 커서 결과 집합을 만들 수 있습니다. 버전 3.0부터는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 키 집합 및 동적 커서도 사용할 수 있습니다.  
  
Pdo:: prepare 또는 pdostatement:: Setattribute를 사용 하 여 커서 유형 중 하나를 선택 하 여 서버측 커서 유형을 지정할 수 있습니다.  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_SCROLL  
  
Pdo:: ATTR_CURSOR를 지정 하 여 키 집합 또는 동적 커서를 요청할 수 있습니다 = > pdo:: CURSOR_SCROLL 및 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 적절 한 값을 전달 합니다. Pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 전달할 수 있는 가능한 값은:  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 및 클라이언트 쪽 커서  
버전 3.0에서에서 추가 된 클라이언트 쪽 커서를 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 메모리에 설정 하는 전체 결과 캐시할 수 있습니다. 장점은 쿼리를 실행 한 후 행 개수를 사용할 수 있는지입니다.  
  
소규모-결과 집합에 대 한 클라이언트 쪽 커서를 사용 해야 합니다. 큰 결과 집합은 서버측 커서를 사용 해야 합니다.  
  
쿼리는 버퍼가을 클라이언트 쪽 커서를 사용 하는 경우 설정 하는 전체 결과 저장할 만큼 큰 경우 false를 반환 합니다. PHP 메모리 제한까지 버퍼 크기를 늘릴 수 있습니다.  
  
결과 집합의 PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE 특성을 보유 하는 버퍼의 크기를 구성할 수 있습니다 [pdo:: setattribute](../../connect/php/pdo-setattribute.md) 하거나 [pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)합니다. Pdo_sqlsrv.client_buffer_max_kb_size 사용 하 여 php.ini 파일에서 최대 버퍼 크기를 설정할 수도 있습니다 (예를 들어 pdo_sqlsrv.client_buffer_max_kb_size = 1024)입니다.  
  
Pdo:: prepare 또는 pdostatement:: Setattribute를 사용 하 여 클라이언트 쪽 커서를 원하는 하 여 선택 된 pdo:: ATTR_CURSOR 나타냅니다 = > pdo:: CURSOR_SCROLL 커서 유형입니다.  Pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE 지정 = > PDO::SQLSRV_CURSOR_BUFFERED 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
[커서 유형 지정 및 행 선택](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
