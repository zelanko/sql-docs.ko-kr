---
title: updateAsciiStream 메서드(java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e7386586aec57e379ae66abe48ddcda09aef0bcb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922925"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>updateAsciiStream 메서드(java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 ASCII 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
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
  
  
