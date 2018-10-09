---
title: updateNClob 메서드(java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 338a2bf2-b110-469d-ad08-a0f2bbefcb88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f58bee8fa6bc36ea7bae17ee6f432a26b7c288ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799081"
---
# <a name="updateclob-method-javalangstring-javaioreader"></a>updateClob 메서드(java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 Reader 개체를 사용하여 지정된 열을 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
 *reader*  
  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateClob 메서드는 java.sql.ResultSet 인터페이스의 updateClob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateNClob 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
