---
title: 유효성 검사 없이 암호화 사용 | Microsoft Docs
description: 유효성 검사 없이 암호화 사용
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ef21cdb2a223aaa50b690f5b2b3c30696dd9e196
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67988852"
---
# <a name="using-encryption-without-validation"></a>유효성 검사 없이 암호화 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 로그인과 관련한 네트워크 패킷이 항상 암호화됩니다. 서버를 시작할 때 제공된 인증서가 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 로그인 패킷을 암호화하는 데 사용할 자체 서명된 인증서를 생성합니다.  

자체 서명된 인증서는 보안을 보장하지 않습니다. 암호화된 핸드셰이크는 NTLM(NT LAN Manager)을 기반으로 합니다. 보안 연결을 위해 SQL Server에 확인할 수 있는 인증서를 프로비전하는 것이 좋습니다. TLS(Transport Security Layer)는 인증서 유효성 검사를 통해서만 안전하게 만들 수 있습니다.

애플리케이션에 따라 연결 문자열 키워드나 연결 속성을 사용하여 모든 네트워크 트래픽을 암호화해야 할 수도 있습니다. **IDbInitialize::Initialize**에 공급자 문자열을 사용하는 경우 OLE DB에 대한 키워드는 "Encrypt"이고, **IDataInitialize**에 초기화 문자열을 사용하는 경우 ADO 및 OLE DB에 대한 키워드는 "Use Encryption for Data"입니다. 이는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]강제 프로토콜 암호화**옵션을 사용하고 클라이언트가 암호화된 연결을 요청하도록 구성하여** 구성 관리자에서도 구성할 수 있습니다. 기본적으로 연결의 모든 네트워크 트래픽을 암호화하려면 서버에 인증서를 제공해야 합니다. 서버에서 인증서를 신뢰하도록 클라이언트를 설정하면 메시지 가로채기(man-in-the-middle) 공격에 취약해질 수 있습니다. 서버에 확인할 수 있는 인증서를 배포하는 경우 인증서를 신뢰하는 방법에 대한 클라이언트 설정을 FALSE로 변경해야 합니다.

연결 문자열 키워드에 대한 내용은 [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md )을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager에서 **프로토콜 암호화 강제 사용** 및 **서버 인증서 신뢰** 옵션을 모두 설정하면 서버에 인증서가 제공되지 않은 경우에도 암호화를 사용할 수 있습니다. 이 경우 확인할 수 있는 인증서가 서버에 제공되지 않으면 유효성 검사 없이 자체 서명된 서버 인증서가 암호화에 사용됩니다.  
  
 애플리케이션에서 &quot;TrustServerCertificate&quot; 키워드 또는 이 키워드의 관련 연결 특성을 사용하여 암호화를 보장할 수도 있습니다. 애플리케이션 설정으로 인해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 구성 관리자에서 설정한 보안 수준이 낮아지지는 않지만 더 강화될 수는 있습니다. 예를 들어 클라이언트에 대해 **프로토콜 암호화 강제 사용** 옵션을 설정하지 않았지만 애플리케이션 자체에서 암호화를 요청할 수 있습니다. 또한 서버 인증서가 제공되지 않은 경우에도 암호화를 보장할 수 있도록 애플리케이션에서 암호화 및 &quot;TrustServerCertificate&quot;를 요청할 수도 있습니다. 그러나 클라이언트 구성에 "TrustServerCertificate"가 설정되어 있지 않은 경우에는 제공된 서버 인증서가 필요합니다. 다음 표에서는 이러한 모든 경우에 대해 설명합니다.  
  
|프로토콜 암호화 강제 사용 클라이언트 설정|서버 인증서 신뢰 클라이언트 설정|연결 문자열/연결 특성 Encrypt/Use Encryption for Data|연결 문자열/연결 특성 서버 인증서 신뢰|결과|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|예|해당 없음|아니요(기본값)|무시됨|암호화가 수행되지 않습니다.|  
|예|해당 없음|yes|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|예|해당 없음|yes|yes|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|yes|예|무시됨|무시됨|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|yes|yes|아니요(기본값)|무시됨|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|yes|yes|yes|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|yes|yes|yes|yes|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
||||||

> [!CAUTION]
> 위의 표에서는 다양한 구성에서 시스템 동작에 대한 지침만 제공합니다. 보안 연결의 경우 클라이언트와 서버 모두 암호화가 필요합니다. 또한 서버에 확인할 수 있는 인증서가 있고 클라이언트의 **TrustServerCertificate** 설정이 FALSE로 설정되어 있어야 합니다.

## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 
 SQL Server용 OLE DB 드라이버는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 구현된 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 데이터 원본 초기화 속성이 추가되면서 유효성 검사 없이 암호화를 지원합니다. 또한 "TrustServerCertificate"라는 새로운 연결 문자열 키워드가 추가되었습니다. 이 문자열 키워드는 예 또는 아니요 값을 받으며, 기본값은 아니요입니다. 서비스 구성 요소를 사용하는 경우에는 True 또는 False 값을 받으며, 기본값은 False입니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합의 향상된 기능에 대한 자세한 내용은 [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요.  

  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
