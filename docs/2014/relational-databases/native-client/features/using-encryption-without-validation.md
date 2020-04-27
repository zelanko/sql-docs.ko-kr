---
title: 유효성 검사 없이 암호화 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 443c6e0c556a7e69510796b1d58ab0f7b2567e6e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63225489"
---
# <a name="using-encryption-without-validation"></a>유효성 검사 없이 암호화 사용
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 로그인과 관련한 네트워크 패킷이 항상 암호화됩니다. 서버를 시작할 때 제공된 인증서가 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 로그인 패킷을 암호화하는 데 사용할 자체 서명된 인증서를 생성합니다.  
  
 애플리케이션에 따라 연결 문자열 키워드나 연결 속성을 사용하여 모든 네트워크 트래픽을 암호화해야 할 수도 있습니다. 키워드는 **IDbInitialize:: Initialize**를 사용 하 여 공급자 문자열을 사용 하는 경우, **IDataInitialize**과 함께 초기화 문자열을 사용 하는 경우 ADO 및 OLE DB에서 "데이터 암호화 사용"을 사용 하는 경우에는 OLE DB ODBC의 "Encrypt"입니다. 이는 Configuration Manager [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **프로토콜 암호화 강제** 사용 옵션을 사용 하 여 구성할 수도 있습니다. 기본적으로 연결의 모든 네트워크 트래픽을 암호화하려면 서버에 인증서를 제공해야 합니다.  
  
 연결 문자열 키워드에 대 한 자세한 내용은 [SQL Server Native Client 연결 문자열 키워드 사용](../applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager에서 **프로토콜 암호화 강제 사용** 및 **서버 인증서 신뢰** 옵션을 모두 설정하면 서버에 인증서가 제공되지 않은 경우에도 암호화를 사용할 수 있습니다. 이 경우 확인할 수 있는 인증서가 서버에 제공되지 않으면 유효성 검사 없이 자체 서명된 서버 인증서가 암호화에 사용됩니다.  
  
 애플리케이션에서 &quot;TrustServerCertificate&quot; 키워드 또는 이 키워드의 관련 연결 특성을 사용하여 암호화를 보장할 수도 있습니다. 애플리케이션 설정으로 인해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 구성 관리자에서 설정한 보안 수준이 낮아지지는 않지만 더 강화될 수는 있습니다. 예를 들어 클라이언트에 대해 **프로토콜 암호화 강제 사용** 옵션을 설정하지 않았지만 애플리케이션 자체에서 암호화를 요청할 수 있습니다. 또한 서버 인증서가 제공되지 않은 경우에도 암호화를 보장할 수 있도록 애플리케이션에서 암호화 및 &quot;TrustServerCertificate&quot;를 요청할 수도 있습니다. 그러나 클라이언트 구성에 "TrustServerCertificate"가 설정되어 있지 않은 경우에는 제공된 서버 인증서가 필요합니다. 다음 표에서는 이러한 모든 경우에 대해 설명합니다.  
  
|프로토콜 암호화 강제 사용 클라이언트 설정|서버 인증서 신뢰 클라이언트 설정|연결 문자열/연결 특성 Encrypt/Use Encryption for Data|연결 문자열/연결 특성 서버 인증서 신뢰|결과|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|아니요|해당 없음|아니요(기본값)|무시됨|암호화가 수행되지 않습니다.|  
|아니요|해당 없음|예|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|아니요|해당 없음|예|예|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|예|아니요|무시됨|무시됨|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|yes|예|아니요(기본값)|무시됨|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|예|예|yes|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|예|예|yes|yes|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 DBPROPSET_SQLSERVERDBINIT 속성 집합에서 구현 된 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 데이터 원본 초기화 속성을 추가 하 여 유효성 검사 없이 암호화를 지원 합니다. 또한 "TrustServerCertificate"라는 새로운 연결 문자열 키워드가 추가되었습니다. 이 문자열 키워드는 예 또는 아니요 값을 받으며, 기본값은 아니요입니다. 서비스 구성 요소를 사용하는 경우에는 True 또는 False 값을 받으며, 기본값은 False입니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합의 향상된 기능에 대한 자세한 내용은 [초기화 및 권한 부여 속성](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client ODBC 드라이버는 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md) 함수를 추가 하 여 유효성 검사 없이 암호화를 지원 합니다. SQL_TRUST_SERVER_CERTIFICATE_YES 또는 SQL_TRUST_SERVER_CERTIFICATE_NO를 받는 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE가 추가되었습니다. 기본값은 SQL_TRUST_SERVER_CERTIFICATE_NO입니다. 또한 "TrustServerCertificate"라는 새로운 연결 문자열 키워드가 추가되었습니다. 이 문자열 키워드는 예 또는 아니요 값을 받으며, 기본값은 "아니요"입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  
