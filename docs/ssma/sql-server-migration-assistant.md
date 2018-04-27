---
title: SQL Server Migration Assistant | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d0233525-a83b-4279-813e-c554042abd0e
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1003d5250c2d1e2cc9816fa50ea8f11bdd3a8b29
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-migration-assistant"></a>SQL Server 마이그레이션 길잡이
Microsoft SQL Server Migration Assistant (SSMA)는 Microsoft Access, DB2, MySQL, Oracle 및 SAP ASE에서 SQL Server로 데이터베이스 마이그레이션을 자동화할 수 있는 도구입니다.  
  
## <a name="migration-sources"></a>마이그레이션 원본  
  
-   [SQL Server Migration Assistant for Access](../ssma/access/sql-server-migration-assistant-for-access-accesstosql.md)  
  
-   [D b 2 용 SQL Server Migration Assistant](../ssma/db2/sql-server-migration-assistant-for-db2-db2tosql.md)  
  
-   [MySQL 용 SQL Server Migration Assistant](../ssma/mysql/sql-server-migration-assistant-for-mysql-mysqltosql.md)  
  
-   [Oracle 용 SQL Server Migration Assistant](../ssma/oracle/sql-server-migration-assistant-for-oracle-oracletosql.md)  
  
-   [SAP ASE에 대 한 SQL Server Migration Assistant](../ssma/sybase/sql-server-migration-assistant-for-sybase-sybasetosql.md)  

## <a name="supported-sources-and-target-versions"></a>지원 되는 소스 및 대상 버전
지원 되는 소스에 대 한 SSMA 다운로드에 대 한 다운로드 센터에 대 한 정보를 검토 합니다.

다음 대상 버전 SSMA 지원 됩니다.

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Azure SQL Database
- Windows 및 Linux (미리 보기)에서 SQL Server 2017
- * * Azure SQL 데이터 웨어하우스

* *이 대상 Oracle 용 SSMA 에서만 지원 됩니다.
 
