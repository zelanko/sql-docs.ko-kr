---
title: getApplicationName 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aad921f5c496500d4f9dc5265568bf2956d8c41a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692911"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응용 프로그램 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>반환 값  
 응용 프로그램 이름이 들어 있는 **문자열**이며, 값이 설정되어 있지 않은 경우 “[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”입니다.  
  
## <a name="remarks"></a>Remarks  
 응용 프로그램 이름은 다양한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로파일링 및 로깅 도구에서 특정 응용 프로그램을 식별하는 데 사용됩니다. 응용 프로그램 이름이 설정되어 있지 않으면 getApplicationName 메서드는 지역화되지 않은 문자열인 “[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
