---
title: "getConnection 메서드 (java.lang.String, java.lang.String) | Microsoft Docs"
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
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 39b7a3bb2896ff308fc58510443bd54c487c77f8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터와 연결을 설정 하려고 원본 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 지정 된 사용자 이름 및 암호를 사용 하 여 개체를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *사용자 이름*  
  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
 *암호*  
  
 A **문자열** 암호가 포함 된 합니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 getConnection 메서드는 javax.sql.DataSource 인터페이스의 getConnection 메서드에 의해 지정 됩니다.  
  
 Null이 아닌 사용자 이름이 나 암호를 사용 하 여 메서드 호출의 getConnection SQLServerConnection 개체를 초기화할 때 SQLServerDataSource 클래스에 설정 된 사용자 이름 및 암호 속성을 대체 됩니다. 예를 들어 호출자가 호출 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 및 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) 에서 데이터 원본 및 다음 호출 getConnection 및 공급 장치 null이 아닌 사용자 이름 또는 null이 아닌 암호, 사용자 이름 및 암호 설정 하 여 setUser 및 setPassword 사용자 이름 및 암호 getConnection에 전달 하 여 대체 됩니다.  
  
> [!NOTE]  
>  사용자 이름 및 암호에 대 한 호출을 사용 하 여 URL 내부에서 설정 되는 [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) 메서드가 경우 변경 되지 것입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getConnection 메서드 &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
