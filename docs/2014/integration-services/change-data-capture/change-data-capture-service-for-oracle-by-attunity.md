---
title: Attunity Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 53eecca1c854e13c2302bf65814b1bc77259d2ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154339"
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Attunity Oracle CDC Service
  Oracle CDC Service는 Oracle 트랜잭션 로그를 검색하고 관련 Oracle 테이블의 변경 내용을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경 테이블에 캡처하는 Windows 서비스입니다. Oracle에서 캡처한 변경 내용이 저장되는 SQL 변경 테이블은 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경 데이터 캡처 기능에서 사용하는 변경 테이블과 같은 유형입니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 변경 내용을 사용하는 것만큼 쉽게 이 변경 내용을 사용할 수 있습니다.  
  
## <a name="installation"></a>설치  
 캡처되는 원본 Oracle 데이터베이스와 대상 CDC 데이터베이스가 위치하는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 액세스할 수 있는 지원되는 Windows 컴퓨터에 Oracle CDC Service를 설치할 수 있습니다. CDC Service는 Oracle 데이터베이스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 로컬 설치가 필요 없으며 지원되는 클라이언트만 있으면 됩니다. 필요한 데이터베이스 구성 요소를 설치하는 위치에 대한 자세한 내용은 이 항목의 **데이터베이스 필수 구성 요소** 를 참조하십시오.  
  
 Oracle용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC Service를 설치하면 서비스 구성 UI와 서비스 프로그램이 선택한 위치에 배치됩니다. Oracle CDC Service는 Oracle CDC Service 구성 콘솔을 사용하여 별도로 구성됩니다. Oracle CDC Service 구성에 대한 자세한 내용은 [Change Data Capture Service for Oracle by Attunity F1 도움말](change-data-capture-service-for-oracle-by-attunity-f1-help.md)을 참조하십시오.  
  
 Oracle CDC Service를 설치하려면 SQL Server 설치 미디어에서 **AttunityOracleCdcService.msi** 를 수동으로 실행합니다. X86 및 x64 설치 패키지에 위치한 **.\Tools\AttunityCDCOracle\\**  SQL Server 설치 미디어에 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client가 설치되는 지원되는 Windows 컴퓨터에 Oracle CDC Service를 설치할 수 있으며 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되는 동일한 컴퓨터에 설치할 필요는 없습니다.  
  
## <a name="supported-windows-environments"></a>지원되는 Windows 환경  
 Attunity Oracle CDC Service는 다음 Windows 환경에서 실행할 수 있습니다.  
  
-   Windows 8  
  
-   Windows 7 32비트(x86) 및 64비트(x64)  
  
-   Windows Server 2012  
  
-   • Windows Server 2008 R2 서비스 팩 1  
  
-   Windows Server 2008 32비트(x86) 및 64비트(x64) 서비스 팩 2  
  
## <a name="database-prerequisites"></a>데이터베이스 필수 구성 요소  
 Oracle CDC Service를 사용하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client Oracle 소프트웨어를 설치해야 합니다. 이 항목은 Oracle CDC Service를 설치하기 전에 Oracle에서 구하여 설치해야 하는 필수 구성 요소입니다. 또한 SQL Server 설치 프로그램을 사용하여 SQL Server ODBC 클라이언트를 설치해야 합니다.  
  
 Oracle CDC Service는 다음 버전을 지원합니다.  
  
### <a name="source-oracle-database"></a>원본 Oracle 데이터베이스  
  
-   Oracle 데이터베이스 11x, 모든 버전  
  
-   Oracle 데이터베이스 10x, 모든 버전  
  
### <a name="target-sql-server-database"></a>대상 SQL Server 데이터베이스  
 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="running-the-installation-program"></a>설치 프로그램 실행  
 Oracle CDC Service를 설치하려면 사용 중인 Windows 플랫폼(32/64비트)에 맞는 설치 마법사를 열고 화면에 나타나는 지침을 따릅니다.  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>Attunity Oracle CDC Service 제거  
 제어판, 프로그램 및 기능을 사용하여 Oracle CDC Service를 제거합니다.  
  
 CDC Service를 제거해도 만들어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 제거되지 않습니다. 도구를 완전히 제거하려면 작업한 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 만들어진 MSXDBCDC 데이터베이스와 특정 CDC 데이터베이스를 제거해야 합니다.  
  
 CDC Service 소프트웨어를 한 컴퓨터에서 제거하고 다른 컴퓨터에 설치하려면 다음 정의를 제공하면 됩니다.  
  
-   서비스 계정  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열 및 자격 증명  
  
-   마스터 암호  
  
 다른 모든 정의는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장되며 다른 컴퓨터의 이전 설치에서 사용할 수 있습니다.  
  
## <a name="in-this-documentation"></a>이 설명서의 내용  
  
-   [Attunity Oracle CDC Service 시스템 아키텍처](change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [Oracle CDC Service](the-oracle-cdc-service.md)  
  
-   [Change Data Capture Service for Oracle by Attunity F1 도움말](change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Attunity Oracle CDC Service 방법 가이드](change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>참고 항목  
 [Oracle CDC Service 작업](working-with-the-oracle-cdc-service.md)  
  
  
