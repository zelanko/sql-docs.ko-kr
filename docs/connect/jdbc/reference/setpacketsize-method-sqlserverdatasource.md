---
title: setPacketSize 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e3affcbb2181cf8979196c65a0bcd81e58c541e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973277"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 네트워크 패킷 크기(바이트)를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *packetSize*  
  
 네트워크 패킷 크기가 들어 있는 **int** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 이 속성에 허용되는 값 범위는 [-1 | 0 | 512..32767]입니다. 이 속성을 허용 범위 이외의 값으로 설정하면 예외가 발생합니다.  
  
 애플리케이션에서는 SSL(Secure Sockets Layer) 암호화를 사용하여 연결되어 있는 동안 packetSize 속성을 설정할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 서버와 패킷 크기를 협상합니다. encrypt 속성이 “**true**”로 설정되어 있으며 협상된 패킷 크기가 JVM(Java Virtual Machine)의 기본 보안 공급자가 제공하는 SSL 레코드 크기보다 큰 경우에는 드라이버에서 오류가 발생하고 연결이 종료됩니다.  
  
 또한 애플리케이션에서 SSL 암호화를 요청하지 않고 packetSize 속성을 설정할 수도 있습니다. 이 경우 서버의 요구 사항에 따라 클라이언트에서 SSL 암호화를 지원해야 하면 드라이버에서는 JVM의 기본 보안 공급자가 제공하는 SSL 레코드 크기를 확인합니다. packetSize 속성이 JVM의 기본 보안 공급자가 제공하는 SSL 레코드 크기보다 크면 드라이버에서 오류가 발생하고 연결이 종료됩니다.  
  
 SSL을 사용하는 방법에 대한 자세한 내용은 [SSL 암호화 사용](../../../connect/jdbc/using-ssl-encryption.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
