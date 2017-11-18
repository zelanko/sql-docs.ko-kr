---
title: "JDBC 드라이버에 대 한 대답 (FAQ) 질문과 대답 | Microsoft Docs"
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
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508f8526ed13af3f7f92aa500b182e077f5bb23d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>질문과 대답 (FAQ) JDBC 드라이버에 대 한
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 문서에서는 Microsoft JDBC Driver for SQL Server에 대한 자주 묻는 질문에 대한 답변을 제공합니다.  
  
## <a name="frequently-asked-questions"></a>질문과 대답  
**JDBC 드라이버를 향상 시킬 수 있습니다 어떻게 해야 합니까?**  
JDBC 드라이버는 오픈 소스 이며 소스 코드에서 확인할 수 있습니다 [GitHub](https://github.com/microsoft/mssql-jdbc)합니다. 코드 베이스에 기여 하 고 문제를 신고 하 여 드라이버를 향상 시킬 수 있습니다.

**드라이버가 어떤 버전의 SQL Server 및 Java를 지원 하나요?**  
 참조는 [Microsoft JDBC Driver for SQL Server 지원 매트릭스](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) 페이지 참조 합니다.  
  
 **내 드라이버를 업그레이드할 때 알고 있습니까?**  
 Microsoft JDBC 드라이버 6.2는 JDBC 4.0, 4.1 및 4.2 사양을 지원 하 고 다음과 같이 설치 패키지에 두 개의 JAR 클래스 라이브러리가 포함 합니다.  
  
|JAR|JDBC 사양|JDK 버전|  
|-|-|-|  
|mssql-jdbc-6.2.1.jre8.jar|JDBC 4.2, 4.1 및 4.0|JDK 8.0|  
|mssql-jdbc-6.2.1.jre7.jar|JDBC 4.1 및 4.0|JDK 7.0|  
 
 Microsoft JDBC Driver 6.0 및 4.2 for SQL Server JDBC 4.0, 4.1 및 4.2 사양을 지원 하며 다음과 같이 설치 패키지에 두 개의 JAR 클래스 라이브러리가 포함:  
  
|JAR|JDBC 사양|JDK 버전|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2, 4.1 및 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 및 4.0|JDK 7.0|  
  
 SQL Server 용 Microsoft JDBC Driver 4.1 JDBC 4.0 사양 한 지원 JAR 클래스 라이브러리를 하나 설치 패키지에 다음과 같이 합니다.  
  
|JAR|JDBC 사양|JDK 버전|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 및 6.0|
  
 Microsoft JDBC Driver 4.0 for SQL Server는 JDBC 3.0과 JDBC 4.0 사양을 모두 지원하며 설치 패키지에 각각 sqljdbc.jar 및 sqljdbc4.jar의 2개의 JAR 클래스 라이브러리가 포함되어 있습니다.  
  
|JAR|JDBC 사양|JDK 버전|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 및 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 및 5.0|  
  
 **최신 드라이버를 사용 하 여 기존 SQL Server 버전 내에 응용 프로그램에서 코드를 변경 해야 합니까?**  
 일반적으로 드라이버는 이전 버전과 호환되도록 설계되므로 드라이버를 업그레이드할 때 기존 응용 프로그램을 변경할 필요는 없습니다. 새 드라이버 버전에는 주요 변경 사항이 도입 하는 [JDBC 드라이버에 대 한 릴리스 정보](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) 섹션 변경 및 기존 응용 프로그램에 대 한 영향에 세부 정보가 제공 됩니다. 또한 드라이버에 포함된 릴리스 정보에서 해당 릴리스에서 수정된 버그 목록과 알려진 문제를 검토할 수 있습니다.  
  
 **드라이버의 비용은 얼마 입니까?**  
 Microsoft JDBC Driver for SQL Server는 추가 비용 없이 사용할 수 있습니다.  
  
 **드라이버를 재배포할 수 있나요?** JDBC Driver 4.1, 4.2, 6.0 및 6.2은 재배포 가능 합니다. 사용권 계약에서 "배포 가능 코드" 절을 검토 하십시오.
 
 JDBC Driver 4.0은 별도 재배포 라이선스 등록이 필요에 따라 무료로 재배포할 합니다. 등록 하거나 자세한 내용은 참조는 [Microsoft JDBC Driver를 재배포](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md)합니다. 
 
   
 **Linux 컴퓨터에서 Microsoft SQL Server에 액세스할 수는 드라이버를 사용할 수 있습니까?** 예 이 드라이버를 사용하여 Linux, Unix 및 기타 Windows 이외의 플랫폼에서 SQL Server에 액세스할 수 있습니다. 참조 우리의 [Microsoft JDBC Driver for SQL Server 지원 매트릭스](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) 내용을 확인 합니다.  
  
 **드라이버가 (SECURE Sockets Layer) 암호화를 지원 하나요?** 버전 1.2부터 이 드라이버는 SSL(Secure Sockets Layer) 암호화를 지원합니다. 자세한 내용은 참조 [SSL 암호화를 사용 하 여](../../connect/jdbc/using-ssl-encryption.md)합니다.  
  
 **SQL Server 용 Microsoft JDBC 드라이버에서 지원 되는 인증 유형은?**  
 다음 표에는서 사용할 수 있는 인증 옵션을 보여 줍니다. 이 드라이버 4.0 릴리스부터는 순수한 Java Kerberos 인증을 사용할 수 있습니다.  
  
|||  
|-|-|  
|플랫폼|인증|  
|비 Windows|순수 Java Kerberos|  
|비 Windows|SQL Server|  
|창|순수 Java Kerberos|  
|창|SQL Server|  
|창|NTLM 백업을 사용하는 Kerberos|  
|창|NTLM|  
  
**드라이버가 인터넷 프로토콜 버전 6 (IPv6)를 지원 하나요 주소?**  
 예, 이 드라이버는 연결 속성 컬렉션 및 serverName 연결 문자열 속성에 IPv6 주소를 사용하도록 지원합니다. 자세한 내용은 참조 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.  
  
**선택 버퍼링 하는 것이 무엇입니까?**  
 선택 버퍼링은 Microsoft SQL Server 2005 JDBC Driver 버전 1.2부터 도입되었으며 서버 커서의 오버헤드 없이 모든 유형의 큰 값 데이터를 검색하도록 설계되었습니다. Microsoft SQL Server JDBC Driver의 선택 버퍼링 기능은 "선택" 또는 "전체"로 설정될 수 있는 responseBuffering 연결 문자열 속성을 제공합니다. JDBC Driver 버전 2.0부터, 이 드라이버의 기본 동작은 "선택"입니다. 즉 선택 버퍼링을 사용하기 위해 응용 프로그램에서 명시적으로 선택 동작을 요청할 필요가 없습니다. 그러나 버전 1.2 릴리스에서는 버퍼링 모드가 기본적으로 "전체"이므로 응용 프로그램에서 명시적으로 선택 버퍼링 모드를 요청해야 했습니다. 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../connect/jdbc/using-adaptive-buffering.md) 항목 및 블로그 [어떤 버퍼링 이란 무엇 이며 왜 사용 해야 합니까?](http://go.microsoft.com/fwlink/?LinkId=111575)합니다.  
  
**드라이버는 연결 풀링을 지원 하나요?**  
 이 드라이버는 Java Platform, Enterprise Edition 5(Java EE 5) 연결 풀링을 지원합니다. 미들웨어 응용 프로그램 서버 공급업체가 제공하며 JDBC 3.0과 호환되는 모든 연결 풀링 구현에 참여할 수 있도록 드라이버는 JDBC 3.0 필수 인터페이스를 구현합니다. 이 드라이버는 이러한 환경에서 풀링된 연결에 참여합니다. 자세한 내용은 참조 [연결 풀링을 사용 하 여](../../connect/jdbc/using-connection-pooling.md)합니다. 이 드라이버는 자체 풀링 구현을 제공하지 않으며 타사 Java 응용 프로그램 서버에 의존합니다.  
  
**지원은 드라이버에 사용할 수 있는?**  
 몇 가지 지원 옵션을 사용할 수 있습니다. 질문을 게시 하거나를 발급할 수 있습니다이 [GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc) Microsoft에 의해 모니터링 되는 합니다. [포럼](http://go.microsoft.com/fwlink/?LinkID=246673) Microsoft, MVP 및 커뮤니티에서 모니터링 됩니다. Microsoft 고객 지원 서비스에 문의할 수도 있습니다. Microsoft 지원 서비스에서는 타사 응용 프로그램 서버 외부에서 발생하는 문제를 재현하도록 요청할 수도 있습니다. 호스팅 Java 컨테이너 환경 외부에서 발생하는 문제를 재현할 수 없는 경우 관련 타사에 문의해야만 계속 지원을 받을 수 있습니다. 최적의 도움을 주기 위해 Windows와 같은 운영 체제에서 문제를 재현하도록 요청될 수 있습니다.  
  
**드라이버는 타사 응용 프로그램 서버와 함께 사용 하도록 인증 되었는지?**
이 드라이버는 IBM WebSphere 및 SAP NetWeaver를 비롯한 다양한 응용 프로그램 서버에서 테스트되었습니다.  
  
**추적을 어떻게 사용 합니까?**  
 이 드라이버에서는 추적 또는 로깅 기능을 사용하여 응용 프로그램에서 사용되는 JDBC Driver 관련 문제를 해결할 수 있습니다. 클라이언트 쪽 JAR 추적을 사용으로 설정할 수 있도록 JDBC Driver는 java.util.logging의 로깅 API를 사용합니다. 자세한 내용은 참조 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)합니다. 서버 쪽 XA 추적에 대한 자세한 내용은 [SQL Server의 데이터 액세스 추적](http://go.microsoft.com/fwlink/?LinkId=248705)을 참조하세요.  
  
**이전 버전의 SQL Server 2000 JDBC driver, 2005 driver와 같은 드라이버를 다운로드할 수는 있는 1.0, 1.1 또는 1.2 driver?**  
 이러한 드라이버 버전은 더 이상 지원되지 않으므로 다운로드할 수 없습니다. Java 연결 지원을 지속적으로 개선하고 있습니다. 따라서 최신 버전의 JDBC 드라이버를 사용하여 작업하는 것이 좋습니다.  
  
 **JRE 1.4를 사용 합니다. 어떤 드라이버가 JRE 1.4와 호환 되** SAP 제품을 사용 하 고 JRE 1.4 지원이 필요한을 고객에 대 한 문의 [SAPService 마켓플레이스](http://service.sap.com/) 1.2 Microsoft JDBC driver를 가져올 수 있습니다.  
  
**드라이버가는 FIPS 유효성 검사 알고리즘을 사용 하 여 통신할 수 있습니까?** Microsoft JDBC Driver에는 암호화 알고리즘이 포함되어 있지 않습니다. 고객이 FIPS(Federal Information Processing Standards)에서 허용될 수 있는 운영 체제, 응용 프로그램 및 JVM 알고리즘을 활용하며 해당 알고리즘을 사용하도록 드라이버를 구성하는 경우 해당 드라이버는 지정된 알고리즘만 통신에 사용합니다.  
  
  

