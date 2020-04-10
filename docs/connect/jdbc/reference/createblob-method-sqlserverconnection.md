---
title: createBlob 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 630a93b0-6e3c-4255-a007-1097ce0ee243
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fee6b9fd1143991d6b18a3eb4d84a534c103163d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927716"
---
# <a name="createblob-method-sqlserverconnection"></a>createBlob 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터가 없는 Blob 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Blob createBlob()  
```  
  
## <a name="return-value"></a>Return Value  
 Blob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 createBlob 메서드는 java.sql.Connection 인터페이스의 createBlob 메서드에 의해 지정됩니다.  
  
 이 메서드를 사용하면 [SQLServerBlob 생성자&#40;SQLServerConnection, byte&#41;](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md)를 사용할 필요가 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
