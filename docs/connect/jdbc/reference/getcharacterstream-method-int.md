---
title: "getCharacterStream 메서드 (int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.getCharacterStream (int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f345dc0fe0c52b4c70d280fbbd6c893095dbf36c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getcharacterstream-method-int"></a>getCharacterStream 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 java.io.Reader 개체로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 getCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 읽기 전용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nchar, nvarchar, nvarchar (max), 및 ntext와 같은 유니코드 문자 데이터 형식입니다. ASCII 문자 형식을 비롯한 다른 모든 데이터 형식에서는 예외가 발생합니다. ASCII 데이터 형식을 읽으려면, 사용 된 [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [getCharacterStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
