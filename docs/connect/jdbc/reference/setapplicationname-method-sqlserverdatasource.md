---
title: setApplicationName 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3853262dd5e1a62542387e9b61f8c30f5967f09b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210592"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응용 프로그램 이름을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *applicationName*  
  
 애플리케이션 이름이 포함된 **문자열**입니다.  
  
## <a name="remarks"></a>Remarks  
 애플리케이션 이름은 다양한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로파일링 및 로깅 도구에서 특정 애플리케이션을 식별하는 데 사용됩니다. 애플리케이션 이름이 설정되어 있지 않으면 getApplicationName 메서드는 지역화되지 않은 문자열인 “[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]”를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
