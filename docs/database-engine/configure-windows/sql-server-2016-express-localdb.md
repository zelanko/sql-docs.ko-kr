---
title: SQL Server 2016 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: high-availability
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
ms.openlocfilehash: 723d35453dcc01fb333a8c3a212a6a1b288cce8b
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851788"
---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 이전 버전의 SQL Server와 관련된 내용은 [SQL Server 2014 Express LocalDB(영문)](https://msdn.microsoft.com/library/hh510202(SQL.120).aspx)를 참조하세요.

Microsoft SQL Server 2016 Express **LocalDB** 는 개발자를 대상으로 하는 [SQL Server Express](../../sql-server/editions-and-components-of-sql-server-2016.md) 기능입니다. SQL Server 2016 Express with Advanced Services에서 사용할 수 있습니다.  

 **LocalDB** 를 설치하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 시작하는 데 필요한 최소한의 파일 집합이 복사됩니다. LocalDB가 설치되면 특수 연결 문자열을 사용하여 연결을 시작할 수 있습니다. 연결할 때, 필요한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라가 자동으로 생성되고 시작되므로 복잡한 구성 태스크 없이 응용 프로그램에서 데이터베이스를 사용하도록 할 수 있습니다. 개발자 도구는 개발자가 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 전체 서버 인스턴스를 관리할 필요 없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 작성하고 테스트할 수 있게 해주는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 제공할 수 있습니다. 
 
 
 ## <a name="try-it-out"></a>사용해 보세요! 
  
-   SQL Server 2016 Express를 다운로드하고 설치하려면 **[SQL Server 다운로드](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)** 로 이동하세요. LocalDB는 설치 중에 선택하는 기능이며, 미디어를 다운로드할 때 사용할 수 있습니다. 미디어를 다운로드하는 경우 **Visual Studio 설치 관리자**를 통해 **Express Advanced** 또는 **LocalDB** 패키지를 선택합니다. **Visual Studio 설치 관리자**에서 **.NET 데스크톱 개발** 워크로드의 일부로 또는 개별 구성 요소로서 SQL Server Express LocalDB를 설치할 수 있습니다.

   > [!TIP]
   > 또한 LocalDB를 Visual Studio 2017의 일부로 설치할 수도 있습니다. Visual Studio 설치 중에 SQL Server Express LocalDB를 포함하는 **.NET 데스크톱 개발** 워크로드를 선택합니다.
  
-   Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/services/virtual-machines/sql-server/)** 로 이동하여 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]이(가) 이미 설치된 가상 머신을 실행해 보세요.  
  
## <a name="install-localdb"></a>LocalDB 설치  
 설치 마법사를 통해 또는 SqlLocalDB.msi 프로그램을 사용하여 **LocalDB** 를 설치합니다. **LocalDB** 는 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]설치 시 옵션 항목입니다. 
 
