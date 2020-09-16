---
description: isCurrency 메서드(SQLServerResultSetMetaData)
title: isCurrency 메서드(SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7fe25d90-693c-4d3b-9dd2-0f8351c5a9ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b5c127dab64cfd77599fb9f2dfb50b4605c64e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433665"
---
# <a name="iscurrency-method-sqlserverresultsetmetadata"></a>isCurrency 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열이 현금 값인지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isCurrency(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 열이 현금 값이면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 isCurrency 메서드는 java.sql.ResultSetMetaData 인터페이스의 isCurrency 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] money 및 smallmoney 데이터 형식에 대해서만 **true**를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
