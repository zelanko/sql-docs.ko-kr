---
title: updateBinaryStream 메서드(int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c0106d85f00bf406f8b79b1df3c6562fd56e7ae
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925561"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>updateBinaryStream 메서드(int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 이진 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBinaryStream(int columnIndex,  
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
 이 updateBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정됩니다.  
  
 **image**, **text** 및 **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 이 메서드를 사용할 경우 성능이 저하될 수 있습니다.  
  
 이 메서드는 InputStream 개체의 바이트를 binary, varbinary, varbinary(max), image, xml, udt와 같은 선택된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이진 열에 전달합니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 InputStream으로 업데이트하려면 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
