---
title: '1단원: 데이터베이스 엔진에 연결 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 32b78c210647ab5b3722f01f334e9cb2e8bbfc13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63145473"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>1단원: 데이터베이스 엔진에 연결
  [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]을 설치할 때 설치되는 도구는 버전 및 설치 선택 사항에 따라 달라집니다. 이 단원에서는 주 도구를 검토하고 이러한 도구에 연결하는 방법을 보여 주며 보다 많은 사용자에게 권한을 부여하는 기본 기능을 수행하는 방법을 보여 줍니다.  
  
  
  
##  <a name="tools"></a> 시작 도구  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 은 다양한 도구와 함께 제공됩니다. 이 항목에서는 이 중 가장 필요한 도구를 설명하고 작업에 적합한 도구를 선택할 수 있도록 도움을 줍니다. 모든 도구는 **시작** 메뉴에서 액세스할 수 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]와 같은 일부 도구는 기본적으로 설치되지 않으며 설치하는 동안 클라이언트 구성 요소의 일부로 해당 도구를 선택해야 합니다. 아래에서 설명하는 도구에 대한 전체 설명을 보려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서에서 검색하세요. [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 에는 이러한 도구의 일부만 포함되어 있습니다.  
  
### <a name="basic-tools"></a>기본 도구  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 [!INCLUDE[ssDE](../includes/ssde-md.md)]을 관리하고 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드를 기록하는 주 도구이며 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 셸에 호스팅됩니다. 에 포함 되지 않습니다 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 에서 개별 다운로드로 사용할 수 있지만 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkId=144346)합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 클라이언트 도구 둘 다와 함께 설치됩니다. 이 관리자를 사용하면 서버 프로토콜을 설정하고, TCP 포트와 같은 프로토콜 옵션을 구성하고, 서버 서비스가 자동으로 시작되도록 구성하고, 클라이언트 컴퓨터에서 사용자가 선호하는 방법으로 연결을 설정하도록 구성할 수 있습니다. 이 도구는 더 많은 고급 연결 요소를 구성하지만 기능을 설정하지는 않습니다.  
  
### <a name="sample-database"></a>예제 데이터베이스  
 예제 데이터베이스 및 예제는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]과 함께 제공되지 않습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서에 설명된 대부분의 예제에서는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 샘플 데이터베이스가 사용됩니다.  
  
##### <a name="to-start-sql-server-management-studio"></a>SQL Server Management Studio를 시작하려면  
  
-   에 **시작** 메뉴에서 **모든 프로그램**를 가리킨 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]를 클릭 하 고 **SQL Server Management Studio**.  
  
##### <a name="to-start-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 시작하려면  
  
-   **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
##  <a name="connect"></a> Management Studio를 사용 하 여 연결  
 인스턴스 이름을 알고 있으며 컴퓨터의 Administrators 그룹 멤버로 연결하는 경우에는 동일한 컴퓨터에서 실행하는 도구의 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 쉽게 연결할 수 있습니다. 다음 절차는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 호스팅하는 컴퓨터에서 수행해야 합니다.  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>데이터베이스 엔진 인스턴스의 이름을 확인하려면  
  
1.  Administrators 그룹의 멤버로 Windows에 로그인한 다음 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 엽니다.  
  
    > [!IMPORTANT]  
    >  에 연결 하는 경우 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 온 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] 또는 [!INCLUDE[nextref_longhorn](../includes/nextref-longhorn-md.md)] (또는 이상 버전)를 마우스 오른쪽 단추로 클릭 해야 할 수 있습니다 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 클릭 하 고 **관리자 권한으로 실행** 관리자를 사용 하 여 연결 하려면 자격 증명입니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]부터는 설치 과정에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대해 선택한 로그인이 추가되므로 관리자 자격 증명은 필요하지 않습니다.  
  
2.  **서버에 연결** 대화 상자에서 **취소**를 클릭합니다.  
  
3.  등록된 서버가 표시되지 않으면 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
4.  등록된 서버 도구 모음에서 **데이터베이스 엔진** 을 선택한 상태로 **데이터베이스 엔진**을 확장하고 **로컬 서버 그룹**을 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **로컬 서버 등록**을 클릭합니다. 컴퓨터에 설치된 모든 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스가 표시됩니다. 기본 인스턴스의 이름은 지정되지 않으며 컴퓨터 이름으로 표시됩니다. 명명된 인스턴스는 컴퓨터 이름 다음에 백슬래시(\\)가 오고 마지막으로 인스턴스 이름이 붙는 형식으로 표시됩니다. [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]의 경우 설치하는 동안 이름을 변경하지 않은 한 인스턴스 이름이 *<computer_name>* \sqlexpress로 지정됩니다.  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>데이터베이스 엔진이 실행 중인지 확인하려면  
  
