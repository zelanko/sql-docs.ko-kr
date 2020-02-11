---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 224facf54b0cde09f97010be472e3cc28754e94b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62757004"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 프로그램 개발자를 대상 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 으로 하는의 실행 모드입니다. [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` `LocalDB`설치는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 시작 하는 데 필요한 최소한의 파일 집합을 복사 합니다. 가 `LocalDB` 설치 되 면 개발자가 특수 연결 문자열을 사용 하 여 연결을 시작 합니다. 연결할 때, 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라가 자동으로 생성되고 시작되므로 복잡한 태스크 또는 시간이 많이 걸리는 구성 태스크 없이 애플리케이션에서 데이터베이스를 사용하도록 할 수 있습니다. 개발자 도구는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 전체 서버 인스턴스를 관리할 필요 없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 작성하고 테스트할 수 있게 해주는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진을 개발자에게 제공합니다.
 인스턴스 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` 는 유틸리티를 `SqlLocalDB.exe` 사용 하 여 관리 됩니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`는 사용 되지 않는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 사용자 인스턴스 기능 대신 사용 해야 합니다.  
  
## <a name="installing-localdb"></a>LocalDB 설치  
 을 설치 `LocalDB` 하는 기본 방법은 SqlLocalDB 프로그램을 사용 하는 것입니다. `LocalDB`는의 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]SKU를 설치할 때 사용할 수 있는 옵션입니다. 설치 `LocalDB` 중 **기능 선택** 페이지에서를 선택 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]합니다. 각 주 `LocalDB` [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 버전에는 이진 파일을 하나만 설치할 수 있습니다. 여러 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스를 시작할 수 있으며, 이러한 프로세스에는 모두 동일한 이진 파일이 사용됩니다. 로 시작 된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에는 다음과 `LocalDB` 같은 제한 사항이 있습니다.[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Description  
 설치 `LocalDB` 프로그램은 SqlLocalDB 프로그램을 사용 하 여 컴퓨터에 필요한 파일을 설치 합니다. 설치 되 면 `LocalDB` 는 데이터베이스를 만들고 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수 있는의 인스턴스입니다. 데이터베이스의 시스템 데이터베이스 파일은 사용자의 로컬 AppData 경로에 저장되는데, 이 경로는 일반적으로 숨겨져 있습니다. 예를 들어 **C:\Users\\<사용자\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\** 입니다. 사용자 데이터베이스 파일은 사용자가 지정하는 위치(일반적으로 **C:\Users\\<사용자\>\Documents\\** 폴더 내 임의 위치)에 저장됩니다.  
  
 응용 프로그램에를 포함 `LocalDB` 하는 방법에 대 한 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 자세한 내용은 설명서 [로컬 데이터 개요](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [연습: SQL Server LocalDB 데이터베이스 만들기](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)및 [연습: SQL Server localdb 데이터베이스의 데이터에 연결 (Windows Forms)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)을 참조 하세요.  
  
 `LocalDB` Api에 대 한 자세한 내용은 [SQL SERVER EXPRESS LocalDB 인스턴스 API 참조](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) 및 [localdbstartinstance 함수](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)를 참조 하세요.  
  
 SqlLocalDb 유틸리티는의 `LocalDB`새 인스턴스를 만들고, 인스턴스 `LocalDB`를 시작 및 중지 하 고,를 관리 `LocalDB`하는 데 도움이 되는 옵션을 제공 합니다.  SqlLocalDb 유틸리티에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
 에 대 한 `LocalDB` 인스턴스 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS로 설정 되며 변경할 수 없습니다. 데이터베이스 수준, 열 수준 및 식 수준 데이터 정렬은 일반적으로 지원됩니다. 포함된 데이터베이스는 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)에 정의된 메타데이터 및 tempdb 데이터 정렬 규칙을 따릅니다.  
  
### <a name="restrictions"></a>제한  
 `LocalDB`은 (는) 병합 복제 구독자 일 수 없습니다.  
  
 `LocalDB`에서는 FILESTREAM을 지원 하지 않습니다.  
  
 `LocalDB`Service Broker에 대 한 로컬 큐만 허용 합니다.  
  
 NT 권한으로 `LocalDB` 구성 된 기본 제공 계정에서 소유 하는 인스턴스는 windows 파일 시스템 리디렉션으로 인해 관리 효율성 문제가 발생할 수 있습니다. 대신 일반 windows 계정을 소유자로 사용 합니다.  
  
### <a name="automatic-and-named-instances"></a>자동 및 명명된 인스턴스  
 `LocalDB`는 자동 인스턴스 및 명명 된 인스턴스와 같은 두 가지 인스턴스를 지원 합니다.  
  
-   의 `LocalDB` 자동 인스턴스는 공용입니다. 이 인스턴스는 자동으로 생성 및 관리되고 모든 애플리케이션에서 사용될 수 있습니다. 사용자의 컴퓨터에 `LocalDB` 설치 된의 `LocalDB` 모든 버전에 대해 하나의 자동 인스턴스가 존재 합니다. 의 자동 인스턴스 `LocalDB` 는 원활한 인스턴스 관리를 제공 합니다. 인스턴스를 만들 필요 없이 그대로 작동합니다. 따라서 애플리케이션을 쉽게 설치할 수 있으며 다른 컴퓨터에 쉽게 마이그레이션할 수 있습니다. 대상 컴퓨터에 지정된 버전의 `LocalDB`가 설치되어 있을 경우 해당 버전에 대한 자동 `LocalDB` 인스턴스를 대상 컴퓨터에서도 사용할 수 있습니다. 자동 인스턴스는 `LocalDB` 예약 된 네임 스페이스에 속하는 인스턴스 이름에 대 한 특수 한 패턴을 갖습니다. 이렇게 하면 명명 된 인스턴스의 이름 충돌을 `LocalDB`방지할 수 있습니다. 자동 인스턴스의 이름은 **MSSQLLocalDB**입니다.  
  
-   의 `LocalDB` 명명 된 인스턴스는 전용입니다. 이 인스턴스는 인스턴스 만들기와 관리를 담당하는 단일 애플리케이션에 의해 소유됩니다. 명명된 인스턴스는 다른 인스턴스로부터의 격리를 제공하고 다른 데이터베이스 사용자와의 리소스 경합을 줄여서 성능을 향상시킬 수 있습니다. 관리 되는 응용 프로그램의 경우 관리 되는 응용 `LocalDB` 프로그램 에서도 API를 사용할 수 있지만 관리 되는 응용 프로그램의 경우 사용자가 관리 api를 통해 명시적으로 명명 된 인스턴스를 만들어야 합니다. 의 `LocalDB` 각 명명 된 인스턴스에는 해당 `LocalDB` `LocalDB` 이진 파일 집합을 가리키는 연결 된 버전이 있습니다. 의 `LocalDB` 인스턴스 이름은 `sysname` 데이터 형식이 며 최대 128 자까지 지정할 수 있습니다. 이는 이름을 16 ASCII 문자의 일반 NetBIOS [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이름으로 제한 하는의 일반적인 명명 된 인스턴스와 다릅니다. 인스턴스의 이름에는 파일 이름 `LocalDB` 내에 유효한 모든 유니코드 문자가 포함 될 수 있습니다.  자동 인스턴스 이름을 사용하는 명명된 인스턴스는 자동 인스턴스가 됩니다.  
  
 컴퓨터의 다른 사용자는 동일한 이름의 인스턴스를 가질 수 있습니다. 각 인스턴스는 다른 사용자로 실행되는 서로 다른 프로세스입니다.  
  
## <a name="shared-instances-of-localdb"></a>LocalDB의 공유 인스턴스  
 컴퓨터의 여러 사용자가의 `LocalDB`단일 인스턴스에 연결 해야 하는 시나리오를 지원 하기 위해는 `LocalDB` 인스턴스 공유를 지원 합니다. 인스턴스 소유자는 컴퓨터의 다른 사용자가 자신의 인스턴스에 연결하도록 허용할 수 있습니다. 의 `LocalDB` 자동 및 명명 된 인스턴스를 모두 공유할 수 있습니다. 
  `LocalDB` 인스턴스를 공유하려면 사용자가 해당 인스턴스에 대한 공유 이름(별칭)을 선택합니다. 공유 이름은 컴퓨터의 모든 사용자에게 표시되기 때문에 이 공유 이름은 해당 컴퓨터에서 고유해야 합니다. 인스턴스의 `LocalDB` 공유 이름은의 `LocalDB`명명 된 인스턴스와 형식이 동일 합니다.  
  
 컴퓨터의 관리자만의 `LocalDB`공유 인스턴스를 만들 수 있습니다. 의 `LocalDB` 공유 인스턴스는 관리자 또는 공유 인스턴스 소유자가 공유 하지 않을 수 있습니다 `LocalDB`. 인스턴스를 공유 하 고 공유 하지 `LocalDB`않는 경우 `LocalDB` API `LocalDBShareInstance` 의 `LocalDBUnShareInstance` 및 메서드를 사용 하거나 SqlLocalDb 유틸리티의 공유 및 공유 해제 옵션을 사용 합니다.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>LocalDB 시작 및 LocalDB에 연결  
  
### <a name="connecting-to-the-automatic-instance"></a>자동 인스턴스에 연결  
 를 사용 `LocalDB` 하는 가장 쉬운 방법은 연결 문자열 **"Server = (localdb) \MSSQLLocalDB; Integrated Security = true"** 를 사용 하 여 현재 사용자가 소유한 자동 인스턴스에 연결 하는 것입니다. 파일 이름을 사용하여 특정 데이터베이스에 연결하려면 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 와 유사한 연결 문자열을 사용하여 연결합니다.  
  
> [!NOTE]  
>  컴퓨터의 사용자가에 처음으로 `LocalDB`연결 하려고 할 때 자동 인스턴스를 만들고 시작 해야 합니다. 인스턴스를 만드는 추가 시간으로 인해 시간 초과 메시지와 함께 연결 시도가 실패할 수 있습니다. 이 경우 만들기 프로세스가 완료되도록 몇 초 정도 기다린 후에 다시 연결하세요.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>명명된 인스턴스 만들기 및 연결  
 자동 인스턴스 외에도에서는 `LocalDB` 명명 된 인스턴스를 지원 합니다. SqlLocalDB 프로그램을 사용 하 여의 `LocalDB`명명 된 인스턴스를 만들고 시작 하 고 중지할 수 있습니다. SqlLocalDB.exe에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 위에서 마지막 줄은 다음과 비슷한 정보를 반환합니다.  
  
|||  
|-|-|  
|속성|"LocalDBApp1"|  
|버전|\<현재 버전>|  
|공유 이름|""|  
|소유자|"\<Windows 사용자>"|  
|자동 만들기|예|  
|시스템 상태|실행 중|  
|마지막 시작 시간|\<날짜 및 시간>|  
|인스턴스 파이프 이름|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  4.0.2 전에 응용 프로그램에서 .NET 버전을 사용 하는 경우의 명명 된 파이프에 직접 연결 해야 `LocalDB`합니다. 인스턴스 파이프 이름 값은 인스턴스가 수신 대기 `LocalDB` 중인 명명 된 파이프입니다. 인스턴스 파이프 이름 다음의 `LocalDB` 인스턴스는 인스턴스가 시작 될 때마다 변경 됩니다. `LocalDB` 를 사용 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하 여 인스턴스에 연결 하려면 **연결 대상 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ** 대화 상자의 **서버 이름** 상자에 인스턴스 파이프 이름을 입력 합니다. 사용자 지정 프로그램에서와 비슷한 연결 문자열을 `LocalDB` 사용 하 여 인스턴스에 대 한 연결을 설정할 수 있습니다.`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>LocalDB의 공유 인스턴스에 연결  
 공유 인스턴스에 연결 하려면 공유 인스턴스에 대해 `LocalDB` 예약 된 네임 스페이스를 참조 하기 위해 연결 문자열에 (점 + 백슬래시)를 추가 **합니다.\\ ** 예를 들어 명명 `LocalDB` `AppData` 된의 공유 인스턴스에 연결 하려면 연결 문자열의 일부로와 `(localdb)\.\AppData` 같은 연결 문자열을 사용 합니다. 자신이 소유 하 고 있지 않은의 `LocalDB` 공유 인스턴스에 연결 하는 사용자에 게는 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인이 있어야 합니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 문제 해결 `LocalDB`에 대 한 자세한 내용은 [SQL Server 2012 Express LocalDB 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)을 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 인스턴스 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 는 사용자가 사용 하기 위해 만든 인스턴스입니다. 컴퓨터의 모든 사용자는 인스턴스 `LocalDB`를 사용 하 여 데이터베이스를 만들고, 해당 사용자 프로필에 파일을 저장 하 고, 해당 자격 증명으로 프로세스를 실행할 수 있습니다. 기본적으로 인스턴스에 대 한 액세스 `LocalDB` 는 소유자에 게 제한 됩니다. 에 포함 된 데이터는 `LocalDB` 데이터베이스 파일에 대 한 파일 시스템 액세스를 통해 보호 됩니다. 사용자 데이터베이스 파일을 공유 위치에 저장 하는 경우 해당 사용자가 소유한 인스턴스 `LocalDB` 를 사용 하 여 해당 위치에 대 한 파일 시스템 액세스 권한이 있는 모든 사용자가 데이터베이스를 열 수 있습니다. 데이터베이스 파일이 사용자 데이터 폴더와 같은 보호되는 위치에 있으면 해당 사용자 및 해당 폴더에 대한 액세스 권한이 있는 관리자만 데이터베이스를 열 수 있습니다. 파일 `LocalDB` 은 한 번 `LocalDB` 에 하나의 인스턴스만 열 수 있습니다.  
  
> [!NOTE]  
>  `LocalDB`는 항상 사용자 보안 컨텍스트에서 실행 됩니다. 즉, `LocalDB` 은 로컬 관리자 그룹의 자격 증명으로 실행 되지 않습니다. 즉, 로컬 Administrators 그룹의 멤버 자격을 `LocalDB` 고려 하지 않고 소유 사용자의 Windows 계정을 사용 하 여 인스턴스에서 사용 하는 모든 데이터베이스 파일에 액세스할 수 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)  
  
  
