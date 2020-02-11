---
title: SQL Server에 SSMA 구성 요소 설치 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 1f0cea859e9465eebefebc061ee51107dc7844aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71713307"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>SQL Server에 SSMA 구성 요소 설치 (OracleToSQL)

SSMA를 설치 하는 것 외에도를 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 구성 요소를 설치 해야 합니다. 이러한 구성 요소에는 데이터 마이그레이션을 지 원하는 SSMA 확장 팩과 서버 간 연결을 사용 하도록 설정 하는 Oracle 공급자가 포함 됩니다.  
  
## <a name="ssma-for-oracle-extension-pack"></a>Oracle 용 SSMA 확장 팩

SSMA 확장 팩은 **sysdb** 및 **ssmatesterdb** 데이터베이스를 지정 된 인스턴스에 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 데이터베이스 **sysdb** 에는 데이터를 마이그레이션하는 데 필요한 테이블 및 저장 프로시저와 Oracle 시스템 함수를 에뮬레이트하는 사용자 정의 함수가 포함 되어 있습니다. **Ssmatesterdb** 데이터베이스는 테스터 구성 요소에 필요한 테이블과 프로시저를 포함 합니다.  
  
또한 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하는 경우 ssma는 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션에 서버 쪽 데이터 마이그레이션 엔진이 사용 될 때 에이전트 작업을 만듭니다.  
  
### <a name="prerequisites"></a>사전 요구 사항

Oracle 용 SSMA 서버 구성 요소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치 하기 전에 시스템이 다음과 같은 요구 사항을 충족 하는지 확인 합니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스가 설치 되었습니다. SSMA는 SQL Server 2008 Express Edition을 지원 하지 않습니다.
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전  
  
- Oracle 클라이언트 공급자나 oracle 용 OLE DB 공급자 및 마이그레이션할 Oracle 데이터베이스에 대 한 연결을 제공 합니다. Oracle 제품 미디어 또는 Oracle 웹 사이트에서 공급자를 설치할 수 있습니다.  
  
- 설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 동안 Browser 서비스를 실행 해야 합니다. 이는 설치 마법사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 인스턴스 목록을 채우는 데 사용 됩니다. 설치 후 Browser 서비스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하지 않도록 설정할 수 있습니다.  
  
    > [!NOTE]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행 되 고 있지만 설치 프로그램에 인스턴스 목록이 표시 되지 않는 경우 UDP 포트 1434을 차단 해제 해야 합니다. Windows 방화벽을 사용 하 여 일시적으로 포트 차단을 해제 하거나 Windows 방화벽을 일시적으로 사용 하지 않도록 설정할 수 있습니다. 바이러스 백신 소프트웨어를 일시적으로 사용 하지 않도록 설정 해야 할 수도 있습니다. 설치 후 방화벽 및 바이러스 백신 소프트웨어를 사용 하도록 설정 해야 합니다.  
  
### <a name="installing-the-extension-pack"></a>확장 팩 설치

에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하기 전에 언제 든 지 확장 팩을 설치할 수 있습니다.  
  
> [!IMPORTANT]  
> 확장 팩을 설치 하려면 인스턴스에서 **sysadmin** 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**확장 팩을 설치 하려면**
  
1. 아직 없는 경우 SSMA Zip 파일에서 모든 파일을 추출 합니다.  
  
    포함 된 WinZip 버전에 따라 파일을 두 번 클릭 하거나 파일을 마우스 오른쪽 단추로 클릭 한 다음 **모두 압축 풀기** 또는 **WinZip에서 열기**를 선택할 수 있습니다. WinZip 사용자 인터페이스의 지침에 따라 파일을 추출 합니다.  
  
2. **Oracle 용 Ssma 확장 팩을 복사 합니다.* n*. **을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터에 .exe (여기서 *n* 은 빌드 번호)를 설치 합니다.  
  
3. **Oracle 용 Ssma 확장 팩을 두 번 클릭 합니다.* n*. Setup.exe를 설치**합니다.  
  
4. 
  **Welcome** 페이지에서 **다음**을 선택합니다.  
  
5. **최종 사용자 사용권 계약** 페이지에서 사용권 계약을 읽습니다. 동의 **하면 동의 함 확인란을** 선택 하 고 **다음**을 선택 합니다.  
  
6. **설치 유형 선택** 페이지에서 **일반**을 선택 합니다.  
  
7. **설치 준비 완료** 페이지에서 **설치**를 선택 합니다.  
  
8. **설치의 첫 번째 단계 완료** 페이지에서 **다음**을 선택 합니다.  
  
    새 대화 상자가 표시 되 고 확장 팩을 설치할 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택 합니다.  
  
9. Oracle 스키마를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택 하 고 **다음**을 선택 합니다.  
  
    기본 인스턴스의 이름은 컴퓨터와 동일 합니다. 명명 된 인스턴스에는 백슬래시와 인스턴스 이름이 나옵니다.  
  
10. 연결 페이지에서 인증 방법을 선택 하 고 **다음**을 선택 합니다.  
  
    Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그인을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 인증을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 로그인 이름 및 암호를 입력 해야 합니다.  
  
11. 다음 페이지에서 **유틸리티 데이터베이스** *n*설치를 선택 합니다. 여기서 *n* 은 버전 번호 이며 **다음**을 선택 합니다.  
  
    **Sysdb** 데이터베이스가 만들어지고 사용자 정의 함수 및 저장 프로시저가 해당 데이터베이스에 만들어집니다.  
  
    **테스터 데이터베이스 설치** 옵션을 선택 하면 테스터 **ssmatesterdb** 데이터베이스가 생성 됩니다.  
  
12. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 유틸리티를 설치 하려면 **예**를 선택 하 고 **다음**을 선택 하거나 마법사를 종료 하려면 **아니요**를 선택 합니다.  
  
13. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 sqlcmd 유틸리티를 사용 하 여 다음 스크립트를 실행 하 여 CLR을 사용 하도록 설정 합니다.  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    CLR을 사용 하지 않는 경우 SSMA를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결할 때 다음과 같은 오류가 표시 됩니다.  
  
    SSMA가 확장 팩 어셈블리 버전 정보를 검색할 수 없습니다. 데이터베이스 서버에 확장 팩을 다시 설치 합니다.  
  
### <a name="sql-server-database-objects"></a>데이터베이스 개체 SQL Server  

확장 팩을 설치한 후에는 **ssma_oracle bcp_migration_packages** 테이블이 **sysdb** 데이터베이스에 표시 됩니다.

데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션할 때마다 ssma는 에이전트 작업을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만듭니다. 이러한 작업에는 **데이터 마이그레이션 패키지 {GUID} ssma_oracle**이름이 지정 되 고 작업 폴더 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 에이전트 노드에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목

[Oracle 용 SSMA 클라이언트 &#40;설치 OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
