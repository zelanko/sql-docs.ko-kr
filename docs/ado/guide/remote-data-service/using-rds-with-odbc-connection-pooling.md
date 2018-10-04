---
title: RDS를 사용 하 여 ODBC 연결 풀링 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40efbdd80f5c6ba814936d952cba03cc7ac5b8ae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812201"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>ODBC 연결 풀링에서 RDS 사용
ODBC 데이터 소스를 사용 하는 경우의 연결 풀링 옵션에서 인터넷 정보 서비스 (IIS)를 사용 하 여 클라이언트 부하의 처리 성능을 향상 시킬 수 있습니다. 연결 풀링은 자주 사용 되는 연결에서 열려 있는 상태를 유지 관리 연결에 대 한 리소스에 대 한 관리자입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 연결 풀링을 사용 하려면 인터넷 정보 서비스 설명서를 참조 하십시오.  
  
 연결 풀링을 사용 하면 Microsoft 인터넷 정보 서비스 설명서에 설명 된 대로 웹 서버에 다른 제한을 설정할 수 있습니다 note 하십시오.  
  
 연결 풀링을 안정적 이며 추가 성능 향상을 제공 하도록 TCP/IP 소켓 네트워크 라이브러리를 사용 하려면 Microsoft SQL Server를 구성 해야 합니다.  
  
 이 작업을 수행 하려면을 지정 해야 합니다.  
  
-   TCP/IP 소켓을 사용 하도록 SQL Server 컴퓨터를 구성 합니다.  
  
-   TCP/IP 소켓을 사용 하도록 웹 서버를 구성 합니다.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>TCP/IP 소켓을 사용 하도록 SQL Server 컴퓨터를 구성 합니다.  
 SQL Server 컴퓨터에서 TCP/IP 소켓 네트워크 라이브러리를 사용 하 여 데이터 원본과 상호 작용 하는 SQL Server 설치 프로그램을 실행 합니다.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>SQL Server 컴퓨터의 TCP/IP 소켓 네트워크 라이브러리를 지정 하려면  
  
### <a name="in-microsoft-sql-server-65"></a>Microsoft SQL server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5, 가리키고 SQL 설치 프로그램을 클릭 합니다.  
  
2.  계속 하기를 두 번 클릭 합니다.  
  
3.  Microsoft SQL server에서-옵션 대화 상자 변경 네트워크 지원을 선택 하 고 계속을 클릭 합니다.  
  
4.  TCP/IP 소켓 확인란 선택 되어 있는지 확인 하 고 확인을 클릭 합니다.  
  
5.  완료 되는 데 계속을 클릭 하 고 설치를 종료 합니다.  
  
### <a name="in-microsoft-sql-server-70"></a>Microsoft SQL server 7.0:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 7.0 차례로 가리킨 다음 서버 네트워크 유틸리티를 클릭 합니다.  
  
2.  대화 상자의 일반 탭에서 추가 클릭 합니다.  
  
3.  네트워크 라이브러리 구성 추가 대화 상자에서 TCP/IP를 클릭 합니다.  
  
4.  포트 번호 및 프록시 주소 상자에서 네트워크 관리자가 제공 하는 포트 번호와 프록시 주소를 입력 합니다.  
  
5.  를 완료 하려면 확인을 클릭 하 고 설치를 종료 합니다.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>TCP/IP 소켓을 사용 하도록 웹 서버 구성  
 TCP/IP 소켓을 사용 하 여 웹 서버를 구성 하기 위한 두 가지 옵션이 있습니다. 모든 SQL Server 웹 서버에서 액세스 하는 여부에 따라 달라 집니다 여러분 또는 웹 서버에서 액세스 하는 특정 SQL Server만 합니다.  
  
 모든 SQL Server 웹 서버에서 액세스 하는 경우 웹 서버 컴퓨터에서 SQL Server 클라이언트 구성 유틸리티를 실행 해야 합니다. 다음 단계를 모든 SQL Server 연결에 대 한이 IIS 웹 서버에서 TCP/IP 소켓 네트워크 라이브러리를 사용 하 여 기본 네트워크 라이브러리를 변경 합니다.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>웹 서버 (모든 SQL Server)를 구성 하려면  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5, 가리키고 SQL 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  네트워크 라이브러리 탭을 클릭 합니다.  
  
3.  기본 네트워크 상자에서 TCP/IP 소켓을 선택 합니다.  
  
4.  변경 내용을 저장 하 고 유틸리티를 종료 완료를 클릭 합니다.  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0:  
  
1.  시작 메뉴에서 Microsoft SQL Server 7.0, 프로그램, 가리키고 클라이언트 네트워크 유틸리티를 클릭 합니다.  
  
2.  일반 탭을 클릭 합니다.  
  
3.  기본 네트워크 라이브러리 상자에서 TCP/IP를 클릭 합니다.  
  
4.  변경 내용을 저장 하 고 유틸리티를 종료 하려면 확인을 클릭 합니다.  
  
 특정 SQL Server 웹 서버에서 액세스 하는 경우 웹 서버 컴퓨터에서 SQL Server 클라이언트 구성 유틸리티를 실행 해야 합니다. 특정 SQL Server 연결에 대 한 네트워크 라이브러리를 변경 하려면 웹 서버 컴퓨터의 SQL Server Client 소프트웨어를 다음과 같이 구성 합니다.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>웹 서버 (특정 SQL Server)를 구성 하려면  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5, 가리키고 SQL 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  고급 탭을 클릭 합니다.  
  
3.  서버 상자에서 TCP/IP 소켓을 사용 하 여 연결할 서버의 이름을 입력 합니다.  
  
4.  DLL 이름 상자에서 TCP/IP 소켓을 선택 합니다.  
  
5.  추가/수정을 클릭 합니다. 이 서버를 가리키는 모든 데이터 원본 TCP/IP 소켓을 사용 합니다.  
  
6.  완료를 클릭 합니다.  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL server 7.0:  
  
1.  시작 메뉴에서 Microsoft SQL Server 7.0, 프로그램, 가리키고 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  일반 탭을 클릭 합니다.  
  
3.  추가를 클릭합니다.  
  
4.  서버 별칭 상자에 서버의 별칭을 입력 합니다. 네트워크 라이브러리 상자에서 TCP/IP를 클릭 합니다. 컴퓨터 이름 상자에 TCP/IP 소켓 클라이언트에 대 한 수신 대기 하는 컴퓨터의 컴퓨터 이름을 입력 합니다. 포트 번호 상자에 SQL Server는 수신 포트를 입력 합니다.  
  
5.  확인을 클릭 한 다음 확인 다시 유틸리티를 종료 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















