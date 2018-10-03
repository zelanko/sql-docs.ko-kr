---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: 676bc7adc3debb0beaee10d09d6fbe8018d42c2c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158953"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 실행 모드는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 프로그램 개발자를 대상으로 합니다. `LocalDB` 설치를 시작 하는 데 필요한 파일의 최소 집합을 복사 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]합니다. 한 번 `LocalDB` 가 설치 되어 개발자가 연결을 시작 특수 연결 문자열을 사용 하 여 합니다. 에 연결 하 고 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라는 자동으로 만들어지고 시작 복잡 하거나 시간이 오래 걸리는 구성 태스크 없이 데이터베이스를 사용 하도록 응용 프로그램을 사용 하도록 설정 합니다. 개발자 도구는 개발자가 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 전체 서버 인스턴스를 관리할 필요 없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 작성하고 테스트할 수 있게 해주는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 제공할 수 있습니다. 인스턴스의 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` 사용 하 여 관리 되는 `SqlLocalDB.exe` 유틸리티입니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` 대신 사용 해야는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 되지 않는 사용자 인스턴스 기능입니다.  
  
## <a name="installing-localdb"></a>LocalDB 설치  
 설치 하는 기본 방법은 `LocalDB` SqlLocalDB.msi 프로그램을 사용 하는 것입니다. `LocalDB` SKU를 설치할 때 옵션 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]합니다. 선택 `LocalDB` 에 **기능 선택** 설치 하는 동안 페이지 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]합니다. 하나만 설치할 수는 `LocalDB` 각 주에 대 한 이진 파일 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 버전입니다. 여러 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스를 시작할 수 있으며, 이러한 프로세스에는 모두 동일한 이진 파일이 사용됩니다. 인스턴스를 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로 시작 된 `LocalDB` 동일한 제약이 있습니다 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Description  
 `LocalDB` 설치 프로그램 SqlLocalDB.msi 프로그램을 사용 하 여 컴퓨터에 필요한 파일을 설치 합니다. 설치가 끝나면 `LocalDB` 의 인스턴스이고 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 만들고 열 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 데이터베이스의 시스템 데이터베이스 파일은 사용자의 로컬 AppData 경로에 저장되는데, 이 경로는 일반적으로 숨겨져 있습니다. 예를 들어 **C:\Users\\<사용자\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**입니다. 사용자 데이터베이스 파일은 사용자가 지정하는 위치(일반적으로 **C:\Users\\<사용자\>\Documents\\** 폴더 내 임의 위치)에 저장됩니다.  
  
 포함 하는 방법에 대 한 자세한 내용은 `LocalDB` 응용 프로그램에서 참조 합니다 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서 [로컬 데이터 개요](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx)를 [연습: SQL Server LocalDB 데이터베이스를 만드는](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx), 및 [연습: 데이터 (Windows Forms) SQL Server LocalDB 데이터베이스에 연결할](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx)합니다.  
  
 에 대 한 자세한 내용은 합니다 `LocalDB` API 참조 [SQL Server Express LocalDB 인스턴스 API 참조](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) 및 [LocalDBStartInstance 함수](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx)합니다.  
  
 SqlLocalDb 유틸리티의 새 인스턴스를 만들 수 있습니다 `LocalDB`start 및 stop 인스턴스의 `LocalDB`를 관리할 수 있도록 하는 옵션을 포함 하 고 `LocalDB`입니다.  SqlLocalDb 유틸리티에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
 인스턴스 데이터 정렬은 `LocalDB` 정렬은 SQL_Latin1_General_CP1_CI_AS로 설정 되 고 변경할 수 없습니다. 데이터베이스 수준, 열 수준 및 식 수준 데이터 정렬은 일반적으로 지원됩니다. 포함된 데이터베이스는 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)에 정의된 메타데이터 및 tempdb 데이터 정렬 규칙을 따릅니다.  
  
### <a name="restrictions"></a>Restrictions  
 `LocalDB` 병합 복제 구독자 일 수 없습니다.  
  
 `LocalDB` FILESTREAM을 지원 하지 않습니다.  
  
 `LocalDB` Service Broker에 대 한 로컬 큐만 허용 합니다.  
  
 인스턴스의 `LocalDB` NT AUTHORITY\SYSTEM; windows 파일 시스템 리디렉션으로 인해 관리 효율성 문제가 있습니다와 같은 기본 제공 계정에서 소유 대신 일반 windows 계정을 소유자로 사용 합니다.  
  
### <a name="automatic-and-named-instances"></a>자동 및 명명된 인스턴스  
 `LocalDB` 두 가지 인스턴스를 지원 합니다: Automatic instance 및 named instance.  
  
