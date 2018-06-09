---
title: SQL Server (MySQLToSql)에 SSMA 구성 요소 설치 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dc0a4555d41d4848fdbbe8a3b3244275dae1aaa2
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776329"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>SQL Server (MySQLToSql)에 SSMA 구성 요소 설치
SSMA를 설치 하는 것 외에도 설치 해야 구성 요소를 실행 하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이러한 구성 요소는 데이터 마이그레이션 및 서버 간 연결을 사용 하도록 설정 하려면 MySQL 공급자를 지 원하는 SSMA 확장 팩을 포함 합니다.  
  
## <a name="ssma-for-mysql-extension-pack"></a>MySQL 확장 팩 용 SSMA  
데이터베이스를 추가 하는 SSMA 확장 팩 **sysdb**의 지정 된 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이 데이터베이스 테이블 및 데이터를 마이그레이션하는 데 필요한 저장된 프로시저를 포함 합니다.  
  
또한 데이터를 마이그레이션할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업, 서버 쪽 데이터 마이그레이션 엔진으로 데이터를 마이그레이션하는 데 사용 되는 경우.  
  
### <a name="prerequisites"></a>사전 요구 사항  
에 MySQL 서버 구성 요소에 대 한 SSMA를 설치 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 또는 이후 버전입니다.  
  
-   MySQL 클라이언트 공급자 및 마이그레이션할 MySQL 데이터베이스에 연결 합니다. MySQL 제품 미디어 또는 MySQL 웹 사이트에서 공급자를 설치할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 브라우저 서비스를 설치 하는 동안 실행 해야 합니다. 인스턴스 목록을 채우는 데 사용 되는이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설치 마법사에서 합니다. 사용 하지 않도록 설정할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설치 후 브라우저 서비스입니다.  
  
    > [!NOTE]  
    > 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 브라우저 서비스가 실행 되 고 있지만 여전히 설치 프로그램에서 인스턴스 목록이 표시 되지 않으면, UDP 포트 1434의 차단을 해제 해야 합니다. Windows 방화벽을 사용 하 여 일시적으로 해당 포트를 차단 해제 하거나 Windows 방화벽을 임시로 해제할 수 있습니다. 또한 바이러스 백신 소프트웨어를 일시적으로 해제 해야 합니다. 설치 후 방화벽 및 바이러스 백신 소프트웨어를 사용 하도록 설정 했는지 확인 합니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치  
데이터를 마이그레이션하기 전에 든 지 확장 팩을 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면의 구성원 이어야는 **sysadmin** 서버 역할의 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
**확장 팩을 설치 하려면**  
  
1.  MySQL 확장 팩 SSMA를 복사 합니다. *n*합니다. Install.exe 여기서 *n* 실행 중인 컴퓨터에 있는 빌드 번호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
2.  MySQL 확장 팩 SSMA를 두 번 클릭 합니다. *n*합니다. Install.exe 합니다.  
  
3.  시작 대화 상자에서 클릭 **다음**합니다.  
  
4.  최종 사용자 사용권 계약 대화 상자에서 사용권 계약을 읽습니다. 동의 하면 선택 된 **사용권 계약에 동의** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
5.  설치 유형 선택 대화 상자에서 클릭 **일반**합니다.  
  
6.  설치 대화 상자, 준비 완료에서 클릭 **설치**합니다.  
  
7.  완료 된 첫 번째 설치 단계 대화 상자에서 클릭 **다음**합니다.  
  
    인스턴스를 선택 하면 새 대화 상자가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 확장 팩 설치에 대 한 합니다.  
  
8.  인스턴스를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] MySQL 스키마 마이그레이션 선택한 다음 클릭 위치 **다음**합니다.  
  
    기본 인스턴스는 컴퓨터와 동일한 이름이 있습니다. 명명 된 인스턴스 수 뒤에 백슬래시 및 인스턴스 이름입니다.  
  
9. 연결 대화 상자에서 인증 방법을 선택한 다음 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의에 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 입력 해야 인증을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인 이름 및 암호.  
  
10. 다음 대화 상자에서 선택 **설치 유틸리티 데이터베이스** *n*여기서 *n* 버전 번호 이며 클릭 **다음**합니다.  
  
    **sysdb** 테이블은 데이터베이스가 만들어지고 (서버 쪽 데이터 마이그레이션 엔진 사용) 하는 데이터 마이그레이션에 필요한 저장된 프로시저는 해당 데이터베이스에 만들어집니다.  
  
11. 다른 인스턴스에 유틸리티를 설치 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]선택, **예**, 클릭 하 고 **다음**합니다. 마법사를 종료 하려면 또는 **아니요**합니다.  
  
## <a name="see-also"></a>관련 항목  
[SSMA MySQL 클라이언트에 대 한 설치 &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server-SQL Azure DB로 데이터베이스 마이그레이션 MySQL &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
