---
title: SQL Server Native Client의 새로운 기능&#39;| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 003abb67cd66d02294210ddb3f55061abcc804f4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704138"
---
# <a name="what39s-new-in-sql-server-native-client"></a>SQL Server Native Client의 새로운 기능&#39;
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client를 설치하며, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client는 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 ODBC 드라이버에 대한 업데이트는 더 이상 없습니다. Windows에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC Driver 11 for [!INCLUDE[msCoName](../../includes/msconame-md.md)]이라 불리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 후속 ODBC 드라이버는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]와 함께 설치됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 기반 Odbc driver 11 for에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Microsoft odbc driver 11 For SQL Server-Windows](https://www.microsoft.com/download/details.aspx?id=36434)를 참조 하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 OLE DB 공급자는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client에서 마지막으로 업데이트되었습니다. OLE DB 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 최신 버전에 연결하려는 개발자는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client에서 제공되는 OLE DB 공급자를 사용해야 합니다.  
  
 다음 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새로운 주요 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 기능에 대해 설명합니다.  
  
-   [LocalDB에 대한 SQL Server Native Client 지원](features/sql-server-native-client-support-for-localdb.md)  
  
-   [메타데이터 검색](features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0의 UTF-16 지원](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [고가용성 재해 복구를 위한 SQL Server Native Client 지원](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [확장 이벤트 로그의 진단 정보 액세스](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 또한 이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 ODBC에서는 Windows 7 SDK의 표준 ODBC에 추가된 다음과 같은 3가지 기능을 지원합니다.  
  
-   연결 관련 작업에 대한 비동기 실행. 자세한 내용은 [비동기 실행](https://go.microsoft.com/fwlink/?LinkID=191493)을 참조 하세요.  
  
-   C 데이터 형식 확장성. 자세한 내용은 [ODBC의 C 데이터 형식](https://go.microsoft.com/fwlink/?LinkID=191495)을 참조 하세요.  
  
     Native Client에서이 기능을 지원 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLGetDescField는 `SQL_C_SS_TIME2` `time` `SQL_C_SS_TIMESTAMPOFFSET` `datetimeoffset` `SQL_C_BINARY` 응용 프로그램에서 ODBC 3.8를 사용 하는 경우 대신 (형식) 또는 (의 경우)를 반환할 수 있습니다. 자세한 내용은 [ODBC 날짜 및 시간 향상을 위한 데이터 형식 지원](features/date-and-time-improvements.md)을 참조 하세요.  
  
-   큰 매개 변수 값을 검색하기 위해 작은 버퍼로 여러 번 `SQLGetData` 호출. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](https://go.microsoft.com/fwlink/?LinkID=191494)을 참조 하세요.  
  
 다음 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 동작 변경에 대해 설명합니다.  
  
-   를 호출 하는 경우 `ICommandWithParameters::SetParameterInfo` *pwszName* 매개 변수에 전달 된 값은 올바른 식별자 여야 합니다. 자세한 내용은 [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md)를 참조 하세요.  
  
-   `SQLDescribeParam`은 이제 ODBC 사양을 따르는 값을 일관성 있게 반환합니다. 자세한 내용은 [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md)를 참조 하세요.  
  
-   [문자 변환을 처리 시 ODBC 드라이버 동작 변경](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](features/sql-server-native-client-features.md)  
  
  
