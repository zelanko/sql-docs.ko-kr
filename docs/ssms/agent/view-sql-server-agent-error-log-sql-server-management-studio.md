---
title: SQL Server 에이전트 오류 로그 보기(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3459644d9f2b749b431ec49656328f570a9ec0e2
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67680574"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에이전트 오류 로그를 보는 방법에 대해 설명합니다.  
  
로그 파일 뷰어는 다양한 구성 요소의 로그 정보를 표시합니다. 로그 파일 뷰어를 연 다음 **로그 선택** 창을 사용하여 표시할 로그를 선택할 수 있습니다. 각 로그는 해당 로그 유형에 적합한 열을 표시합니다. 사용 가능한 로그는 로그 파일 뷰어를 여는 방법에 따라 다릅니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트 오류 로그를 보려면](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정에 필요한 Windows 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 설정](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-view-the-includessnoversionincludesssnoversion-mdmd-agent-error-log"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그를 보려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 보려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그가 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **오류 로그** 폴더를 확장합니다.  
  
4.  보려는 오류 로그를 마우스 오른쪽 단추로 클릭하고 **에이전트 로그 보기**를 선택합니다.  
  
    다음 옵션은 **로그 파일 뷰어-** _server_name_ 대화 상자에서 사용할 수 있습니다.  
  
    **로그 로드**  
    로드할 로그 파일을 지정할 수 있는 대화 상자를 엽니다.  
  
    **내보내기**  
    **로그 파일 요약** 표에 표시된 정보를 텍스트 파일로 내보낼 수 있는 대화 상자를 엽니다.  
  
    **새로 고침**  
    선택한 로그의 뷰를 새로 고칩니다. **새로 고침** 단추를 누르면 필터 설정을 적용하는 동안 대상 서버에서 선택한 로그를 다시 읽습니다.  
  
    **필터**  
    **연결**, **날짜**또는 기타 **일반** 필터 조건과 같이 로그 파일 필터링에 사용되는 설정을 지정할 수 있는 대화 상자를 엽니다.  
  
    **검색**  
    로그 파일에서 특정 텍스트를 검색합니다. 와일드카드 문자를 사용한 검색은 지원되지 않습니다.  
  
    **중지**  
    로그 파일 항목의 로드를 중지합니다. 예를 들어 원격 또는 오프라인 로그 파일을 로드하는 데 시간이 오래 걸리며 최근 항목만 보려는 경우 이 옵션을 사용할 수 있습니다.  
  
    **로그 파일 요약**  
    이 정보 창에는 로그 파일 필터링에 대한 요약이 표시됩니다. 파일을 필터링하지 않은 경우 **적용된 필터 없음**이 표시됩니다. 로그에 필터를 적용한 경우에는 **로그 항목 필터링 조건:** <filter criteria>라는 텍스트가 표시됩니다.  
  
    **선택한 행 정보**  
    선택한 이벤트 행에 대한 추가 정보를 페이지 아래쪽에 표시하려면 해당 행을 선택합니다. 열을 표의 새 위치로 끌어서 다시 정렬할 수 있습니다. 표 머리글의 열 구분선을 왼쪽이나 오른쪽으로 끌어 열의 크기를 조정할 수도 있습니다. 열 내용에 맞게 열 너비를 자동 조정하려면 표 머리글의 열 구분선을 두 번 클릭합니다.  
  
    **인스턴스**  
    이벤트가 발생한 인스턴스의 이름입니다. 이 이름은 *컴퓨터 이름*\\*인스턴스 이름*으로 표시됩니다.  
  
    **Date**  
    이벤트의 날짜를 표시합니다.  
  
    **원본**  
    서비스의 이름(예: MSSQLSERVER)과 같이 이벤트가 생성된 원본 기능을 표시합니다. 이 열은 일부 로그 유형의 경우에만 나타납니다.  
  
    **메시지**  
    이벤트와 관련된 메시지를 표시합니다.  
  
    **로그 유형**  
    이벤트가 속한 로그의 유형을 표시합니다. 선택한 모든 로그가 로그 파일 요약 창에 나타납니다.  
  
    **로그 원본**  
    이벤트가 캡처되는 원본 로그에 대한 설명을 표시합니다.  
  
5.  완료되면 **닫기**를 클릭합니다.  
  
