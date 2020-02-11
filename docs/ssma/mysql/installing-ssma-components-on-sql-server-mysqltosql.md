---
title: SQL Server에 SSMA 구성 요소 설치 (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 64040f4a0caf8253e6d6e8a3b00ff21e0cebe6d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68075355"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>SQL Server에 SSMA 구성 요소 설치(MySQLToSql)
SSMA를 설치 하는 것 외에도를 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 구성 요소를 설치 해야 합니다. 이러한 구성 요소에는 데이터 마이그레이션을 지 원하는 SSMA 확장 팩과 서버 간 연결을 사용 하도록 설정 하는 MySQL 공급자가 포함 됩니다.  
  
## <a name="ssma-for-mysql-extension-pack"></a>MySQL 용 SSMA 확장 팩  
SSMA 확장 팩은 지정 된 인스턴스에 **sysdb**데이터베이스를 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 이 데이터베이스에는 데이터를 마이그레이션하는 데 필요한 테이블과 저장 프로시저가 포함 되어 있습니다.  
  
또한 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하는 경우 ssma는 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션에 서버 쪽 데이터 마이그레이션 엔진이 사용 될 때 에이전트 작업을 만듭니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MYSQL 용 ssma 서버 구성 요소를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전  
  
-   MySQL 클라이언트 공급자와 마이그레이션하려는 MySQL 데이터베이스에 연결 합니다. MySQL 제품 미디어 또는 MySQL 웹 사이트에서 공급자를 설치할 수 있습니다.  
  
-   설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 동안 Browser 서비스를 실행 해야 합니다. 이는 설치 마법사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 인스턴스 목록을 채우는 데 사용 됩니다. 설치 후 Browser 서비스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하지 않도록 설정할 수 있습니다.  
  
    > [!NOTE]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행 되 고 있지만 설치 프로그램에 인스턴스 목록이 표시 되지 않는 경우 UDP 포트 1434을 차단 해제 해야 합니다. Windows 방화벽을 사용 하 여 일시적으로 포트 차단을 해제 하거나 Windows 방화벽을 일시적으로 사용 하지 않도록 설정할 수 있습니다. 바이러스 백신 소프트웨어를 일시적으로 사용 하지 않도록 설정 해야 할 수도 있습니다. 설치 후 방화벽 및 바이러스 백신 소프트웨어를 사용 하도록 설정 해야 합니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치  
에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하기 전에 언제 든 지 확장 팩을 설치할 수 있습니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면 인스턴스에서 **sysadmin** 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**확장 팩을 설치 하려면**  
  
1.  MySQL 용 SSMA 확장 팩을 복사 합니다. *n*. 을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 .exe를 설치 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2.  MySQL 용 SSMA 확장 팩을 두 번 클릭 합니다. *n*. Setup.exe를 설치 합니다.  
  
3.  시작 대화 상자에서 **다음**을 클릭 합니다.  
  
4.  최종 사용자 사용권 계약 대화 상자에서 사용권 계약을 읽습니다. 동의 **하면 동의 함 확인란을** 선택 하 고 **다음**을 클릭 합니다.  
  
5.  설치 유형 선택 대화 상자에서 **일반**을 클릭 합니다.  
  
6.  설치 준비 완료 대화 상자에서 **설치**를 클릭 합니다.  
  
7.  설치의 첫 번째 단계 완료 대화 상자에서 **다음**을 클릭 합니다.  
  
    새 대화 상자가 표시 되 고 확장 팩을 설치할 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택 합니다.  
  
8.  MySQL 스키마를 마이그레이션하려 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 인스턴스를 선택 하 고 **다음**을 클릭 합니다.  
  
    기본 인스턴스의 이름은 컴퓨터와 동일 합니다. 명명 된 인스턴스에는 백슬래시와 인스턴스 이름이 나옵니다.  
  
9. 연결 대화 상자에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.  
  
    Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그온을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 인증을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 로그인 이름 및 암호를 입력 해야 합니다.  
  
10. 다음 대화 상자에서 **유틸리티 데이터베이스** *n*설치를 선택 합니다. 여기서 *n* 은 버전 번호이 고 **다음**을 클릭 합니다.  
  
    **Sysdb** 데이터베이스는 테이블을 사용 하 여 생성 되 고 데이터 마이그레이션에 필요한 저장 프로시저 (서버 쪽 데이터 마이그레이션 엔진 사용)는 해당 데이터베이스에 생성 됩니다.  
  
11. 다른 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유틸리티를 설치 하려면 **예**를 선택 하 고 **다음**을 클릭 합니다. 또는 마법사를 종료 하려면 **아니요**를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQLToSQL&#41;&#40;MySQL 용 SSMA 클라이언트 설치](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
