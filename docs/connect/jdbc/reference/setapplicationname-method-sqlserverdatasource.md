---
title: "setApplicationName 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dddba9b465d2b9bd2edfe42f850af6a3b64cd503
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
 A **문자열** 응용 프로그램의 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 응용 프로그램 이름은 다양 한 특정 응용 프로그램을 식별 하는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 프로 파일링 및 로깅 도구입니다. GetApplicationName 메서드 지역화 되지 않은 문자열을 반환 하는 경우 응용 프로그램 이름이 설정 되지 않은 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]"입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
