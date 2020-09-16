---
description: getNCharacterStream 메서드(int)(SQLServerResultSet)
title: getNCharacterStream 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1cfa4e4-3e1f-4504-b0de-cc626d653661
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78d94536a297d28c1a181c165b6ceda39456d9aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435365"
---
# <a name="getncharacterstream-method-int-sqlserverresultset"></a>getNCharacterStream 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열의 값을 Reader 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getNCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 getNCharacterStream 메서드에 의해 지정됩니다.  
  
 이 메서드를 사용하여 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 **nvarchar**, **nchar**, **nvarchar(max)**, **ntext** 또는 **xml** 열의 값을 검색할 수 있습니다. 이 메서드를 사용하여 다른 데이터 형식의 값을 검색하려고 하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNCharacterStream 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
