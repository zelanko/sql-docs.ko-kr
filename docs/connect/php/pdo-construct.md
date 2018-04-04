---
title: ':: __Construct | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a1c40e8e31cbba9eb93155c3f81f6dd03452b59
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 대한 연결을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$dsn*: 접두사 이름을 포함 하는 문자열 (항상 `sqlsrv`), 콜론 및 서버 키워드입니다. `"sqlsrv:server=(local)"`)을 입력합니다. 필요에 따라 다른 연결 키워드를 지정할 수 있습니다. 서버 키워드 및 다른 연결 키워드에 대한 설명은 [Connection Options](../../connect/php/connection-options.md) 를 참조하세요. 전체 *$dsn* 가 따옴표 안에 있으므로 각 연결 키워드를 각각 따옴표로 묶으면 안 됩니다.  
  
*$username*: 선택 사항입니다. 사용자 이름을 포함하는 문자열입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증을 사용하여 연결하려면 로그인 ID를 지정합니다. Windows 인증을 사용하여 연결하려면 `""`를 지정합니다.  
  
*$password*: 선택 사항입니다. 사용자의 암호를 포함하는 문자열입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증을 사용하여 연결하려면 암호를 지정합니다. Windows 인증을 사용하여 연결하려면 `""`를 지정합니다.  
  
*$driver_options*: 선택 사항입니다. PDO 드라이버 관리자 특성을 지정할 수 있습니다 및 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 관련 드라이버 특성 pdo:: SQLSRV_ATTR_ENCODING, pdo:: SQLSRV_ATTR_DIRECT_QUERY 합니다. 잘못 된 특성이 예외를 생성 하지 않습니다. [PDO::setAttribute](../../connect/php/pdo-setattribute.md)로 지정되면 잘못된 특성이 예외를 생성합니다.  
  
## <a name="return-value"></a>반환 값  
PDO 개체를 반환합니다. 실패하는 경우 PDOException 개체를 반환합니다.  
  
## <a name="exceptions"></a>예외  
PDOException  
  
## <a name="remarks"></a>주의  
인스턴스를 null로 설정하여 연결 개체를 닫을 수 있습니다.  
  
연결 되 면 pdo:: errorcode는 00000 대신 01000을 표시합니다.  
  
:: __Construct 어떤 이유로 든 실패 하면 pdo:: ATTR_ERRMODE가 pdo:: ERRMODE_SILENT로 설정 된 경우에 예외가 throw 됩니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제는 Windows 인증을 사용하여 서버에 연결하고 데이터베이스를 지정하는 방법을 보여 줍니다.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>예제  
이 예제는 서버에 연결하여 나중에 데이터베이스를 지정하는 방법을 보여 줍니다.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
