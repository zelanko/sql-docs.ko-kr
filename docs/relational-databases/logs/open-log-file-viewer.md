---
title: 로그 파일 뷰어 열기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19dfb08572ae79a3ca2d82609641426791957924
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32943308"
---
# <a name="open-log-file-viewer"></a>로그 파일 뷰어 열기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 로그 파일 뷰어를 사용하여 다음 로그에 기록되는 오류 및 이벤트에 대한 정보에 액세스할 수 있습니다.  
  
-   감사 컬렉션  
  
-   데이터 컬렉션  
  
-   데이터베이스 메일  
  
-   작업 기록  
  
-   SQL Server  
  
-   SQL Server 에이전트  
  
-   Windows 이벤트(이벤트 뷰어에서도 이러한 Windows 이벤트에 액세스할 수 있음)  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 등록된 서버를 사용하여 로컬 또는 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그 파일을 볼 수 있습니다. 등록된 서버를 사용하면 인스턴스가 온라인인지 오프라인인지 관계없이 로그 파일을 볼 수 있습니다. 온라인 액세스에 대한 자세한 내용은 이 항목의 "등록된 서버에서 온라인 로그 파일을 보려면" 절차를 참조하십시오. 오프라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일에 액세스하는 방법은 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)를 참조하세요.  
  
 로그 파일 뷰어는 보려는 정보에 따라 여러 방법으로 열 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a> 사용 권한  
 온라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 로그 파일에 액세스하려면 securityadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
 오프라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 로그 파일에 액세스하려면 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 네임스페이스 및 로그 파일이 저장된 폴더 모두에 대한 읽기 권한이 있어야 합니다. 자세한 내용은 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)항목의 보안 섹션을 참조하세요.  
  
### <a name="security"></a>보안  
 securityadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
### <a name="view-log-files"></a>로그 파일 보기  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>일반적인 SQL Server 작업과 관련된 로그를 보려면  
  
1.  개체 탐색기에서 **관리**를 확장합니다.  
  
2.  다음 중 하나를 수행합니다.  
  
    -   **SQL Server 로그**를 마우스 오른쪽 단추로 클릭하고 **보기**를 가리킨 다음 **SQL Server 로그** 또는 **SQL Server 및 Windows 로그**를 클릭합니다.  
  
    -   **SQL Server 로그**를 확장하고 로그 파일을 마우스 오른쪽 단추로 클릭한 다음 **SQL Server 로그 보기**를 클릭합니다. 로그 파일을 두 번 클릭해도 됩니다.  
  
     로그에는 **데이터베이스 메일**, **SQL Server**, **SQL Server 에이전트**및 **Windows NT**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>작업과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **SQL Server 에이전트**를 확장하고 **작업**을 마우스 오른쪽 단추로 클릭한 다음 **기록 보기**를 클릭합니다.  
  
     로그에는 **데이터베이스 메일**, **작업 기록**및 **SQL Server 에이전트**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>유지 관리 계획과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **관리**를 확장하고 **유지 관리 계획**을 마우스 오른쪽 단추로 클릭한 다음 **기록 보기**를 클릭합니다.  
  
     로그에는 **데이터베이스 메일**, **작업 기록**, **유지 관리 계획**, **원격 유지 관리 계획**및 **SQL Server 에이전트**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>데이터 컬렉션과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **관리**를 확장하고 **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **로그 보기**를 클릭합니다.  
  
     로그에는 **데이터 컬렉션**, **작업 기록**및 **SQL Server 에이전트**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>데이터베이스 메일과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **관리**를 확장하고 **데이터베이스 메일**을 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 메일 로그 보기**를 클릭합니다.  
  
     로그에는 **데이터베이스 메일, 작업 기록**, **유지 관리 계획**, **원격 유지 관리 계획**, **SQL Server**, **SQL Server 에이전트**및 **Windows NT**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>감사 컬렉션과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **보안**, **감사**를 차례로 확장하고 감사를 마우스 오른쪽 단추로 클릭한 다음 **감사 로그 보기**를 클릭합니다.  
  
     로그에는 **감사 컬렉션** 및 **Windows NT**가 포함됩니다.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>감사 컬렉션과 관련된 로그를 보려면  
  
-   개체 탐색기에서 **보안**, **감사**를 차례로 확장하고 감사를 마우스 오른쪽 단추로 클릭한 다음 **감사 로그 보기**를 클릭합니다.  
  
     로그에는 **감사 컬렉션** 및 **Windows NT**가 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 파일 뷰어](../../relational-databases/logs/log-file-viewer.md)   
 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)  
  
  