-   자동 인스턴스의 `LocalDB` 공개 됩니다. 이 인스턴스는 자동으로 생성 및 관리되고 모든 응용 프로그램에서 사용될 수 있습니다. 자동 인스턴스 `LocalDB` 의 모든 버전에 대 한 `LocalDB` 사용자의 컴퓨터에 설치 합니다. 자동 인스턴스의 `LocalDB` 효율적으로 관리를 제공 합니다. 인스턴스를 만들 필요 없이 그대로 작동합니다. 따라서 응용 프로그램을 쉽게 설치할 수 있으며 다른 컴퓨터에 쉽게 마이그레이션할 수 있습니다. 대상 컴퓨터에 지정된 된 버전의 경우 `LocalDB` 설치의 자동 인스턴스 `LocalDB` 를 해당 버전도 대상 컴퓨터에서 사용할 수 있습니다. 자동 인스턴스의 `LocalDB` 특수 한 예약된 된 네임 스페이스에 속하는 인스턴스 이름 패턴입니다. 명명 된 인스턴스를 사용 하 여 이름 충돌을 방지이 `LocalDB`합니다. 자동 인스턴스의 이름은 **MSSQLLocalDB**입니다.  
  
-   명명 된 인스턴스 `LocalDB` 전용입니다. 이 인스턴스는 인스턴스 만들기와 관리를 담당하는 단일 응용 프로그램에 의해 소유됩니다. 명명된 인스턴스는 다른 인스턴스로부터의 격리를 제공하고 다른 데이터베이스 사용자와의 리소스 경합을 줄여서 성능을 향상시킬 수 있습니다. 명명 된 인스턴스를 통해 사용자가 명시적으로 만들 수 있어야 합니다 `LocalDB` 관리 API 또는 app.config를 통해 암시적으로 (관리 되는 응용 프로그램에서 API를 사용 하더라도) 하지만 관리 응용 프로그램에 대 한 파일입니다. 각 명명 된 인스턴스의 `LocalDB` 에 연결 된 `LocalDB` 버전의 각 집합을 가리키는 `LocalDB` 이진 파일. 인스턴스 이름에 `LocalDB` 는 `sysname` 데이터 입력 하 고 최대 128 자를 포함할 수 있습니다. 이러한 특성은 이름을 16 ASCII 문자의 일반 NetBIOS 이름으로 제한하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일반적인 명명된 인스턴스와 다릅니다. 인스턴스의 이름을 `LocalDB` 파일 이름에 사용할 수 있는 모든 유니코드 문자를 포함할 수 있습니다.  자동 인스턴스 이름을 사용하는 명명된 인스턴스는 자동 인스턴스가 됩니다.  
  
 컴퓨터의 다른 사용자는 동일한 이름의 인스턴스를 가질 수 있습니다. 각 인스턴스는 다른 사용자로 실행되는 서로 다른 프로세스입니다.  
  
## <a name="shared-instances-of-localdb"></a>LocalDB의 공유 인스턴스  
 컴퓨터의 여러 사용자의 단일 인스턴스에 연결 해야 하는 시나리오를 지원 하도록 `LocalDB`, `LocalDB` 인스턴스 공유를 지원 합니다. 인스턴스 소유자는 컴퓨터의 다른 사용자가 자신의 인스턴스에 연결하도록 허용할 수 있습니다. 자동 및 명명 된 인스턴스의 `LocalDB` 공유할 수 있습니다. 인스턴스를 공유 하려면 `LocalDB` 사용자에 대 한 공유 이름 (별칭)을 선택 합니다. 공유 이름은 컴퓨터의 모든 사용자에게 표시되기 때문에 이 공유 이름은 해당 컴퓨터에서 고유해야 합니다. 인스턴스의 공유 이름은 `LocalDB` 의 명명 된 인스턴스와 형식이 동일 `LocalDB`합니다.  
  
 컴퓨터의 관리자의 공유 인스턴스를 만들 수만 `LocalDB`합니다. 공유 인스턴스 `LocalDB` 의 공유 인스턴스 소유자 또는 관리자에 공유할 수 있습니다. `LocalDB`합니다. 공유 인스턴스의 공유 권한 없이 `LocalDB`를 사용 하 여는 `LocalDBShareInstance` 및 `LocalDBUnShareInstance` 의 메서드는 `LocalDB` API 또는 공유 및 공유 해제 옵션 SqlLocalDb 유틸리티의 합니다.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>LocalDB 시작 및 LocalDB에 연결  
  
### <a name="connecting-to-the-automatic-instance"></a>자동 인스턴스에 연결  
 사용 하는 가장 쉬운 방법은 `LocalDB` 연결 문자열을 사용 하 여 현재 사용자가 소유한 자동 인스턴스에 연결 하는 것 **"Server = (localdb) \MSSQLLocalDB;Integrated 보안 = true"** 합니다. 파일 이름을 사용하여 특정 데이터베이스에 연결하려면 **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** 와 유사한 연결 문자열을 사용하여 연결합니다.  
  
