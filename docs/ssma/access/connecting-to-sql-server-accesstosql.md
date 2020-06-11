---
title: SQL Server에 연결 (AccessToSQL) | Microsoft Docs
description: SQL Database의 대상 인스턴스에 연결 하 여 Access 데이터베이스를 마이그레이션하는 방법에 대해 알아봅니다. SSMA는 SQL Database의 데이터베이스에 대 한 메타 데이터를 가져옵니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6266eb0596b351a7ef54baed6a7a76a7a655ac60
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293100"
---
# <a name="connecting-to-sql-server-accesstosql"></a>SQL Server에 연결 (AccessToSQL)
Access 데이터베이스를로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 대상 인스턴스에 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 연결할 때 SSMA는 인스턴스의 데이터베이스에 대 한 메타 데이터를 가져오고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기에 데이터베이스 메타 데이터를 표시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. SSMA는 연결 된 인스턴스에 대 한 정보 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 저장 하지만 암호를 저장 하지는 않습니다.  
  
SQL Server에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 서버에 대 한 활성 연결을 원하는 경우 SQL Server에 다시 연결 해야 합니다. 데이터베이스 개체를 SQL Server로 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
SQL Server 인스턴스에 대 한 메타 데이터는 자동으로 동기화 되지 않습니다. 대신 메타 데이터 탐색기 SQL Server에서 메타 데이터를 업데이트 하려면 SQL Server 메타 데이터를 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Server 메타 데이터 동기화" 섹션을 참조 하십시오.  
  
## <a name="required-sql-server-permissions"></a>필요한 SQL Server 권한  
에 연결 하는 데 사용 되는 계정에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 해당 계정에서 수행 하는 작업에 따라 다른 사용 권한이 필요 합니다.  
  
-   Access 개체를 구문으로 변환 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하거나에서 메타 데이터를 새로 고치거 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 나 변환 된 구문을 스크립트에 저장 하려면 계정에 인스턴스에 로그인 할 수 있는 권한이 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   에 데이터베이스 개체를 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고로 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최소 권한 요구 사항은 대상 데이터베이스에서 **db_owner** 데이터베이스 역할의 멤버 자격입니다.  
  
## <a name="establishing-a-sql-server-connection"></a>SQL Server 연결 설정  
Access 데이터베이스 개체를 구문으로 변환 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] access 데이터베이스를 마이그레이션하려는 인스턴스에 대 한 연결을 설정 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
연결 속성을 정의 하는 경우 개체 및 데이터가 마이그레이션되는 데이터베이스도 지정 합니다. 에 연결한 후 액세스 데이터베이스 수준에서이 매핑을 사용자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [원본 및 대상 데이터베이스 매핑](mapping-source-and-target-databases-accesstosql.md)을 참조 하세요.  
  
> [!IMPORTANT]  
> 에 연결 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 중이 고 연결을 허용할 수 있는지 확인 합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "데이터베이스 엔진에 연결"을 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**SQL Server에 연결하려면**  
  
1.  **파일** 메뉴에서 **SQL Server에 연결**을 선택 합니다.  
  
    이전에에 연결한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령 이름이 **SQL Server에 다시 연결**됩니다.  
  
2.  **서버 이름** 상자에 인스턴스의 이름을 입력 하거나 선택 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 **localhost** 또는 점 (**.**)을 입력할 수 있습니다.  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우 컴퓨터 이름을 입력 합니다.  
  
    -   명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 입력 합니다. 예: MyServer\MyInstance.  
  
    -   의 활성 사용자 인스턴스에 연결 하려면 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 명명 된 파이프 프로토콜을 사용 하 여 연결 하 고 파이프 이름 (예: .\pipe\sql\query)을 지정 합니다. \\ \\ 자세한 내용은 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 설명서를 참조하세요.  
  
