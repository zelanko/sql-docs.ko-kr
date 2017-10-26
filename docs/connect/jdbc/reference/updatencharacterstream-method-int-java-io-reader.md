---
title: "updateNCharacterStream 메서드 (int, java.io.Reader) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03460e0fc6529ac01fff341c0082ab886bd11e16
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatencharacterstream-method-int-javaioreader"></a>updateNCharacterStream 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *x*  
  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateNCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 판독기 개체를 유니코드 문자를 전달 **nchar**, **nvarchar (max)**, **ntext** 및 **xml** 열입니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateNCharacterStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

