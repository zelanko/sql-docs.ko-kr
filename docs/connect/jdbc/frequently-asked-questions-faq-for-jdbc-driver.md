---
title: JDBC 드라이버에 대한 FAQ(질문과 대답) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2860034ae67fc7cc376e84251dbeebc5a123fade
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028068"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>JDBC 드라이버에 대한 FAQ(질문과 대답)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 페이지에서는 Microsoft JDBC Driver for SQL Server에 대한 자주 묻는 질문에 대한 답변을 제공합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

**JDBC Drive 향상에 도움을 주려면 어떻게 해야 하나요?**  
JDBC Driver는 오픈 소스이며 소스 코드는 [GitHub](https://github.com/microsoft/mssql-jdbc)에서 찾을 수 있습니다. 문제를 신고하고 코드베이스에 기여하여 드라이버 향상에 도움을 줄 수 있습니다.

**드라이버가 어떤 버전의 SQL Server 및 Java를 지원하나요?**  
자세한 내용은 [Microsoft JDBC Driver for SQL Server 지원 매트릭스](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md) 페이지를 참조하세요.

**Microsoft 다운로드 센터에서 사용할 수 있는 JDBC Driver 패키지와 GitHub에서 사용할 수 있는 JDBC Driver의 차이점은 무엇인가요?**  
Microsoft JDBC Driver용 GitHub 리포지토리에서 사용할 수 있는 JDBC Driver 파일은 JDBC Driver의 핵심이며 리포지토리에 나열된 오픈 소스 라이선스가 적용됩니다. Microsoft 다운로드 센터의 드라이버 패키지에는 Windows 통합 인증에 필요하고 JDBC 드라이버에서 XA 트랜잭션을 사용하도록 설정하기 위해 필요한 추가 라이브러리가 포함됩니다. 이러한 추가 라이브러리에는 다운로드 가능한 패키지에 포함되는 라이선스가 적용됩니다.

**내 드라이버를 업그레이드할 때 어떤 정보를 알아야 하나요?**
Microsoft JDBC Driver 7.4는 JDBC 4.2 및 4.3(부분) 사양을 지원하며 설치 패키지에 다음과 같은 세 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR                        | JDBC 사양            | JDK 버전 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.4.1. jre12 | JDBC 4.3(부분) 및 4.2 | JDK 12.0    |
| mssql-jdbc-7.4.1. jre11 | JDBC 4.3(부분) 및 4.2 | JDK 11.0    |
| mssql-jdbc-7.4.1. jre8  | JDBC 4.2                      | JDK 8.0     |

 Microsoft JDBC Driver 7.2는 JDBC 4.2 및 4.3(부분) 사양을 지원하며 설치 패키지에 다음과 같은 두 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR                        | JDBC 사양            | JDK 버전 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3(부분) 및 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

 Microsoft JDBC Driver 7.0은 JDBC 4.2 및 4.3(부분) 사양을 지원하며 설치 패키지에 다음과 같은 두 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR                        | JDBC 사양            | JDK 버전 |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3(부분) 및 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

Microsoft JDBC Driver 6.4는 JDBC 4.1, 4.2 및 4.3(부분) 사양을 지원하며 설치 패키지에 다음과 같은 세 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR                       | JDBC 사양                 | JDK 버전 |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3(부분), 4.2 및 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 및 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |

Microsoft JDBC Driver 6.2는 JDBC 4.0, 4.1 및 4.2 사양을 지원하며 설치 패키지에 다음과 같은 두 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR                       | JDBC 사양     | JDK 버전 |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2, 4.1 및 4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 및 4.0       | JDK 7.0     |

SQL Server용 Microsoft JDBC Driver 6.0 및 4.2는 JDBC 4.0, 4.1 및 4.2 사양을 지원하며 설치 패키지에 다음과 같은 두 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR           | JDBC 사양     | JDK 버전 |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2, 4.1 및 4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 및 4.0       | JDK 7.0     |

SQL Server용 Microsoft JDBC Driver 4.1은 JDBC 4.0 사양을 지원하며 설치 패키지에 다음과 같은 한 개의 JAR 클래스 라이브러리를 포함합니다.

| JAR           | JDBC 사양 | JDK 버전     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 및 6.0 |

**기존에 사용하던 SQL Server 버전에서 최신 드라이버를 사용하기 위해 내 애플리케이션에서 코드를 변경해야 하나요?**  
일반적으로 드라이버는 이전 버전과 호환되도록 설계되므로 드라이버를 업그레이드할 때 기존 애플리케이션을 변경할 필요는 없습니다. 새 드라이버 버전에 주요 변경 내용이 도입될 예정이면 [Release Notes for the JDBC Driver](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)(JDBC Drive 릴리스 정보) 섹션에 변경 내용 및 기존 애플리케이션에 미치는 영향에 관한 세부 정보가 제공됩니다. 또한 드라이버에 포함된 릴리스 정보에서 해당 릴리스에서 수정된 버그 목록과 알려진 문제를 검토할 수 있습니다.

**드라이버의 비용은 얼마나 되나요?**  
Microsoft JDBC Driver for SQL Server는 추가 비용 없이 사용할 수 있습니다.

**드라이버를 재배포할 수 있나요?**
JDBC 드라이버 4.1, 4.2, 6.0, 6.2, 6.4 및 7.0은 재배포 가능합니다. 라이선스 계약의 "배포 가능 코드" 절을 검토하세요.

**이 드라이버를 사용하여 Linux 컴퓨터에서 Microsoft SQL Server에 액세스할 수 있나요?**
예 이 드라이버를 사용하여 Linux, Unix 및 기타 Windows 이외의 플랫폼에서 SQL Server에 액세스할 수 있습니다. 자세한 내용은 [Microsoft JDBC Driver for SQL Server Support Matrix](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)(SQL Server용 Microsoft JDBC Driver 지원 매트릭스)를 참조하세요.

**드라이버가 SSL(Secure Sockets Layer) 암호화를 지원하나요?**
버전 1.2부터 이 드라이버는 SSL(Secure Sockets Layer) 암호화를 지원합니다. 자세한 내용은 [Using SSL Encryption](../../connect/jdbc/using-ssl-encryption.md)(SSL 암호화 사용)을 참조하세요.

**Microsoft JDBC Driver for SQL Server에서는 어떤 유형의 인증을 지원하나요?**  
다음 표에는서 사용할 수 있는 인증 옵션을 보여 줍니다. 이 드라이버 4.0 릴리스부터는 순수한 Java Kerberos 인증을 사용할 수 있습니다.

|             |                                       |
| ----------- | ------------------------------------- |
| 플랫폼    | 인증                        |
| 비 Windows | 순수 Java Kerberos                    |
| 비 Windows | SQL Server                            |
| 비 Windows | Azure Active Directory 인증 |
| Windows     | 순수 Java Kerberos                    |
| Windows     | SQL Server                            |
| 창     | NTLM 백업을 사용하는 Kerberos             |
| Windows     | NTLM                                  |
| Windows     | Azure Active Directory 인증 |

**이 드라이버가 IPv6(인터넷 프로토콜 버전 6) 주소를 지원하나요?**  
예 드라이버는 IPv6 주소 사용을 지원합니다. 연결 속성 컬렉션 및 serverName 연결 문자열 속성을 사용합니다. 자세한 내용은 [Building the Connection URL](../../connect/jdbc/building-the-connection-url.md)(연결 URL 작성)을 참조하세요.

**적응 버퍼링이란 무엇인가요?**  
적응 버퍼링 Microsoft SQL Server 2005 JDBC 드라이버 버전 1.2부터 도입되었습니다. 이 기능은 서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있도록 설계되었습니다. Microsoft SQL Server JDBC Driver의 선택 버퍼링 기능은 "선택" 또는 "전체"로 설정될 수 있는 responseBuffering 연결 문자열 속성을 제공합니다. 버전 1.2 릴리스에서는 버퍼링 모드가 기본적으로 "full"이므로 애플리케이션에서 명시적으로 적응 버퍼링 모드를 설정해야 합니다. JDBC Driver 버전 2.0부터, 이 드라이버의 기본 동작은 "선택"입니다. 따라서 적응 버퍼링을 사용하기 위해 애플리케이션에서 명시적으로 적응 버퍼링을 요청할 필요가 없습니다. 자세한 내용은 [적응 버퍼링 사용](../../connect/jdbc/using-adaptive-buffering.md) 및 [적응 응답 버퍼링이란 무엇이며 왜 사용해야 하나요?](https://go.microsoft.com/fwlink/?LinkId=111575) 블로그를 참조하세요.

**이 드라이버는 연결 풀링을 지원하나요?**  
이 드라이버는 Java Platform, Enterprise Edition 5(Java EE 5) 연결 풀링을 지원합니다. 미들웨어 애플리케이션 서버 공급업체가 제공하며 JDBC 3.0과 호환되는 모든 연결 풀링 구현에 참여할 수 있도록 드라이버는 JDBC 3.0 필수 인터페이스를 구현합니다. 이 드라이버는 이러한 환경에서 풀링된 연결에 참여합니다. 자세한 내용은 [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md)을 참조하세요. 이 드라이버는 자체 풀링 구현을 제공하지 않으며 타사 Java 애플리케이션 서버에 의존합니다.

**이 드라이버에 대한 지원을 사용할 수 있나요?**  
몇 가지 지원 옵션을 사용할 수 있습니다. Microsoft에서 모니터링하는 [GitHub 리포지토리](https://github.com/microsoft/mssql-jdbc)에 질문이나 문제를 게시할 수 있습니다. [포럼](https://go.microsoft.com/fwlink/?LinkID=246673)은 Microsoft, MVP 및 커뮤니티에서 모니터링합니다. Microsoft 고객 지원 서비스에 문의할 수도 있습니다. 개발 팀에서는 타사 애플리케이션 서버 외부에서 발생하는 문제를 재현하도록 요청할 수도 있습니다. 호스팅 Java 컨테이너 환경 외부에서 발생하는 문제를 재현할 수 없는 경우 관련 타사에 문의해야만 계속 팀의 지원을 받을 수 있습니다. 팀에서는 문제와 관련하여 최적의 도움을 주기 위해 Windows와 같은 운영 체제에서 문제를 재현하도록 요청할 수도 있습니다.

**이 드라이버는 타사 애플리케이션 서버에서 사용할 수 있도록 인증되었나요?**
이 드라이버는 IBM WebSphere 및 SAP NetWeaver를 비롯한 다양한 애플리케이션 서버에서 테스트되었습니다.

**추적을 사용하도록 설정하려면 어떻게 하나요?**  
이 드라이버에서는 추적 또는 로깅 기능을 사용하여 애플리케이션에서 사용되는 JDBC Driver 관련 문제를 해결할 수 있습니다. 클라이언트 쪽 JAR 추적을 사용으로 설정할 수 있도록 JDBC Driver는 java.util.logging의 로깅 API를 사용합니다. 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요. 서버 쪽 XA 추적에 대한 자세한 내용은 [SQL Server의 데이터 액세스 추적](https://go.microsoft.com/fwlink/?LinkId=248705)을 참조하세요.

**SQL Server 2000 JDBC Driver, 2005 Driver, 1.0, 1.1 또는 1.2 Driver와 같은 이전 버전의 드라이버는 어디에서 다운로드할 수 있나요?**  
이러한 드라이버 버전은 더 이상 지원되지 않으므로 다운로드할 수 없습니다. Java 연결 지원을 지속적으로 개선하고 있습니다. 따라서 최신 버전의 Microsoft JDBC 드라이버를 사용하는 것이 좋습니다.

**현재 JRE 1.4를 사용하고 있습니다. 어떤 드라이버가 JRE 1.4와 호환되나요?**  
SAP 제품을 사용하고 있으며 JRE 1.4 지원이 필요한 고객의 경우 [SAPService 마켓플레이스](https://service.sap.com/) 에 연결하여 1.2 Microsoft JDBC Driver를 얻을 수 있습니다.

**이 드라이버가 FIPS 유효성 검사 알고리즘을 사용하여 통신할 수 있나요?**  
Microsoft JDBC Driver에는 암호화 알고리즘이 포함되어 있지 않습니다. 고객이 FIPS(Federal Information Processing Standards)에서 허용될 수 있는 운영 체제, 애플리케이션 및 JVM 알고리즘을 활용하며 해당 알고리즘을 사용하도록 드라이버를 구성하는 경우 해당 드라이버는 지정된 알고리즘만 통신에 사용합니다.

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)