> [!NOTE]  
>  사용자 컴퓨터에 연결 하려고 처음 `LocalDB`, 자동 인스턴스 둘 다를 만든 다음 시작 합니다. 인스턴스를 만드는 추가 시간으로 인해 시간 초과 메시지와 함께 연결 시도가 실패할 수 있습니다. 이 경우 만들기 프로세스가 완료되도록 몇 초 정도 기다린 후에 다시 연결하세요.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>명명된 인스턴스 만들기 및 연결  
 자동 인스턴스 외에도 `LocalDB` 명명 된 인스턴스도 지원 합니다. SqlLocalDB.exe 프로그램 만들기, 시작 및 중지의 명명 된 인스턴스를 사용 하 여 `LocalDB`입니다. SqlLocalDB.exe에 대한 자세한 내용은 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)를 참조하세요.  
  
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
|이름|"LocalDBApp1"|  
|버전|\<현재 버전>|  
|공유 이름|""|  
|소유자|"\<Windows 사용자>"|  
|자동 만들기|아니요|  
|State|실행|  
|마지막 시작 시간|\<날짜 및 시간>|  
|인스턴스 파이프 이름|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  명명된 된 파이프에 직접 연결 해야 응용 프로그램에.NET 4.0.2 버전이 사용 하는 경우는 `LocalDB`합니다. 인스턴스 파이프 이름 값은 명명 된 파이프 인스턴스의 `LocalDB` 에서 수신 대기 합니다. LOCALDB #를 변경한 후 각 인스턴스 파이프 이름 부분은 인스턴스의 시간 `LocalDB` 시작 됩니다. 인스턴스에 연결 하려면 `LocalDB` 를 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 인스턴스 파이프 이름을 입력 합니다 **서버 이름** 상자를 **연결할 [!INCLUDE[ssDE](../../includes/ssde-md.md)]**  대화 상자. 사용자 지정 프로그램에서의 인스턴스에 연결을 설정할 수 있습니다 `LocalDB` 유사한 연결 문자열을 사용 하 여 `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>LocalDB의 공유 인스턴스에 연결  
 공유 인스턴스에 연결 하려면 `LocalDB` 추가할 **.\\**  (점과 백슬래시)를 공유 인스턴스에 대해 예약 된 네임 스페이스를 참조 하도록 연결 문자열입니다. 예를 들어의 공유 인스턴스에 연결 하려면 `LocalDB` 라는 `AppData` 와 같은 연결 문자열을 사용 하 여 `(localdb)\.\AppData` 연결 문자열의 일부로. 사용자의 공유 인스턴스에 연결 `LocalDB` Windows 인증을 소유 하지 않는 있어야 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 합니다.  
  
## <a name="troubleshooting"></a>문제 해결  
 문제 해결에 대 한 자세한 `LocalDB`를 참조 하세요 [SQL Server 2012 Express LocalDB 문제 해결](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)합니다.  
  
## <a name="permissions"></a>사용 권한  
 인스턴스의 [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` 해당 용도로 사용자가 만든 인스턴스입니다. 컴퓨터의 모든 사용자의 인스턴스를 사용 하 여 데이터베이스를 만들 수 `LocalDB`, 사용자 프로필 아래에 있는 파일을 저장 하 고 자격 증명으로 프로세스를 실행 합니다. 기본적으로 인스턴스에 액세스할 `LocalDB` 해당 소유자로 제한 됩니다. 포함 된 데이터는 `LocalDB` 데이터베이스 파일에 대 한 파일 시스템 액세스에 의해 보호 됩니다. 인스턴스를 사용 하 여 해당 위치에 대 한 파일 시스템 액세스를 사용 하 여 모든 사용자 데이터베이스를 열 수 사용자 데이터베이스 파일 공유 위치에 저장 되 면 `LocalDB` 소유한 합니다. 데이터베이스 파일이 사용자 데이터 폴더와 같은 보호되는 위치에 있으면 해당 사용자 및 해당 폴더에 대한 액세스 권한이 있는 관리자만 데이터베이스를 열 수 있습니다. 합니다 `LocalDB` 파일의 인스턴스 하나 에서만 열 수 `LocalDB` 번입니다.  
  
> [!NOTE]  
>  `LocalDB` 항상 사용자 보안 컨텍스트에서 실행 즉, `LocalDB` 로컬 관리자 그룹에서 자격 증명으로 실행 되지 않습니다. 즉, 모든 데이터베이스에서 사용 하는 파일을 `LocalDB` 인스턴스는 로컬 관리자 그룹의 멤버 자격을 고려 하지 않고 소유 사용자의 Windows 계정을 사용 하 여 액세스할 수 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SqlLocalDB 유틸리티](../../tools/sqllocaldb-utility.md)  
  
  