## <a name="downloads"></a>다운로드
- [SSMA for Access](http://aka.ms/ssmaforaccess)
- [SSMA for DB2](http://aka.ms/ssmafordb2)
- [MySQL용 SSMA](http://aka.ms/ssmaformysql)
- [SSMA for Oracle](http://aka.ms/ssmafororacle)
- [SSMA for SAP ASE](http://aka.ms/ssmaforsybase)
 
## <a name="getting-ssma-support"></a>SSMA 지원 받기  
**도움말 및 지원에 대 한 Microsoft SQL Server Migration Assistant (SSMA):**  
  
-   **제품 도움말** -하려면 기술 지원 서비스에 액세스, SSMA를 시작 하 고 도움말 메뉴를 선택 하거나 F1 키를 누릅니다.  
  
-   **SQL Server 커뮤니티 포럼** – SQL Server 커뮤니티에서 질문 하기  
  
    -   [SQL Server 커뮤니티](http://go.microsoft.com/fwlink/?LinkId=42455) -뉴스 그룹 및 SQL Server 커뮤니티에서 모니터링 하는 포럼입니다. 이 사이트에는 블로그 및 웹 사이트와 같은 커뮤니티 정보 소스도 나열됩니다.  
  
    -   [SQL Server Developer Center 커뮤니티](http://go.microsoft.com/fwlink/?LinkId=42456) -뉴스 그룹, 포럼 및 SQL Server 개발자에 유용한 기타 커뮤니티 리소스  
  
-   지원-이동 부서 [ https://support.microsoft.com/assistedsupportproducts ](https://support.microsoft.com/assistedsupportproducts) ' SQL Server Migration Assistant'으로 검색 합니다.  버전을 선택한 다음 "시작 요청입니다." 선택  도움을 받아 SQL Server 마이그레이션 길잡이 도구가 포함 되어 있습니다.  
  
-   프리미어 지원-프리미어 계약에 있는 경우 가져올 수 있습니다 프리미어 지원에 [Premier Online 포털](https://premier.microsoft.com/)합니다.  
  
-   Go 마이그레이션 기술 컨설팅 파트너에 대 한 서비스 –는 [파트너 포털](https://www.platformmodernization.org/Pages/default.aspx)합니다.  
  
## <a name="legal-notice-ssma"></a>법적 고지 사항(SSMA)  
포함된 예제 응용 프로그램을 포함하여 이 설명서는 정보 제공의 목적으로만 제공되며 Microsoft 및 그 공급자는 이 설명서에 대해서 어떠한 명시적이거나 묵시적인 보증도 하지 않습니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여, 이 설명서의 내용은 예고 없이 변경될 수 있습니다. 이 설명서의 사용이나 사용 결과에 따른 책임은 전적으로 사용자에게 있습니다.  
  
이 설명서에 포함된 예제는 주로 특정 문이나 절의 개념을 설명하거나 적당한 사용법을 보여 주기 위한 것입니다. 특정 개념이나 문에 대한 예제를 중점적으로 제공하기 위해 일반적인 데이터 유효성 검사 및 오류 처리의 일부가 제거되었으므로 대부분의 예제에 전체 프로덕션 시스템에서 일반적으로 찾을 수 있는 모든 코드가 포함되어 있지는 않습니다. 이러한 예제나 포함된 원본 코드에 대한 기술 지원은 받을 수 없습니다.  
  
다른 설명이 없는 한, 용례에 사용된 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 사람, 장소 및 이벤트 등은 실제 데이터가 아닙니다. 어떠한 실제 회사, 기관, 제품, 도메인 이름, 전자 메일 주소, 사람, 장소 또는 이벤트와도 연관시킬 의도가 없으며 그렇게 유추해서도 안 됩니다. 해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.  
  
Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허여하지 않습니다.  
  
© 2017 Microsoft Corporation. All rights reserved.  
  
Microsoft, Windows, Windows NT, Windows Server, Active Directory, ActiveX, BackOffice, bCentral, BizTalk, DirectX, Excel, Hotmail, IntelliSense, J/Direct, Jscript, Microsoft Press, MSDN, MS-DOS, Outlook, PivotChart, PivotTable, PowerPoint, SharePoint, SQL Server, Visual Basic, Visual C#, Visual C++, Visual FoxPro, Visual InterDev, Visual J#, Visual J++, Visual SourceSafe, Visual Studio, Win32, Win32s, Windows Mobile, Windows Server System 및 WinFX는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  
  
SAP NetWeaver는 독일 및 기타 여러 국가/지역에서 SAP AG의 등록 상표입니다.  
  
다른 모든 상표는 해당 소유자의 자산입니다.  
  
## <a name="documentation-policy-for-sql-server-support-and-upgrade"></a>SQL Server 지원 및 업그레이드에 대한 설명서 정책  
SQL Server 설명서의 콘텐츠는 충분한 테스트를 거친 후에만 게시됩니다. 제품 설명서(SQL Server 온라인 설명서, 추가 정보 파일, 알려진 문제점 문서 및 기술 자료 문서)에는 모든 고객의 일반적 용도에 안전하도록 충분히 강력한 SQL Server 기능에 관한 콘텐츠가 포함됩니다. 이 정책은 릴리스 및 서비스 팩에 대한 추가 정보 파일을 포함한 모든 SQL Server 설명서에 적용됩니다. 추가 정보 파일은 온라인 설명서의 확장으로 간주합니다.  
  
경우에 따라 특정 기능은 고객의 직접 사용이 금지되므로 문서화되지 않습니다. Microsoft에서 게시한 SQL Server 설명서에서도 해당 기능을 설명하는 경우 이외에는 타사 서적 또는 웹 사이트의 콘텐츠는 Microsoft 고객 지원에서 지원하지 않으므로 프로덕션 데이터베이스 또는 응용 프로그램에 사용하지 않아야 합니다.  
  
고객은 저장 프로시저, 확장 저장 프로시저, 기능, 뷰, 테이블, 열, 속성 또는 메타데이터 등을 포함하여 문서화되지 않은 API를 사용하지 않아야 합니다. Microsoft 고객 지원 서비스에 데이터베이스 또는 문서화 되지 않은 진입점을 사용 하는 응용 프로그램 지원 하지 않습니다.  
  
문서화되지 않은 진입점을 사용하는 응용 프로그램 및 데이터베이스의 경우 SQL Server의 나중 버전으로 서버 및 데이터베이스를 업그레이드하지 못할 수 있습니다. SQL Server 기능의 사용은 Microsoft SQL Server 설명서에 포함된 기능으로 제한되어야 합니다. 기능이 Microsoft SQL Server 설명서에 문서화되어 있지 않은 경우는 SQL Server의 지원되는 부분이 아닙니다.  
  
