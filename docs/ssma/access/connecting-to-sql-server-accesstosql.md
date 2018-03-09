---
title: "SQL Server (AccessToSQL)에 연결 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7f2c52a7af7fc3f9a35585678b222d6a29e5787
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-sql-server-accesstosql"></a>SQL Server (AccessToSQL)에 연결
Access 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 대상 인스턴스에 연결 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. SSMA 인스턴스의 데이터베이스에 대 한 메타 데이터를 가져오며 연결 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 데이터베이스 메타 데이터를 표시 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다. SSMA는의 인스턴스에 대 한 정보를 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결 하지만 암호를 저장 하지 않는 있습니다.  
  
SQL Server에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 SQL Server로 활성 서버에 연결 하려는 경우. SQL Server에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Server의 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, SQL Server 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 SQL Server 메타 데이터 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Server 메타 데이터 동기화 중" 섹션을 참조 하십시오.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 사용 권한  
에 연결 하는 데 사용 되는 계정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 해당 계정에서 수행 하는 동작에 따라 다른 사용 권한이 필요 합니다.  
  
-   Access 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문에서 메타 데이터를 새로 고치려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 변환 된 구문에 스크립트를 저장 하려면 계정이의 인스턴스에 로그인 할 수 있는 권한이 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   에 데이터베이스 개체를 로드 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 최소 권한 요구 사항은의 멤버 자격이 **db_owner** 대상 데이터베이스의 데이터베이스 역할입니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
Access 데이터베이스 개체를 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문의 인스턴스에 대 한 연결을 설정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Access 데이터베이스 마이그레이션하려 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. 에 연결한 후에 Access 데이터베이스 수준에서이 매핑을 사용자 지정할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [매핑 소스와 대상 데이터베이스](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> 에 연결 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 있는지 확인 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 실행 중이 고 연결을 허용할 수 있습니다. 자세한 내용은 참조 "에 연결 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 엔진"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Server에 연결**합니다.  
  
    이전에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 명령 이름은 **SQL Server에 다시 연결**합니다.  
  
2.  에 **서버 이름** 상자를 입력 하거나 선택의 인스턴스 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있는 **localhost** 또는 점 (**.**).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 입력 합니다. 예를 들어: MyServer\MyInstance 합니다.  
  
    -   활성 사용자 인스턴스에 연결 하려면 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], 명명 된 파이프를 사용 하 여 연결 같이 파이프 이름을 지정 하 고 프로토콜 \\ \\.\pipe\sql\query 합니다. 자세한 내용은 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 설명서를 참조하세요.  
  
3.  경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 사용 되는 포트 번호를 입력, 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 연결 모드는 **서버 포트** 상자입니다. 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 기본 포트 번호는 1433입니다. 명명 된 인스턴스에 대 한 SSMA는에서 포트 번호 가져오기를 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 서비스입니다.  
  
4.  에 **데이터베이스** 상자 개체 및 데이터 마이그레이션 위한 대상 데이터베이스의 이름을 입력 합니다.  
  
    다시 연결할 때이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
    대상 데이터베이스 이름입니다. 공백이 나 특수 문자를 포함할 수 없습니다. 예를 들어 Access 데이터베이스를 마이그레이션할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "abc" 라는 데이터베이스입니다. Access 데이터베이스를 마이그레이션할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "는 b-c" 라는 데이터베이스입니다.  
  
    연결한 후 데이터베이스 마다이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [매핑 소스와 대상 데이터베이스](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
5.  에 **인증** 드롭 다운 메뉴에서 선택 된 연결에 사용할 인증 유형을 합니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인을 **SQL Server 인증**, 사용자 이름 및 암호를 제공 합니다.  
  
6.  보안 연결에 대 한 두 개의 추가 되 면 **연결 암호화** 확인란을 선택 하 고 **TrustServerCertificate** 확인란을 선택 합니다. 경우에만 **연결 암호화** 확인란이 선택 되어 **TrustServerCertificate** 이 확인란은 표시 합니다. 때 **연결 암호화** checked(true)은 및 **TrustServerCertificate** unchecked(false)는, SQL Server SSL 인증서의 유효성을 검사 합니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이 위해 서버 쪽 뿐만 아니라 클라이언트측에서 인증서를 설치 합니다.  
  
7.  **연결**을 클릭합니다.  
  
**더 높은 버전 호환성**  
  
더 높은 버전의 SQL Server에 연결/다시 연결할 허용 됩니다.  
  
1.  생성 되는 프로젝트는 SQL Server 2005 때 SQL Server 2008 또는 SQL Server 2012에 연결할 수 있습니다.  
  
2.  생성 되는 프로젝트에는 SQL Server 2008이 있지만 더 낮은 버전 즉, SQL Server 2005에 연결 하는 허용 되지 않습니다 때 SQL Server 2012에 연결할 수 됩니다.  
  
3.  생성 되는 프로젝트는 SQL Server 2012 때만 SQL Server 2012에 연결할 수 있습니다.  
  
4.  더 높은 버전 호환성 SQL Azure에 대해 올바르지 않습니다.  
  
||||||||
|-|-|-|-|-|-|-|
|**프로젝트 형식 및 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 (버전: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008 (버전: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|예|예|예|예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||예|예|예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||예|예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||예||
|SQL Azure||||||예|
  
> [!IMPORTANT]  
> 데이터베이스 개체의 변환에 연결 된 SQL Server의 버전에 따라 되지 않습니다 되지만 프로젝트 형식에 따라 수행 됩니다. SQL Server 2005 프로젝트의 경우 변환 상위 버전의 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)에 연결 되어 있는 경우에 SQL Server 2005를 기준으로 수행 됩니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터를 동기화합니다.  
경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마 변경에 연결한 후, 메타 데이터를 서버와 동기화 할 수 있습니다.  
  
**SQL Server 메타 데이터를 동기화 하려면**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기, 마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **데이터베이스와 동기화**합니다.  
  
## <a name="reconnecting-to-sql-server"></a>SQL Server에 다시 연결  
에 대 한 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 합니다. 에 다시 연결 해야 프로젝트를 다시 열 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 활성 서버에 연결 하려는 경우. 데이터베이스 개체에 로드 될 때까지 오프 라인으로 작업할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터를 마이그레이션합니다.  
  
에 다시 연결 하는 절차가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결을 설정 하는 절차와 같습니다.  
  
## <a name="next-steps"></a>Next Steps  
원본 및 대상 데이터베이스 간의 매핑을 사용자 지정 하는 경우 참조 [매핑 소스와 대상 데이터베이스](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4) 데이터베이스 개체를 변환 하려면 다음 단계는 그렇지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문을 사용 하 여 [데이터베이스 개체를 변환 합니다.](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
