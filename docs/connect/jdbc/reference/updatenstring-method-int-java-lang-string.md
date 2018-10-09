---
title: updateNString 메서드 (int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1bb909f1-4a96-4be1-adea-36c8d9703112
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b307dd027f45c54d6bd00dfc5614c12ad496544a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834131"
---
# <a name="updatenstring-method-int-javalangstring"></a>updateNString 메서드(int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열 레이블을 사용하여 지정된 열을 **String** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNString(int columnIndex,  
                        java.lang.String nString)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *항목이*  
  
 A **문자열** 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateNString 메서드는 java.sql.ResultSet 인터페이스의 updateNString 메서드에 의해 지정 됩니다.  
  
 이 메서드는 Java 전달 **문자열** 를 선택한 **nchar**를 **nvarchar (max)** 를 **ntext**, 및 **xml** 열입니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateNString 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
