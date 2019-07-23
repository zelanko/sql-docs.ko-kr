---
title: updateNString 메서드 (int, java. lang) | Microsoft Docs
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
ms.openlocfilehash: 90aa44eda2af60ffdc73a65e01b3ae12b949d79f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998800"
---
# <a name="updatenstring-method-int-javalangstring"></a>updateNString 메서드(int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열 인덱스를 사용하여 지정된 열을 **문자열** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNString(int columnIndex,  
                        java.lang.String nString)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *nString*  
  
 **문자열** 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateNString 메서드는 java.sql.ResultSet 인터페이스의 updateNString 메서드에 의해 지정됩니다.  
  
 이 메서드는 Java **문자열** 을 선택한 **nchar**, **nvarchar (max)** , **ntext**및 **xml** 열에 전달 합니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateNString 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
