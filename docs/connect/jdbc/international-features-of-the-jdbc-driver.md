---
title: JDBC 드라이버의 국가별 기능 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64c046ade18bfdf8789ce9fec221f3d33517fcbb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028013"
---
# <a name="international-features-of-the-jdbc-driver"></a>JDBC 드라이버의 국가별 기능
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 국가별 기능은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 동일한 언어로 완전히 지역화된 환경을 지원합니다.  
  
-   로캘을 구분하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터에 대해 Java 언어 변환을 지원합니다.  
  
-   운영 체제와 상관없이 국가별 언어 지원  
  
-   국제 도메인 이름 지원(SQL Server용 Microsoft JDBC Driver 6.0부터 지원)  
  
## <a name="handling-of-character-data"></a>문자 데이터 처리  
 Java 문자 데이터는 기본적으로 유니코드로 처리하며 Java **문자열** 개체는 유니코드 문자 데이터를 나타냅니다. JDBC 드라이버에서 이 규칙의 유일한 예외는 ASCII 스트림 getter 및 setter 메서드입니다. 이들 메서드는 암시적으로 잘 알려진 단일 코드 페이지(ASCII)를 전제로 한 바이트 스트림을 사용하기 때문에 특수한 경우에 해당합니다.  
  
 또한 JDBC 드라이버는 **sendStringParametersAsUnicode** 연결 문자열 속성을 제공합니다. 이 속성을 사용하여 문자 데이터의 준비된 매개 변수를 유니코드 대신 ASCII 또는 MBCS(멀티바이트 문자 집합)로 보내도록 지정할 수 있습니다. **sendStringParametersAsUnicode** 연결 문자열 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
### <a name="driver-incoming-conversions"></a>드라이버의 들어오는 데이터 변환  
 서버에서 들어오는 유니코드 텍스트 데이터는 유니코드로 직접 전달되므로 변환할 필요가 없습니다. 서버에서 들어오는 데이터 중 유니코드가 아닌 데이터는 데이터베이스 또는 열 수준에서 데이터의 코드 페이지에서 유니코드로 변환됩니다. JDBC 드라이버는 이러한 변환을 수행하기 위해 JVM(Java Virtual Machine) 변환 루틴을 사용합니다. 이러한 변환은 형식화된 모든 문자열 및 문자 스트림 getter 메서드에서 수행됩니다.  
  
 JVM이 데이터베이스의 데이터에 대해 적절한 코드 페이지를 지원하지 않는 경우 JDBC 드라이버에서 "XXX 코드 페이지는 Java 환경에서 지원되지 않습니다." 예외가 발생합니다. 이 문제를 해결하려면 해당 JVM에 필요한 전체 국가별 문자 지원을 설치해야 합니다. 이러한 예를 보려면 Sun Microsystems 웹 사이트의 Supported Encodings 설명서를 참조하십시오.  
  
### <a name="driver-outgoing-conversions"></a>드라이버의 나가는 데이터 변환  
 드라이버에서 서버로 나가는 문자 데이터는 ASCII 또는 유니코드일 수 있습니다. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 setNString, setNCharacterStream 및 setNClob 메서드와 같은 새 JDBC 4.0 국가별 문자 메서드는 항상 매개 변수 값을 유니코드로 서버에 보냅니다.  
  
 반면 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 setString, setCharacterStream 및 setClob 메서드와 같은 비국가별 문자 API 메서드는 **sendStringParametersAsUnicode** 속성이 “true”로 설정(기본값)된 경우에만 해당 값을 유니코드로 서버에 전송합니다.  
  
## <a name="non-unicode-parameters"></a>유니코드가 아닌 매개 변수  
 유니코드가 아닌 매개 변수의 **CHAR**, **VARCHAR** 또는 **LONGVARCHAR** **sendStringParametersAsUnicode** 속성을 사용 하는 최적의 성능을 위해, 연결 문자열 속성을 "false"로 설정 하 고 국가별 문자 메서드가 아닌 메서드를 사용 합니다.  
  
## <a name="formatting-issues"></a>서식 지정 문제  
 날짜, 시간 및 통화의 경우 지역화된 데이터에 관한 모든 서식 지정은 Locale 개체와 **Date**, **Calendar** 및 **Number** 데이터 형식의 다양한 서식 지정 메서드를 사용하여 Java 언어 수준에서 수행됩니다. 드문 경우이기는 하지만 JDBC 드라이버가 지역화된 형식으로 로캘 구분 데이터를 함께 전달해야 하는 경우 기본 JVM 로캘과 함께 적절한 포맷터가 사용됩니다.  
  
## <a name="collation-support"></a>데이터 정렬 지원  
 JDBC 드라이버 3.0에서는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 지원하는 모든 데이터 정렬 및 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에 도입된 새로운 버전의 Windows 데이터 정렬 이름 또는 새 데이터 정렬을 지원합니다.  
  
 데이터 정렬에 대한 자세한 내용은 [ 온라인 설명서의](https://go.microsoft.com/fwlink/?LinkId=131366)데이터 정렬 및 유니코드 지원[ 및 ](https://go.microsoft.com/fwlink/?LinkId=131367)Windows 데이터 정렬 이름(Transact-SQL)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 참조하십시오.  
  
## <a name="using-international-domain-names-idn"></a>IDN(국제 도메인 이름) 사용  
 SQL Server용 JDBC Driver 6.0에서는 IDN(Internationalized Domain Name)의 사용을 지원하고 연결 중 필요한 경우 유니코드 serverName을 ASCII 호환 인코딩(Punycode)으로 변환할 수 있습니다.  IDN이 Punycode 형식(RFC 3490에서 지정)의 ASCII 문자열로 DNS(Domain Name System)에 저장되면 serverNameAsACE 속성을 true로 설정하여 유니코드 서버 이름을 변환할 수 있습니다.  그렇지 않으면 DNS 서비스가 유니코드 문자를 사용할 수 있도록 구성된 경우 serverNameAsACE 속성을 false(기본값)로 설정합니다.  또한 이전 버전의 JDBC 드라이버의 경우 연결을 위해 해당 속성을 설정하기 전에 [Java의 IDN.toASCII](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) 메서드를 사용하여 serverName을 Punycode로 변환할 수 있습니다.  
  
> [!NOTE]  
>  Windows 이외의 플랫폼용으로 작성된 대부분의 확인 프로그램 소프트웨어는 인터넷 DSN 표준 기반이므로 IDN에 대해 Punycode 형식을 사용할 가능성이 높은 반면 프라이빗 네트워크의 Windows 기반 DNS 서버는 서버 단위로 UTF-8 문자 사용을 허용하도록 구성될 수 있습니다.  자세한 내용은 [유니코드 문자 지원](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
