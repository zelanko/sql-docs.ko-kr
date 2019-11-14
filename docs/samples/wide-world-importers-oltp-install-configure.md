---
title: WideWorldImporters 샘플 데이터베이스 설치 및 구성
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: e1683adfa20851d279e8b8e18a3c767db9e5810d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056271"
---
# <a name="installation-and-configuration"></a>설치 및 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide 세계 가져오기 OLTP 데이터베이스 설치 및 구성 지침

## <a name="prerequisites"></a>전제 조건

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 이상 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)합니다. 샘플의 전체 버전은 SQL Server Evaluation/Developer/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 위해 6 월 2016 릴리스 이상을 사용 합니다.

## <a name="download"></a>다운로드

예제의 최신 릴리스는 다음과 같습니다.

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server 또는 Azure SQL Database 버전에 해당 하는 샘플 WideWorldImporters database backup/bacpac를 다운로드 합니다.

예제 데이터베이스를 다시 만드는 소스 코드는 다음 위치에서 사용할 수 있습니다. 데이터 생성에 임의 요소가 있으므로 샘플을 다시 만들면 데이터에 약간의 차이가 발생 합니다.

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스에 백업을 복원 하려면 Management Studio를 사용할 수 있습니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스 복원**을 선택 합니다.
3. **장치** 를 선택 하 **고 단추를 클릭 합니다.**
4. 대화 상자에서 **백업 장치를 선택**하 고, **추가**를 클릭 하 고, 서버의 파일 시스템에 있는 데이터베이스 백업으로 이동 하 고, 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 **파일** 창에서 데이터 및 로그 파일의 대상 위치를 변경 합니다. 데이터와 로그 파일을 서로 다른 드라이브에 저장 하는 것이 가장 좋습니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원이 시작 됩니다. 완료 되 면 데이터베이스 WideWorldImporters이 SQL Server 인스턴스에 설치 됩니다.

### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

Bacpac를 새 SQL Database 가져오려면 Management Studio를 사용할 수 있습니다.

1. 필드 Azure에 아직 SQL Server 없는 경우 [Azure Portal](https://portal.azure.com/) 로 이동 하 여 새 SQL Database를 만듭니다. 데이터베이스를 만드는 과정에서 서버를 만듭니다. 서버를 기록해 둡니다.
   - 몇 분만에 데이터베이스를 만들려면 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 를 참조 하세요.
2. SQL Server Management Studio를 열고 Azure에서 서버에 연결 합니다.
3. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **데이터 계층 응용 프로그램 가져오기**를 선택 합니다.
4. **가져오기 설정** 에서 **로컬 디스크에서 가져오기** 를 선택 하 고 파일 시스템에서 샘플 데이터베이스의 bacpac를 선택 합니다.
5. **데이터베이스 설정** 에서 데이터베이스 이름을 *WideWorldImporters* 로 변경 하 고 사용할 대상 버전 및 서비스 목표를 선택 합니다.
6. **다음** 을 클릭 하 고 **마침** 을 클릭 하 여 배포를 시작 합니다. P1에서 완료 하는 데 몇 분이 걸립니다. 낮은 가격 책정 계층을 원하는 경우 새 P1 데이터베이스로 가져온 다음 가격 책정 계층을 원하는 수준으로 변경 하는 것이 좋습니다.

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>전체 텍스트 인덱싱

예제 데이터베이스는 전체 텍스트 인덱싱을 사용할 수 있습니다. 그러나이 기능은 기본적으로 SQL Server와 함께 설치 되지 않습니다. SQL Server 설치 중에 선택 해야 합니다 (Azure SQL DB에서 기본적으로 사용 하도록 설정 됨). 따라서 사후 설치 단계가 필요 합니다.

1. SQL Server Management Studio에서 WideWorldImporters 데이터베이스에 연결 하 고 새 쿼리 창을 엽니다.
2. 다음 T-sql 명령을 실행 하 여 데이터베이스에서 전체 텍스트 인덱싱을 사용할 수 있도록 설정 합니다. `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

적용 대상: SQL Server

SQL Server에서 감사를 사용 하도록 설정 하려면 서버 구성이 필요 합니다. WideWorldImporters 샘플에 대 한 SQL Server 감사를 사용 하도록 설정 하려면 데이터베이스에서 다음 문을 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyAuditing]

Azure SQL Database에서 감사는 [Azure Portal](https://portal.azure.com/)를 통해 구성 됩니다.

### <a name="row-level-security"></a>행 수준 보안

적용 대상: Azure SQL Database

행 수준 보안은 WideWorldImporters의 bacpac 다운로드에서 기본적으로 사용 하도록 설정 되어 있지 않습니다. 데이터베이스에서 행 수준 보안을 사용 하도록 설정 하려면 다음 저장 프로시저를 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

