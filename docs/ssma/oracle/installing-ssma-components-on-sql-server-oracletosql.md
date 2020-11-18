---
title: SQL Server에 SSMA 구성 요소 설치 (OracleToSQL) | Microsoft Docs
description: Oracle 데이터베이스 변환을 지원 하기 위해 SQL Server를 실행 하는 컴퓨터에 SSMA 확장 팩 및 Oracle 공급자를 설치 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the extension pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 64850d1a701491f0dc5817576a568fdc3ebc2483
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870107"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>SQL Server에 SSMA 구성 요소 설치 (OracleToSQL)

SSMA를 설치 하는 것 외에도를 실행 하는 컴퓨터에 구성 요소를 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이러한 구성 요소에는 데이터 마이그레이션을 지 원하는 SSMA 확장 팩과 서버 간 연결을 사용 하도록 설정 하는 Oracle 공급자가 포함 됩니다.

## <a name="ssma-for-oracle-extension-pack"></a>Oracle 용 SSMA 확장 팩

SSMA 확장 팩은 확장 저장 프로시저를 배포 하 고 지정 된 인스턴스에 **sysdb** 및 **ssmatesterdb** 데이터베이스를 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 확장 저장 프로시저는 Oracle의 기능 및 behaiov을 에뮬레이트하는 데 필요한 기능을 제공 하는 반면 **sysdb** 데이터베이스에는 데이터를 마이그레이션하는 데 필요한 테이블과 저장 프로시저가 포함 되어 있습니다. **Ssmatesterdb** 데이터베이스에는 테스터 구성 요소에 필요한 테이블 및 프로시저 (설치 된 경우)가 포함 되어 있습니다.

또한 데이터를로 마이그레이션하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이그레이션에 서버 쪽 데이터 마이그레이션 엔진이 사용 될 때 에이전트 작업을 만듭니다.

### <a name="prerequisites"></a>사전 요구 사항

Oracle 용 SSMA 서버 구성 요소를 설치 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템이 다음과 같은 요구 사항을 충족 하는지 확인 합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 설치 되었습니다.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- Oracle에 대 한 OLE DB 공급자 (OLE DB를 사용 하는 경우) 및 마이그레이션할 Oracle 데이터베이스에 대 한 연결입니다. Oracle 제품 미디어 또는 Oracle 웹 사이트에서 공급자를 설치할 수 있습니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 하는 동안 Browser 서비스를 실행 해야 합니다. 이는 설치 마법사에서 인스턴스 목록을 채우는 데 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 설치 후 Browser 서비스를 사용 하지 않도록 설정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

  > [!NOTE]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 서비스가 실행 되 고 있지만 설치 프로그램에 인스턴스 목록이 표시 되지 않는 경우 UDP 포트 1434을 차단 해제 해야 합니다. Windows 방화벽을 사용 하 여 일시적으로 포트 차단을 해제 하거나 Windows 방화벽을 일시적으로 사용 하지 않도록 설정할 수 있습니다. 바이러스 백신 소프트웨어를 일시적으로 사용 하지 않도록 설정 해야 할 수도 있습니다. 설치 후 방화벽 및 바이러스 백신 소프트웨어를 사용 하도록 설정 해야 합니다.

### <a name="installing-the-extension-pack"></a>확장 팩 설치

에 데이터를 마이그레이션하기 전에 언제 든 지 확장 팩을 설치할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> 확장 팩을 설치 하려면 인스턴스에서 **sysadmin** 서버 역할의 멤버 여야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

확장 팩을 설치 하려면:

1. 을 실행 하는 컴퓨터에 **SSMAforOracleExtensionPack_ *n*.msi** (여기서 *n* 은 빌드 번호)를 복사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.
2. **SSMAforOracleExtensionPack_ *n*.msi** 를 두 번 클릭 합니다.
3. **시작** 페이지에서 **다음** 을 클릭합니다.
4. **최종 사용자 사용권 계약** 페이지에서 사용권 계약을 읽습니다. 동의 **하면 동의 함 옵션을** 선택 하 고 **다음** 을 클릭 합니다.
5. **설치 유형 선택** 페이지에서 **일반** 을 선택 합니다.
6. **설치 준비** 페이지에서 **설치** 를 선택합니다.
7. **설치의 첫 번째 단계 완료** 페이지에서 **다음** 을 선택 합니다.
  
   새 대화 상자가 나타납니다. 확장 팩 유형을 선택 합니다.
  
