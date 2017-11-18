---
title: "setPacketSize 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9684140ed084cc7a096675935ceec81209f8fa66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  와 통신 하는 데 사용 되는 현재 네트워크 패킷 크기 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], 바이트 단위로 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *패킷 크기*  
  
 **int** 네트워크 패킷 크기를 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 이 속성에 허용되는 값 범위는 [-1 | 0 | 512..32767]입니다. 이 속성을 허용 범위 이외의 값으로 설정하면 예외가 발생합니다.  
  
 응용 프로그램에서는 SSL(Secure Sockets Layer) 암호화를 사용하여 연결되어 있는 동안 packetSize 속성을 설정할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 서버와 패킷 크기를 협상 합니다. Encrypt 속성이로 설정 되어 있으면 "**true**" 및 협상 된 패킷 크기는 가상 컴퓨터 JVM (Java)의 기본 보안 공급자는 SSL 레코드 크기 보다 크면, 드라이버에서 오류가 발생 하 고 연결이 종료 됩니다.  
  
 또한 응용 프로그램에서 SSL 암호화를 요청하지 않고 packetSize 속성을 설정할 수도 있습니다. 이 경우 서버의 요구 사항에 따라 클라이언트에서 SSL 암호화를 지원해야 하면 드라이버에서는 JVM의 기본 보안 공급자가 제공하는 SSL 레코드 크기를 확인합니다. packetSize 속성이 JVM의 기본 보안 공급자가 제공하는 SSL 레코드 크기보다 크면 드라이버에서 오류가 발생하고 연결이 종료됩니다.  
  
 SSL을 사용 하는 방법에 대 한 자세한 내용은 참조 [SSL 암호화를 사용 하 여](../../../connect/jdbc/using-ssl-encryption.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

