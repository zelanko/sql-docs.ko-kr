---
title: updateAsciiStream 메서드(java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1dcc3d4f-ae30-45c0-afad-a531358807af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9acd8b75a7152a8e10faeb7f80d6d02c070ad2f0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67985509"
---
# <a name="updateasciistream-method-int-javaioinputstream"></a>updateAsciiStream 메서드(int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 ASCII 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateAsciiStream 메서드는 java.sql.ResultSet 인터페이스의 updateAsciiStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 InputStream 개체의 ASCII 문자(바이트)를 변환 가능한 문자 열에 전달합니다. 이러한 열은 유니코드의 ASCII 범위 [0x00 – 0x7F]와 874, 932, 936, 949, 950, 1250-1258 코드 페이지입니다. 이 메서드는 대상 데이터 정렬 페이지에 대한 변환을 수행합니다. 변환할 수 없는 대상 열을 업데이트하려고 하면 예외가 발생합니다. 이진 열의 경우 원시 바이트가 전달됩니다.  
  
 **image**, **text** 및 **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 이 메서드를 사용할 경우 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateAsciiStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
