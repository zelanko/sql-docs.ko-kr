---
title: getConnection 메서드(java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f72babc3375c0720807322520a9761cb49e05919
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677467"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 사용자 이름 및 암호를 사용하여 이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체가 나타내는 데이터 원본과의 연결을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *username*  
  
 사용자 이름을 포함하는 **문자열**입니다.  
  
 *password*  
  
 암호가 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 getConnection 메서드는 javax.sql.DataSource 인터페이스의 getConnection 메서드에 의해 지정 됩니다.  
  
 Null이 아닌 사용자 이름이 나 암호를 사용 하 여 메서드 호출의 getConnection SQLServerConnection 개체를 초기화할 때 SQLServerDataSource 클래스에 설정 된 사용자 이름 및 암호 속성을 대체 됩니다. 예를 들어 호출자가 데이터 원본에 대해 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 및 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)를 호출한 다음, getConnection을 호출하고 null이 아닌 사용자 이름이나 null이 아닌 암호를 제공하면 setUser 및 setPassword로 설정된 사용자 이름과 암호는 getConnection에 전달된 사용자 이름 및 암호로 대체됩니다.  
  
> [!NOTE]  
>  [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) 메서드를 호출하여 URL 내부에서 설정된 사용자 이름 및 암호는 이 경우에도 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getConnection 메서드(SQLServerDataSource)](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
