---
title: updateSQLXML 메서드(java.lang.String, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac198bb6b235768eb6c6223dc7cddfc93ff9b9ae
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919613"
---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>updateSQLXML 메서드(java.lang.String, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 java.sql.SQLXML 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블을 나타내는 **문자열**입니다.  
  
 *xmlObject*  
  
 SQLXML 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateSQLXML 메서드는 java.sql.ResultSet 인터페이스의 updateSQLXML 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateSQLXML 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
