---
title: getClientInfoProperties 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bf9c0696c2169ee9b0dd1af198fcb50333c5d9ca
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763765"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  드라이버에서 지원하는 클라이언트 정보 속성의 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>반환 값  
 ResultSet 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getClientInfoProperties 메서드는 java.sql.DatabaseMetaData 인터페이스의 getClientInfoProperties 메서드에 의해 지정 됩니다.  
  
> [!NOTE]  
>  이 메서드는 빈 결과 집합을 반환합니다. 드라이버 설정에 지원 합니다 **applicationName** 설정 합니다 **applicationName** 연결 시에만. SQL Server에서는 연결이 설정된 후 클라이언트 응용 프로그램 정보에 대한 업데이트를 지원하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
