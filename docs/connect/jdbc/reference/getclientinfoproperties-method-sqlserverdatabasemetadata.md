---
description: getClientInfoProperties 메서드(SQLServerDatabaseMetaData)
title: getClientInfoProperties 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a013bdc53a5699ba01accf5629326df7929e798
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436715"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Return Value  
 ResultSet 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getClientInfoProperties 메서드는 java.sql.DatabaseMetaData 인터페이스의 getClientInfoProperties 메서드에 의해 지정됩니다.  
  
> [!NOTE]  
>  이 메서드는 빈 결과 집합을 반환합니다. 드라이버에서는 **applicationName**을 설정하는 것만 지원하며, 연결 시에만 **applicationName**을 설정합니다. SQL Server에서는 연결이 설정된 후 클라이언트 애플리케이션 정보에 대한 업데이트를 지원하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