3.  인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **서버 포트** 상자에서 연결에 사용 되는 포트 번호를 입력 합니다. 기본 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA는 Browser 서비스에서 포트 번호를 가져오려고 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
4.  **데이터베이스** 상자에 개체 및 데이터 마이그레이션에 대 한 대상 데이터베이스의 이름을 입력 합니다.  
  
    에 다시 연결 하는 경우에는이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    대상 데이터베이스 이름에는 공백이 나 특수 문자를 사용할 수 없습니다. 예를 들어 Access 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "abc" 라는 데이터베이스로 마이그레이션할 수 있습니다. 하지만 Access 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "a b-c" 라는 데이터베이스로 마이그레이션할 수는 없습니다.  
  
    연결한 후 데이터베이스당이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [원본 및 대상 데이터베이스 매핑](mapping-source-and-target-databases-accesstosql.md) 을 참조 하세요.  
  
5.  **인증** 드롭다운 메뉴에서 연결에 사용할 인증 유형을 선택 합니다. 현재 Windows 계정을 사용 하려면 **Windows 인증**을 선택 합니다. 로그인을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server 인증**을 선택 하 고 사용자 이름 및 암호를 제공 합니다.  
  
6.  보안 연결의 경우, **연결 암호화** 확인란 및 **trustservercertificate** 확인란의 두 컨트롤이 추가 됩니다. **연결 암호화** 확인란을 선택 하는 경우에만 **trustservercertificate** 확인란이 표시 됩니다. **연결 암호화** 를 선택 하 고 (True) **trustservercertificate** 가 선택 취소 (false) 되 면에서 SQL Server SSL 인증서의 유효성을 검사 합니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 이를 위해 클라이언트 쪽 뿐만 아니라 서버 쪽에도 인증서를 설치 해야 합니다.  
  
7.  **연결**을 클릭합니다.  
  
**높은 버전 호환성**  
  
더 높은 버전의 SQL Server에 연결 하거나 다시 연결할 수 있습니다.  
  
1.  만든 프로젝트가 SQL Server 2005 인 경우 SQL Server 2008 또는 SQL Server 2012에 연결할 수 있습니다.  
  
2.  만든 프로젝트가 2008 SQL Server 될 때 SQL Server 2012에 연결할 수 있지만, 더 낮은 버전 (SQL Server 2005)에 연결할 수 없습니다.  
  
3.  만든 프로젝트가 SQL Server 2012 인 경우에는 SQL Server 2012에만 연결할 수 있습니다.  
  
4.  SQL Azure에 대 한 버전 호환성이 더 이상 유효 하지 않습니다.  
  
||||||||
|-|-|-|-|-|-|-|
|**프로젝트 형식 Vs 대상 서버 버전**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 (버전: 4.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 (버전: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 (버전: 11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 (버전: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 (버전: 13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|예|예|예|예|예||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||예|예|예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||예|예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||예|예||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||예||
|SQL Azure||||||예|
  
> [!IMPORTANT]  
> 데이터베이스 개체의 변환은 프로젝트 형식에 따라 수행 되지만에 연결 된 SQL Server 버전에 따라 수행 되지 않습니다. SQL Server 2005 프로젝트의 경우 더 높은 버전의 SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016)에 연결 된 경우에도 SQL Server 2005 마다 변환이 수행 됩니다.  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 메타 데이터 동기화  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결한 후에 스키마가 변경 되 면 메타 데이터를 서버와 동기화 할 수 있습니다.  
  
**SQL Server 메타 데이터를 동기화 하려면**  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메타 데이터 탐색기에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스와 동기화**를 선택 합니다.  
  
## <a name="reconnecting-to-sql-server"></a>SQL Server에 다시 연결  
사용자의 연결은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 대 한 활성 연결을 원하는 경우에 다시 연결 해야 합니다. 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
에 다시 연결 하는 절차는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 설정 하는 절차와 같습니다.  
  
## <a name="next-steps"></a>다음 단계  
원본 데이터베이스와 대상 데이터베이스 간의 매핑을 사용자 지정 하려면 [원본 및](mapping-source-and-target-databases-accesstosql.md) 대상 데이터베이스 매핑을 참조 하세요. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체 [convert](converting-access-database-objects-accesstosql.md) 를 사용 하 여 데이터베이스 개체를 구문으로 변환 합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
