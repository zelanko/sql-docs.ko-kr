---
title: Windows 기반 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 059c949b11c0cd571fdf3c6ff2575476c477ef04
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58788080"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows의 Microsoft ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 표준 ODBC 인터페이스를 구현하는 API(애플리케이션 프로그래밍 인터페이스)를 제공하는 독립 실행형 ODBC 드라이버입니다.

Microsoft ODBC Driver for SQL Server를 사용하여 새 애플리케이션을 만들 수 있습니다. 또한 현재 이전 ODBC 드라이버를 사용하는 이전 애플리케이션을 업그레이드할 수도 있습니다. ODBC Driver for SQL Server는 Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, SQL Server 2017, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 및 SQL Server 2005에 대한 연결을 지원합니다.  

## <a name="summary"></a>요약

| 버전 옵션       | 지원되는 기능      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>BCP API에 대한 Always Encrypted 지원</li><li>새 연결 문자열 속성 UseFMTONLY는 임시 테이블이 필요한 특별한 경우 드라이버에서 구형 메타데이터를 사용하게 합니다.</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Azure AD 인증</li><li>AlwaysOn AG(가용성 그룹)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>IDN(다국어 도메인 이름)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>드라이버 인식 연결 풀링</li><li>연결 복원력</li><li>비동기 실행(폴링 메서드)</li></ul> |    

## <a name="documentation"></a>설명서  
이 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문서에는 다음이 포함되어 있습니다.  
  
-   [Windows 기반 SQL Server에 대한 ODBC 릴리스 정보](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Windows 기반 Microsoft ODBC Driver for SQL Server의 기능](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [시스템 요구 사항, 설치 및 드라이버 파일](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server에서 드라이버 인식 연결 풀링](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [비동기 실행&#40;알림 방법&#41; 샘플](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC 드라이버의 연결 복원](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [상시 암호화와 ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [ODBC 드라이버에서 Azure Active Directory 사용](../../../connect/odbc/using-azure-active-directory.md) 
-   [투명 네트워크 IP 확인 사용](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>커뮤니티  
- [Microsoft ODBC Driver for SQL Server 팀 블로그](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server 데이터 액세스 포럼](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>참고 항목  
- [SQL Server Native Client 정보](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [SQL Server Native Client FAQ](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [ODBC 프로그래머 참조](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client(ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
