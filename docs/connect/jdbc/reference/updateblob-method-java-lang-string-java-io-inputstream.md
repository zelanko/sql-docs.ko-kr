---
title: updateBlob 메서드(java.lang.String, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 018cd71b-4b58-49a7-990e-d28dbb12da70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d669f4a675953b38bf0a14b4c3358c86f7f87b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637431"
---
# <a name="updateblob-method-javalangstring-javaioinputstream"></a>updateBlob 메서드(java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 입력 스트림을 사용하여 지정된 열을 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
 *inputStream*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateBlob 메서드는 java.sql.ResultSet 인터페이스의 updateBlob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBlob 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