설치 중에 **기능 선택/공유 기능** 페이지에서 **LocalDB** 를 선택합니다. 각 주요 **버전에 대해** LocalDB [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이진 파일을 하나만 설치할 수 있습니다. 여러 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스를 시작할 수 있으며, 이러한 프로세스에는 모두 동일한 이진 파일이 사용됩니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]LocalDB**로 시작된**  인스턴스는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]과(와) 동일한 제한 사항을 갖습니다.   

 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** 인스턴스는 **SqlLocalDB.exe** 유틸리티를 사용하여 관리됩니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** LocalDB [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 를 사용해야 합니다. 
  
## <a name="description"></a>설명  
 **LocalDB** 설치 프로그램은 SqlLocalDB.msi 프로그램을 사용하여 컴퓨터에 필요한 파일을 설치합니다. 설치가 끝나면 **LocalDB** 는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 데이터베이스를 만들고 열 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 됩니다. 데이터베이스의 시스템 데이터베이스 파일은 사용자의 로컬 AppData 경로에 저장되는데, 이 경로는 일반적으로 숨겨져 있습니다. 예를 들어 **C:\Users\\<사용자\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**입니다. 사용자 데이터베이스 파일은 사용자가 지정하는 위치(일반적으로 **C:\Users\\<사용자\>\Documents\\** 폴더 내 임의 위치)에 저장됩니다.  
  
 응용 프로그램에 **LocalDB**를 포함하는 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서 [로컬 데이터 개요](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [연습: SQL Server LocalDB 데이터베이스 만들기](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx) 및 [연습: SQL Server LocalDB 데이터베이스의 데이터에 연결(Windows Forms)](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)을 참조하세요.  
  
 **LocalDB** API에 대한 자세한 내용은 [SQL Server Express LocalDB 인스턴스 API 참조](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) 및 [LocalDBStartInstance 함수](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)를 참조하세요.  
  
 SqlLocalDb 유틸리티는 새로운 **LocalDB**인스턴스를 만들고, **LocalDB**인스턴스를 시작 및 중지할 수 있으며, **LocalDB**를 관리하는 데 도움이 되는 옵션을 포함합니다.  SqlLocalDb 유틸리티에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
 **LocalDB** 의 인스턴스 데이터 정렬은 SQL_Latin1_General_CP1_CI_AS로 설정되며 변경할 수 없습니다. 데이터베이스 수준, 열 수준 및 식 수준 데이터 정렬은 일반적으로 지원됩니다. 포함된 데이터베이스는 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)에 정의된 메타데이터 및 tempdb 데이터 정렬 규칙을 따릅니다.  
  
### <a name="restrictions"></a>Restrictions  
 **LocalDB** 는 병합 복제 구독자일 수 없습니다.  
  
 **LocalDB** 는 FILESTREAM을 지원하지 않습니다.  
  
 **LocalDB** 는 Service Broker에 대한 로컬 큐만 허용합니다.  
  
 기본 제공 계정(예: NT AUTHORITY\SYSTEM)에서 소유한 **LocalDB** 의 인스턴스에서 Windows 파일 시스템 리디렉션으로 인해 관리 효율성 문제가 발생할 수 있으므로, 대신 일반 Windows 계정을 소유자로 사용합니다.  
  
### <a name="automatic-and-named-instances"></a>자동 및 명명된 인스턴스  
 **LocalDB** 에서는 Automatic Instance 및 Named Instance의 두 가지 인스턴스를 지원합니다.  
  
-   **LocalDB** 의 자동 인스턴스는 공용입니다. 이 인스턴스는 자동으로 생성 및 관리되고 모든 응용 프로그램에서 사용될 수 있습니다. 사용자의 컴퓨터에 설치되는 모든 버전의 **LocalDB** 에 대해 하나의 자동 **LocalDB** 인스턴스가 있습니다. 자동 **LocalDB** 인스턴스는 효율적으로 관리됩니다. 인스턴스를 만들 필요 없이 그대로 작동합니다. 따라서 응용 프로그램을 쉽게 설치할 수 있으며 다른 컴퓨터에 쉽게 마이그레이션할 수 있습니다. 대상 컴퓨터에 지정된 버전의 **LocalDB** 가 설치되어 있을 경우 해당 버전에 대한 자동 **LocalDB** 인스턴스를 대상 컴퓨터에서도 사용할 수 있습니다. 자동 **LocalDB** 인스턴스는 예약된 네임스페이스에 속하는 특수한 인스턴스 이름 패턴을 사용합니다. 이러한 방식은 명명된 **LocalDB**인스턴스와 이름이 충돌하는 것을 방지합니다. 자동 인스턴스의 이름은 **MSSQLLocalDB**입니다.  
  
-   **LocalDB** 의 명명된 인스턴스는 전용입니다. 이 인스턴스는 인스턴스 만들기와 관리를 담당하는 단일 응용 프로그램에 의해 소유됩니다. 명명된 인스턴스는 다른 인스턴스로부터의 격리를 제공하고 다른 데이터베이스 사용자와의 리소스 경합을 줄여서 성능을 향상시킬 수 있습니다. 명명된 인스턴스는 사용자가 **LocalDB** 관리 API를 통해 명시적으로 또는 관리 응용 프로그램에 대한 app.config 파일을 통해 암시적으로(관리 응용 프로그램에서 필요에 따라 해당 API를 사용하더라도) 만들어야 합니다. **LocalDB** 의 각 명명된 인스턴스에는 해당 **LocalDB** 바이너리 집합을 가리키는 **LocalDB** 버전이 연결되어 있습니다. **LocalDB** 의 인스턴스 이름은 **sysname** 데이터 형식이며 최대 128자를 포함할 수 있습니다. 이러한 특성은 이름을 16 ASCII 문자의 일반 NetBIOS 이름으로 제한하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일반적인 명명된 인스턴스와 다릅니다. **LocalDB** 인스턴스 이름은 파일 이름에 사용할 수 있는 모든 유니코드 문자를 포함할 수 있습니다.  자동 인스턴스 이름을 사용하는 명명된 인스턴스는 자동 인스턴스가 됩니다.  
  
 컴퓨터의 다른 사용자는 동일한 이름의 인스턴스를 가질 수 있습니다. 각 인스턴스는 다른 사용자로 실행되는 서로 다른 프로세스입니다.  
  
## <a name="shared-instances-of-localdb"></a>LocalDB의 공유 인스턴스  
 컴퓨터의 여러 사용자가 단일 **LocalDB**인스턴스에 연결해야 하는 시나리오를 지원하기 위해 **LocalDB** 는 인스턴스 공유를 지원합니다. 인스턴스 소유자는 컴퓨터의 다른 사용자가 자신의 인스턴스에 연결하도록 허용할 수 있습니다. **LocalDB** 의 자동 및 명명된 인스턴스는 모두 공유 가능합니다. **LocalDB** 인스턴스를 공유하려면 사용자가 해당 인스턴스에 대한 공유 이름(별칭)을 선택합니다. 공유 이름은 컴퓨터의 모든 사용자에게 표시되기 때문에 이 공유 이름은 해당 컴퓨터에서 고유해야 합니다. **LocalDB** 인스턴스의 공유 이름은 **LocalDB**의 명명된 인스턴스와 형식이 동일합니다.  
  
 컴퓨터의 관리자만 **LocalDB**의 공유 인스턴스를 만들 수 있습니다. **LocalDB** 의 공유 인스턴스는 관리자 또는 **LocalDB**의 공유 인스턴스 소유자가 공유를 해제할 수 있습니다. **LocalDB**인스턴스를 공유 및 공유 해제하려면 `LocalDBShareInstance` LocalDB `LocalDBUnShareInstance` API의 **및** 메서드를 사용하거나 SqlLocalDb 유틸리티의 공유 및 공유 해제 옵션을 사용합니다.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>LocalDB 시작 및 LocalDB에 연결  
  
### <a name="connecting-to-the-automatic-instance"></a>자동 인스턴스에 연결  
 **LocalDB** 를 사용하는 가장 쉬운 방법은 연결 문자열 **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"** 를 사용하여 현재 사용자가 소유한 자동 인스턴스에 연결하는 것입니다. 파일 이름을 사용하여 특정 데이터베이스에 연결하려면 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 와 유사한 연결 문자열을 사용하여 연결합니다.  
  
> [!NOTE]  
>  컴퓨터에서 사용자가 처음으로 **LocalDB**에 연결하려고 시도하는 경우 자동 인스턴스가 생성되고 시작되어야 합니다. 인스턴스를 만드는 추가 시간으로 인해 시간 초과 메시지와 함께 연결 시도가 실패할 수 있습니다. 이 경우 만들기 프로세스가 완료되도록 몇 초 정도 기다린 후에 다시 연결하세요.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>명명된 인스턴스 만들기 및 연결  
 자동 인스턴스 외에도 **LocalDB** 는 명명된 인스턴스를 지원합니다. SqlLocalDB.exe 프로그램을 사용하여 **LocalDB**의 명명된 인스턴스를 만들고, 시작 및 중지할 수 있습니다. SqlLocalDB.exe에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 위에서 마지막 줄은 다음과 비슷한 정보를 반환합니다.  
  
|||  
|-|-|  
|속성|"LocalDBApp1"|  
|버전 옵션|\<현재 버전>|  
|공유 이름|""|  
|소유자|"\<Windows 사용자>"|  
|자동 만들기|아니오|  
|State|실행|  
|마지막 시작 시간|\<날짜 및 시간>|  
|인스턴스 파이프 이름|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  응용 프로그램에 .NET 4.0.2 버전이 사용될 경우 **LocalDB**의 명명된 파이프에 직접 연결해야 합니다. 인스턴스 파이프 이름 값은 **LocalDB** 인스턴스가 수신 대기 중인 명명된 파이프입니다. LOCALDB# 다음의 인스턴스 파이프 이름 부분은 **LocalDB** 인스턴스가 시작될 때마다 변경됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 **LocalDB** 인스턴스에 연결하려면 **[!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결** 대화 상자의 **서버 이름** 상자에 인스턴스 파이프 이름을 입력합니다. 사용자 지정 프로그램에서 **LocalDB** LocalDB `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>LocalDB의 공유 인스턴스에 연결  
 **LocalDB**의 공유 인스턴스에 연결하려면 연결 문자열에 **.\\**(점과 백슬래시)를 추가하여 공유 인스턴스에 대해 예약된 네임스페이스를 참조합니다. 예를 들어 **라는** LocalDB `AppData` 의 공유 인스턴스에 연결하려면 연결 문자열의 일부로 `(localdb)\.\AppData` 와 같은 연결 문자열을 사용합니다. 자신이 소유하고 있지 않은 **LocalDB** 공유 인스턴스에 연결하는 사용자는 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인을 갖고 있어야 합니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 **LocalDB**문제 해결에 대한 자세한 내용은 [SQL Server 2012 Express LocalDB 문제 해결](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 기본 제공 계정(예: NT AUTHORITY\SYSTEM)에서 소유한 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** 인스턴스는 해당 용도로 사용자가 만든 인스턴스입니다. 컴퓨터의 모든 사용자는 **LocalDB**인스턴스를 사용하고 사용자 프로필에 파일을 저장하고 자격 증명으로 프로세스를 실행하여 데이터베이스를 만들 수 있습니다. 기본적으로 **LocalDB** 인스턴스에 대한 액세스는 해당 인스턴스의 소유자로 제한됩니다. **LocalDB** 에 포함된 데이터는 데이터베이스 파일에 대한 파일 시스템 액세스를 통해 보호됩니다. 공유 위치에 저장된 사용자 데이터베이스 파일은 해당 위치에 대한 파일 시스템 액세스 권한을 가진 사람이면 누구나 소유한 **LocalDB** 인스턴스를 사용하여 열 수 있습니다. 데이터베이스 파일이 사용자 데이터 폴더와 같은 보호되는 위치에 있으면 해당 사용자 및 해당 폴더에 대한 액세스 권한이 있는 관리자만 데이터베이스를 열 수 있습니다. **LocalDB** 파일은 한 번에 하나의 **LocalDB** 인스턴스에서만 열 수 있습니다.  
  
> [!NOTE]  
>  **LocalDB** 는 항상 사용자 보안 컨텍스트에서 실행됩니다. 즉, **LocalDB** 는 로컬 Administrator 그룹의 자격 증명으로는 실행되지 않습니다. 즉, **LocalDB** 인스턴스에서 사용하는 모든 데이터베이스 파일은 로컬 Administrators 그룹의 멤버 자격을 고려하지 않고 소유 사용자의 Windows 계정을 사용하여 액세스할 수 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  

[SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)
