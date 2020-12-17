---
title: SQL Server 구성 관리자 도움말
description: SQL Server 구성 관리자에 대해 알아봅니다. 이 구성 관리자를 사용하여 SQL Server 서비스를 관리하고 네트워크 연결을 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 02/01/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: a9804ef6634a576cbdb8ee32a21b1b1d174d9825
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483795"
---
# <a name="sql-server-configuration-manager-help"></a>SQL Server 구성 관리자 도움말
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 연결을 구성할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용하면 데이터베이스 개체를 만들거나 관리하고, 보안을 구성하고, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]쿼리를 작성할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  

 > [!TIP]
 > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on Linux를 구성해야 하는 경우 **mssql-conf** 도구를 사용합니다. 자세한 내용은 [mssql-conf 도구를 사용하여 SQL Server on Linux 구성](../../linux/sql-server-linux-configure-mssql-conf.md)을 참조하세요.

 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 대화 상자에 대한 F1 도움말 항목을 제공합니다.  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자로 구성할 수 없습니다.  
  
## <a name="services"></a>Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 서비스를 관리합니다. 이러한 태스크의 대부분은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스 대화 상자를 사용하여 수행할 수도 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 자신이 관리하는 서비스에 대해 서비스 계정 변경 시 올바른 권한을 적용하는 등 Windows 서비스 대화 상자에서는 지원하지 않는 작업을 추가로 지원합니다. 일반 Windows 서비스 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 구성할 경우 서비스가 작동하지 않을 수도 있습니다.  
  
 다음 태스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용할 수 있습니다.  
  
-   서비스 시작, 중지 및 일시 중지  
  
-   자동 또는 수동으로 시작하도록 서비스 구성, 서비스 비활성화 또는 기타 서비스 설정 변경  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용되는 계정의 암호 변경  
  
-   추적 플래그(명령줄 매개 변수)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작  
  
-   서비스 속성 보기  
  
## <a name="sql-server-network-configuration"></a>SQL Server 네트워크 구성  
 이 컴퓨터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 관련된 다음 태스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 프로토콜 사용 또는 사용 안 함  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 프로토콜 구성  
  
> [!NOTE]  
>  프로토콜을 구성하고 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 연결하는 방법에 대한 간략한 자습서는 [자습서: 데이터베이스 엔진 시작](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)을 참조하세요.  
  
## <a name="sql-server-native-client-configuration"></a>SQL Server Native Client 구성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 네트워크 라이브러리를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결합니다. 이 컴퓨터의 클라이언트 애플리케이션과 관련된 다음 태스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
-   이 컴퓨터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 애플리케이션의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때 프로토콜 순서를 지정합니다.  
  
-   클라이언트 연결 프로토콜을 구성합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 애플리케이션의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 별칭을 만들어 클라이언트가 사용자 지정 연결 문자열을 사용하여 연결할 수 있도록 합니다.  
  
 각 태스크에 대한 자세한 내용은 F1 도움말을 참조하십시오.  
  
#### <a name="to-open-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 열려면  
  
-   **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server** (버전), **구성 도구** 를 차례로 가리킨 다음 **SQL Server 구성 관리자** 를 클릭합니다.  
  
  
 **[!INCLUDE[win8](../../includes/win8-md.md)]을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에 액세스하려면**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 독립 실행형 프로그램이 아니라 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 프로그램용 스냅인이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[win8](../../includes/win8-md.md)]을(를) 실행할 때 애플리케이션으로 표시되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 열려면 **검색** 참의 **앱** 아래에 **SQLServerManager12.msc**([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) 또는 **SQLServerManager11.msc**([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])를 입력한 다음, **Enter** 키를 누릅니다.  
  

## <a name="see-also"></a>참고 항목  
 [SQL Server 서비스](../../tools/configuration-manager/sql-server-services.md)   
 [SQL Server 네트워크 구성](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [SQL Native Client 11.0 구성](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [네트워크 프로토콜 선택](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
