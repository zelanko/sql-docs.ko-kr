---
title: updateBinaryStream 메서드(java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3557c60f36ea48a8cb03f58997bc2d8093f432e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787304"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>updateBinaryStream 메서드(java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 이진 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 메서드를 사용 하는 **이미지**를 **텍스트**, 및 **ntext** SQL Server 데이터 형식 성능 영향을 줄 수 있습니다.  
  
 이 메서드는 InputStream 개체의 바이트를 binary, varbinary, varbinary(max), image, xml, udt와 같은 선택된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이진 열에 전달합니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 InputStream으로 업데이트하려면 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
