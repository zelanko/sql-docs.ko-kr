---
title: updateBinaryStream 메서드 (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3682c8418ff107eb7ef7a7c91797a9d859a5f1d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>주의  
 이 updateBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 메서드를 사용 하는 **이미지**, **텍스트**, 및 **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식을 성능 영향을 줄 수 있습니다.  
  
 이 메서드를 선택 InputStream 개체에서 바이트 전달 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binary, varbinary, varbinary (max), 이미지, xml 및 udt 등의 이진 열입니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 프로그램 InputStream를 업데이트 하려면 사용 하 여는 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [updateBinaryStream 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