1.  등록된 서버에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 이름 옆에 흰색 화살표가 포함된 녹색 원이 표시되는 경우 [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 실행 중이므로 별도의 동작이 필요하지 않습니다.  
  
2.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 이름 옆에 흰색 사각형이 포함된 빨간색 원이 표시되는 경우 [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 중지된 것입니다. [!INCLUDE[ssDE](../includes/ssde-md.md)]의 이름을 마우스 오른쪽 단추로 클릭한 다음 **서비스 제어**, **시작**을 차례로 클릭합니다. 확인 대화 상자가 표시된 다음 [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 시작되고 원이 흰색 화살표가 포함된 녹색으로 바뀝니다.  
  
##### <a name="to-connect-to-the-database-engine"></a>데이터베이스 엔진에 연결하려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 **파일** 메뉴에서 **개체 탐색기 연결**을 클릭합니다.  
  
     **서버에 연결** 대화 상자가 열립니다. **서버 유형** 상자에 마지막으로 사용한 구성 요소 유형이 표시됩니다.  
  
2.  **데이터베이스 엔진**을 선택합니다.  
  
3.  **서버 이름** 상자에 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스의 이름을 입력합니다. 기본 SQL Server 인스턴스의 경우 서버 이름은 컴퓨터 이름입니다. SQL Server의 명명된 인스턴스의 경우 서버 이름은 *<computer_name>***\\***<instance_name>,*(예: **ACCTG_SRVR\SQLEXPRESS**)입니다.  
  
4.  **연결**을 클릭합니다.  
  
##  <a name="additional"></a> 추가 연결 권한 부여  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 관리자로 연결한 다음 가장 먼저 수행해야 할 태스크 중 하나는 다른 사용자가 연결할 수 있도록 권한을 부여하는 것입니다. 로그인을 만들고 이 로그인이 사용자로서 데이터베이스에 액세스할 수 있도록 권한을 부여하여 이 작업을 수행합니다. 로그인은 Windows 자격 증명을 사용하는 Windows 인증 로그인이나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 인증 정보를 저장하며 Windows 자격 증명과는 독립적인 SQL Server 인증 로그인 중 하나일 수 있습니다. 가능하면 Windows 인증을 사용하십시오.  
  
##### <a name="create-a-windows-authentication-login"></a>Windows 인증 로그인 만들기  
  
1.  이전 태스크에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 를 사용하여 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에 연결했습니다. 개체 탐색기에서 서버 인스턴스, **보안**을 차례로 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 클릭합니다.  
  
     **로그인 - 신규** 대화 상자가 나타납니다.  
  
2.  에 **일반적인** 페이지를 **로그인 이름** 상자 형식의 Windows 로그인을 입력 합니다  *\<도메인 >\\< 로그인\>* 합니다.  
  
3.  **기본 데이터베이스** 상자에서 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 를 선택합니다(사용 가능한 경우). 사용할 수 없는 경우 **master**를 선택합니다.  
  
4.  새 로그인을 관리자로 지정하려는 경우 **서버 역할** 페이지에서 **sysadmin**을 클릭하고, 지정하지 않는 경우 이 확인란을 비워 둡니다.  
  
5.  **사용자 매핑** 페이지에서 **데이터베이스에 대한** 매핑 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 을 선택합니다(사용 가능한 경우). 사용할 수 없는 경우 **master**를 선택합니다. **사용자** 상자가 해당 로그인으로 채워집니다. 이 대화 상자를 닫으면 데이터베이스에 해당 사용자가 생성됩니다.  
  
6.  **기본 스키마** 상자에 **dbo** 를 입력하여 해당 로그인을 데이터베이스 소유자 스키마에 매핑합니다.  
  
7.  **보안 개체** 및 **상태** 상자의 기본 설정을 적용한 다음 **확인** 을 클릭하여 로그인을 만듭니다.  
  
> [!IMPORTANT]  
>  이 섹션의 내용은 초보자를 위한 기본 정보입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 강력한 보안 환경을 제공하며 보안은 데이터베이스 작업의 매우 중요한 한 측면입니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: 다른 컴퓨터에서 연결](lesson-2-connecting-from-another-computer.md)  
  
  
