---
title: 연결 문제 해결
description: Microsoft JDBC Driver for SQL Server를 사용하는 경우 JDBC 연결 및 잠재적인 연결 문제를 해결하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12abdfd169aaea9f2108d2b4776eb99cc4bd2ce7
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728386"
---
# <a name="troubleshooting-connectivity"></a>연결 문제 해결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 TCP/IP를 설치하고 실행해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 통신할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하면 설치된 네트워크 라이브러리 프로토콜을 확인할 수 있습니다.  
  
 데이터베이스 연결 시도가 실패하는 데는 여러 가지 이유가 있습니다. 예를 들면 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 TCP/IP를 사용하고 있지 않거나 지정한 서버 또는 포트 번호가 잘못되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지정한 서버 및 포트에서 TCP/IP로 수신 대기 중인지 확인합니다. 이 경우 “로그인에 실패했습니다. 호스트에 TCP/IP 연결을 설정하지 못했습니다."와 유사한 예외가 함께 보고됩니다. 이는 다음 중 하나를 나타냅니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되어 있지만 TCP/IP가 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 유틸리티 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 네트워크 프로토콜로 설치되어 있지 않습니다.  
  
    -   TCP/IP가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로토콜로 설치되어 있지만 JDBC 연결 URL에 지정한 포트에서 수신 대기하고 있지 않습니다. 기본 포트는 1433이지만 제품 설치 시 임의의 포트에서 수신 대기하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 포트 1433에서 수신 대기 중인지 확인합니다. 또는 포트를 변경한 경우 JDBC 연결 URL에 지정된 포트가 변경된 포트와 일치하는지 확인합니다. JDBC 연결 URL에 대한 자세한 내용은 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)을 참조하세요.  
  
    -   JDBC 연결 URL에 지정한 컴퓨터 주소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되어 실행되는 서버를 가리키지 않습니다.  
  
    -   클라이언트와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 서버 간에 TCP/IP 네트워킹 작업을 수행할 수 없습니다. 텔넷을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 TCP/IP 연결을 확인할 수 있습니다. 예를 들어, 명령 프롬프트에서 192.168.0.0이 `telnet 192.168.0.0 1433`를 실행하는 컴퓨터의 주소이고 1433이 컴퓨터가 수신 대기하는 포트인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 입력합니다. “텔넷으로 연결할 수 없습니다.”라는 메시지가 나타나면 TCP/IP가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 위해 해당 포트에서 수신 대기하고 있지 않다는 뜻입니다. 그러면 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 유틸리티 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 포트 1433에서 TCP/IP를 사용하도록 구성합니다.  
  
    -   서버에서 사용하는 포트가 방화벽에서 열려 있지 않습니다. 서버에서 사용하는 포트이거나 명명된 서버 인스턴스와 관련된 포트(옵션)가 이에 해당합니다.  
  
-   지정한 데이터베이스 이름이 잘못되었습니다. 기존의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 로그인되어 있는지 확인합니다.  
  
-   사용자 이름 또는 암호가 정확하지 않습니다. 값이 정확한지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하려면 JDBC 드라이버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증과 함께 설치해야 합니다. 이 인증은 기본적으로 설치되지 않습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하거나 구성할 때 이 옵션을 반드시 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 관련 문제 진단](diagnosing-problems-with-the-jdbc-driver.md)   
 [JDBC 드라이버로 SQL Server에 연결](connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
