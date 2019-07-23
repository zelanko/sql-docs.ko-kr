---
title: 커서 형식(PDO_SQLSRV 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c62c2a35123e77f5366dd5348fd51b3c50c85605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993692"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>커서 형식(PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO_SQLSRV 드라이버를 사용하면 여러 커서 중 하나가 있는 스크롤 가능 결과 집합을 만들 수 있습니다.

PDO_SQLSRV 드라이버를 사용하여 커서를 지정하는 방법에 대한 자세한 내용과 코드 샘플은 [PDO::prepare](../../connect/php/pdo-prepare.md)를 참조하세요.

## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV 및 서버 쪽 커서
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 3.0 이전에는 PDO_SQLSRV 드라이버를 사용하여 서버 쪽 정방향 전용 또는 정적 커서가 있는 결과 집합을 만들 수 있었습니다. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 3.0부터 키 집합과 동적 커서도 사용할 수 있습니다.

[PDO::prepare](../../connect/php/pdo-prepare.md)를 사용해서 다음 커서 형식 중 하나를 선택하여 서버 쪽 커서 형식을 나타낼 수 있습니다.

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`을 지정하고 적절한 값을 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`에 전달하여 동적, 정적 또는 키 집합 커서를 요청할 수 있습니다. 서버 쪽 커서에 대해 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`에 전달할 수 있는 값은 다음과 같습니다.

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV 및 클라이언트 쪽 커서
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 3.0에서 추가된 클라이언트 쪽 커서를 사용하면 전체 결과 집합을 메모리에 캐시할 수 있습니다. 한 가지 장점은 쿼리를 실행한 후 행 개수가 제공된다는 것입니다.

클라이언트 쪽 커서는 중소 규모의 결과 집합에 사용해야 합니다. 대규모 결과 집합은 서버 쪽 커서를 사용해야 합니다.

클라이언트 쪽 커서를 사용하는 경우 버퍼가 전체 결과 집합을 저장할 만큼 크지 않으면 쿼리에서 false가 반환됩니다. PHP 메모리 한도까지 버퍼 크기를 늘릴 수 있습니다.

[PDO::setAttribute](../../connect/php/pdo-setattribute.md) 또는 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md)의 `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` 특성을 사용하여 결과 집합이 저장되는 버퍼 크기를 구성할 수 있습니다. Pdo_sqlsrv.client_buffer_max_kb_size를 사용하여 php.ini 파일에서 최대 버퍼 크기를 설정할 수도 있습니다(예: pdo_sqlsrv.client_buffer_max_kb_size = 1024).

[PDO::prepare](../../connect/php/pdo-prepare.md)를 사용하고 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 커서 형식을 지정한 다음, `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`를 지정하여 클라이언트 쪽 커서를 요청할 수 있습니다.

## <a name="example"></a>예제
다음 예제에서는 버퍼링된 커서를 지정하는 방법을 보여 줍니다.
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

