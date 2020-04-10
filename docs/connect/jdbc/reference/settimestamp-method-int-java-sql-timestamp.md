---
title: setTimestamp 메서드(int, java.sql.Timestamp) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f7bb89f-ace7-41cb-b596-5aa8d0dd9e3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 023ec113704b9b602049f5ae707d08fe742020e6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926505"
---
# <a name="settimestamp-method-int-javasqltimestamp"></a>setTimestamp 메서드(int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 타임스탬프 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 Timestamp 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setTimestamp 메서드는 java.sql.PreparedStatement 인터페이스의 setTimestamp 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setTimestamp 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
