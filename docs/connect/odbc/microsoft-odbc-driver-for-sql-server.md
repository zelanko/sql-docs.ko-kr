---
title: Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a6c86f3097efdc30089820432fedcb0ab530e04
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662617"
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC는 SQL Server에 대 한 C 및 c + +로 작성 하는 응용 프로그램에 대 한 기본 네이티브 데이터 액세스 API입니다. 대부분의 데이터 원본에 대 한 ODBC 드라이버가 있습니다. ODBC를 사용할 수 있는 다른 언어는 COBOL, Perl, PHP 및 Python을 포함 합니다. ODBC는 데이터 통합 시나리오에서 널리 사용 됩니다.

ODBC 드라이버에는 [**sqlcmd**](../../tools/sqlcmd-utility.md) 및 [**bcp**](../../tools/bcp-utility.md)와 같은 도구가 포함되어 있습니다. **sqlcmd** 유틸리티를 사용하면 Transact-SQL 문, 시스템 프로시저 및 SQL 스크립트를 실행할 수 있습니다. **bcp** 유틸리티는 Microsoft SQL Server 인스턴스와 사용자가 선택한 형식의 데이터 파일 간에 데이터를 대량 복사합니다. **bcp** 유틸리티를 사용하여 많은 수의 새 행을 SQL Server 테이블로 가져오거나 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다.  

## <a name="code-example-in-c"></a>C + +의 코드 예제에서

다음 c + + 샘플 ODBC Api를 사용 하 여 연결 하 고 데이터베이스에 액세스 하는 방법에 설명 합니다.

- [C + + 코드 예제에서는 ODBC를 사용 하 여](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>다운로드

- ![다운로드-아래쪽 화살표-원이](../../ssdt/media/download.png)[ODBC 드라이버를 다운로드 하려면](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>설명서

### <a name="features"></a>기능

- [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)
- [DSN 및 연결 문자열 키워드 및 특성](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (제공 되는 기능 또한 적용, OLEDB, ODBC driver for SQL Server 없이)
- [Always Encrypted 사용](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Azure Active Directory 사용](../../connect/odbc/using-azure-active-directory.md)
- [투명 네트워크 IP 확인 사용](../../connect/odbc/using-transparent-network-ip-resolution.md)
- [XA 트랜잭션 사용](../../connect/odbc/use-xa-with-dtc.md)

### <a name="linux-and-macos"></a>Linux 및 macOS

- [드라이버 설치](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [SQL Server에 연결](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [**bcp**를 사용하여 연결](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [**sqlcmd**를 사용하여 연결](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [데이터 액세스 추적](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [질문과 대답](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [드라이버 관리자 설치](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [알려진 문제](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [프로그래밍 지침](../../connect/odbc/linux-mac/programming-guidelines.md)
- [릴리스 정보](../../connect/odbc/linux-mac/release-notes.md)
- [고가용성 및 재해 복구 지원](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [통합 인증 사용(Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [비동기 실행(알림 메서드) 샘플](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Windows ODBC 드라이버의 연결 복원](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [드라이버 인식 연결 풀링](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [기능 및 동작 변경 내용](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [릴리스 정보](../../connect/odbc/windows/release-notes.md)
- [시스템 요구 사항, 설치 및 드라이버 파일](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>커뮤니티  
- [Microsoft ODBC Driver for SQL Server 팀 블로그](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server 데이터 액세스 포럼](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
