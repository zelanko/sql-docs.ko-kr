---
title: PDO::errorInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe0f0cc2ec15fcdb871f290f03565482a8477995
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936264"
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

데이터베이스 핸들에서 최근 작업의 확장된 오류 정보를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>Return Value  
데이터베이스 핸들에서 최근 작업에 대한 오류 정보입니다. 배열은 다음 필드로 구성됩니다.  
  
-   SQLSTATE 오류 코드입니다.  
  
-   드라이버별 오류 코드입니다.  
  
-   드라이버별 오류 메시지입니다.  
  
오류가 없거나 SQLSTATE가 설정되지 않은 경우 드라이버 관련 필드는 NULL입니다.  
  
## <a name="remarks"></a>설명  
PDO::errorInfo는 데이터베이스에서 직접 수행된 작업에 대한 오류 정보만 검색합니다. PDO::prepare 또는 PDO::query를 사용하여 PDOStatement 인스턴스가 만들어질 때 PDOStatement::errorInfo를 사용합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 열 이름의 철자가 잘못되어(`Cityx`가 아닌 `City`) 오류가 발생하므로 보고됩니다.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
