---
title: "연결 문제 해결 | Microsoft Docs"
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
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4adcdafe8b82a8b35dbb9b27c15749673a56bce2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="troubleshooting-connectivity"></a>연결 문제 해결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] TCP/IP 하 해야 설치 하 고 실행와 통신 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구성 관리자를 설치 된 네트워크 라이브러리 프로토콜을 확인 합니다.  
  
 데이터베이스 연결 시도가 실패하는 데는 여러 가지 이유가 있습니다. 예를 들면 다음과 같습니다.  
  
-   TCP/IP 사용 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 또는 지정 된 서버 또는 포트 번호가 올바르지 않습니다. 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 지정 된 서버 및 포트에서 TCP/IP로 수신 대기 합니다. 이 경우 "로그인에 실패했습니다. 호스트에 TCP/IP 연결을 설정하지 못했습니다."와 유사한 예외가 함께 보고됩니다. 이는 다음 중 하나를 나타냅니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]가 설치 되어 TCP/IP에 대 한 네트워크 프로토콜로 설치 되지 않은 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 사용 하 여는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 용 네트워크 유틸리티 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager에 대 한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 이상.  
  
    -   로 설치 된 TCP/IP는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 프로토콜을 하지만 JDBC 연결 URL에 지정 된 포트에서 수신 하지 않는 합니다. 기본 포트는 1433 이지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 설치 시 임의의 포트에서 수신 하도록 구성할 수 있습니다. 다음 사항을 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 포트 1433에서 수신 합니다. 또는 포트를 변경한 경우 JDBC 연결 URL에 지정된 포트가 변경된 포트와 일치하는지 확인합니다. JDBC 연결 Url에 대 한 자세한 내용은 참조 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.  
  
    -   JDBC 연결에 지정 된 컴퓨터의 주소 URL 서버를 참조 하지 않는 여기서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설치 되어 시작 되었습니다.  
  
    -   TCP/IP 네트워킹 작업을 실행 중인 서버와 클라이언트 간의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 작동 하지 않습니다. TCP/IP 연결을 확인할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 텔넷을 사용 하면 됩니다. 예를 들어 명령 프롬프트에 입력 `telnet 192.168.0.0 1433` 192.168.0.0는 실행 중인 컴퓨터의 주소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 수신 대기 포트는 1433입니다. TCP/IP에 대 한 해당 포트에서 수신 하지 않는 "텔넷 연결할 수 없습니다." 메시지가 표시 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결 합니다. 사용 하 여는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 용 네트워크 유틸리티 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager에 대 한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 나중에 있는지 확인 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 포트 1433에서 TCP/IP를 사용 하도록 구성 됩니다.  
  
    -   서버에서 사용하는 포트가 방화벽에서 열려 있지 않습니다. 서버에서 사용하는 포트이거나 명명된 서버 인스턴스와 관련된 포트(옵션)가 이에 해당합니다.  
  
-   지정한 데이터베이스 이름이 잘못되었습니다. 기존에 로그인 되어 있는지 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
-   사용자 이름 또는 암호가 정확하지 않습니다. 값이 정확한지 확인합니다.  
  
-   사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 하는 인증, JDBC 드라이버에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 함께 설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증의 기본 설정인 합니다. 이 옵션을 설치 하거나의 인스턴스를 구성할 때 포함 되어 있는지 확인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

