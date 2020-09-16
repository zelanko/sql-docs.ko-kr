---
description: updateBlob 메서드(java.lang.String, java.io.InputStream)
title: updateBlob 메서드(java.lang.String, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 018cd71b-4b58-49a7-990e-d28dbb12da70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 701fb7df5f8c9632d139357021fb8793551f5147
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462323"
---
# <a name="updateblob-method-javalangstring-javaioinputstream"></a>updateBlob 메서드(java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 입력 스트림을 사용하여 지정된 열을 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
 *inputStream*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateBlob 메서드는 java.sql.ResultSet 인터페이스의 updateBlob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBlob 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
