---
title: 'Pdo:: getavailabledrivers | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 251d81d568f3ade2a843d3288cb9bc92fdb8bc41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PHP를 설치하는 동안 PDO 드라이버의 배열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>반환 값  
PDO 드라이버의 목록을 사용하는 배열입니다.  
  
## <a name="remarks"></a>주의  
PDO 인스턴스를 만드는 데 PDO 드라이버의 이름이 PDO::__construct로 사용됩니다.  
  
PDO::getAvailableDrivers는 PHP 드라이버에서 구현될 필요가 없습니다. 이 메서드에 대한 자세한 내용은 PHP 설명서를 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