8. 원하는 설치 유형을 선택 하 고 **다음** 을 클릭 합니다.

   > [!IMPORTANT]
   > 원격 옵션은 Linux에서 실행 되는 확장 팩을 설치 하거나 대상으로 지정할 때만 사용 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows에서 실행 되는 설치에는 항상 확장 팩이 로컬로 설치 되어 있어야 합니다. [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 및 Azure Synapse Analytics는 확장 팩을 지원 하지 않습니다.

   로컬 인스턴스에 확장 팩을 설치 하는 경우 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서는 Oracle 스키마를 마이그레이션할 로컬 인스턴스를 선택할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 드롭다운에서 인스턴스를 선택 하 고 **다음** 을 선택 합니다.

   기본 인스턴스의 이름은 컴퓨터와 동일 합니다. 명명 된 인스턴스에는 백슬래시와 인스턴스 이름이 나옵니다.

9. 연결 페이지에서 인증 방법을 선택 하 고 **다음** 을 선택 합니다.

   Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그인을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 서버 인증을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호를 입력 해야 합니다.

10. 다음 단계에서는 서버 쪽 데이터를 마이그레이션하는 동안 확장 팩 데이터베이스에 저장 된 중요 한 데이터를 암호화 하는 데 사용 되는 마스터 키에 대 한 암호를 설정 해야 합니다. 강력한 암호를 입력 하 고 **다음** 을 클릭 합니다.

11. 다음 페이지에서 **유틸리티 데이터베이스 *n* 설치를 선택 하 고 확장 팩 라이브러리를 설치** 합니다. 여기서 *n* 은 버전 번호입니다. 테스터 기능을 사용 하려는 경우 **테스터 데이터베이스 설치** 확인란을 선택 하 고 **다음** 을 선택 합니다.

    이 데이터베이스에는 데이터 마이그레이션에 필요한 테이블 및 저장 프로시저 (서버 쪽 데이터 마이그레이션 엔진 사용)를 사용 하 여 **sysdb** 데이터베이스가 만들어집니다.

    **테스터 데이터베이스 설치** 옵션을 선택 하면 **ssmatesterdb** 데이터베이스가 생성 됩니다.

12. 설치가 완료 되 면 다른 인스턴스에 유틸리티 데이터베이스를 설치할지 묻는 메시지가 표시 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **예** 를 선택 하 고 **다음** 을 선택 하거나 마법사를 종료 하려면 **아니요** 를 선택한 다음 **끝내기** 를 선택 합니다.

13. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 유틸리티를 사용 하 여 `sqlcmd` 다음 스크립트를 실행 하 여 CLR을 사용 하도록 설정 합니다.

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    CLR을 사용 하지 않는 경우 SSMA를 연결할 때 다음과 같은 오류가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

    > SSMA가 확장 팩 어셈블리 버전 정보를 검색할 수 없습니다. 데이터베이스 서버에 확장 팩을 다시 설치 합니다.

### <a name="sql-server-database-objects"></a>데이터베이스 개체 SQL Server

확장 팩을 설치한 후에는 **ssma_oracle _migration_packages** 테이블이 **sysdb** 데이터베이스에 표시 됩니다.

데이터를로 마이그레이션할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만듭니다. 이러한 작업에는 **데이터 마이그레이션 패키지 {GUID} ssma_oracle** 이름이 지정 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 폴더의 에이전트 노드에 표시 됩니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .

또한 다음 확장 저장 프로시저는 **master** 데이터베이스에 추가 됩니다.

- `xp_ora2ms_exec2`
- `xp_ora2ms_exec2_ex`
- `xp_ora2ms_versioninfo2`

## <a name="see-also"></a>참조

- [Oracle 용 SSMA 클라이언트 설치](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [Oracle 데이터베이스를 SQL Server로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
