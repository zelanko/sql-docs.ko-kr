---
title: "setTrustStorePassword 메서드 (SQLServerDataSource) | Microsoft Docs"
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
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d42539e3a0979500c28539d256226624ac6997eb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustStore 데이터의 무결성을 검사하는 데 사용되는 암호를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *trustStorePassword*  
  
 A **문자열** trustStore 데이터의 무결성을 확인 하는 데 사용 되는 암호를 포함 하 합니다.  
  
## <a name="remarks"></a>주의  
 trustStorePassword 속성은 trustStore 속성과 함께 지정할 수 있으며 해당 값을 사용하여 trustStore 파일의 무결성을 검사합니다.  
  
 trustStore 속성은 설정되어 있지만 trustStorePassword 속성이 설정되어 있지 않는 경우 trustStore의 무결성을 검사하지 않습니다.  
  
 trustStore 속성과 trustStorePassword 속성이 모두 지정되어 있지 않는 경우 드라이버에서 JVM(Java Virtual Machine) 시스템 속성 "javax.net.ssl.trustStore" 및 "javax.net.ssl.trustStorePassword"를 사용합니다. "javax.net.ssl.trustStorePassword" 시스템 속성이 지정되어 있지 않는 경우 trustStore의 무결성을 검사하지 않습니다.  
  
 trustStore 속성은 설정되어 있지 않지만 trustStorePassword 속성이 설정되어 있는 경우 JDBC 드라이버에서는 "javax.net.ssl.trustStore"에 지정된 파일을 트러스트 저장소로 사용하여 지정된 trustStorePassword로 트러스트 저장소의 무결성을 검사합니다. 클라이언트 응용 프로그램이 JVM 시스템 속성에 암호를 저장하지 않는 경우 이 방법이 필요할 수 있습니다.  
  
 자세한 내용은 참조 [연결 속성을 설정할](../../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 JDBC 드라이버 3.0부터는 데이터 원본 속성을 바인딩하기 전에 SQLServerDataSource.setTrustStorePassword를 설정할 경우, 연결을 가져오기 전에 SQLServerDataSource.setTrustStorePassword를 호출해야 합니다. 자세한 내용은 참조 [SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
