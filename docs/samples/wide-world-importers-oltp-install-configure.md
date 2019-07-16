---
title: 설치 및 구성 WideWorldImporters 샘플 데이터베이스-SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6fc303892fdefda350a2bb6513a71226264e50fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067669"
---
# <a name="installation-and-configuration"></a>설치 및 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World Importers OLTP 데이터베이스 설치 및 구성 지침은입니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (또는 이상) 또는 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)합니다. 샘플의 전체 버전의 경우 SQL Server 평가/개발자/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과 사용 하 여 2016 년 6 월 릴리스 이상.

## <a name="download"></a>다운로드

샘플의 최신 릴리스:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Bacpac를 다운로드 샘플 WideWorldImporters 데이터베이스 백업/해당 하는 Azure SQL Database 또는 SQL Server의 버전입니다.

샘플 데이터베이스를 다시 소스 코드를 다음 위치에서 사용할 수 있습니다. 이 샘플을 다시 하면 데이터에서 약간의 차이가 데이터 생성에는 임의 요인을 이므로 참고:

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스에 백업을 복원 하려면 Management Studio를 사용할 수 있습니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드를 선택한 **Restore Database**합니다.
3. 선택 **장치** 단추를 클릭 하 고 **...**
4. 대화 상자에서 **백업 장치 선택**, 클릭 **추가**, 서버의 파일 시스템에서 데이터베이스 백업으로 이동 하 고 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 데이터에 대 한 대상 위치를 변경 하 고 로그 파일에는 **파일** 창입니다. 데이터 배치 하 고 여러 드라이브의 로그 파일에 대 한 모범 사례는 note 합니다.
6. **확인**을 클릭합니다. 데이터베이스 복원이 시작 됩니다. 완료 되 면 SQL Server 인스턴스에 설치 된 WideWorldImporters 데이터베이스를 해야 합니다.

### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

새 SQL Database를 bacpac로 가져오려면 Management Studio를 사용할 수 있습니다.

1. (선택 사항) 수행 하지 아직 있는 경우 SQL Server Azure를 이동할 합니다 [Azure portal](https://portal.azure.com/) 새 SQL 데이터베이스를 만듭니다. 데이터베이스 만들기, 서버를 만듭니다. 서버를 기록해 둡니다.
   - 참조 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 몇 분 안에 데이터베이스를 만들려면
2. SQL Server Management Studio를 열고 Azure에서 서버에 연결 합니다.
3. 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드를 선택한 **Import Data-tier Application**합니다.
4. 에 **설정 가져오기** 선택 **로컬 디스크에서 가져오기** 파일 시스템에서 예제 데이터베이스의 bacpac를 선택 합니다.
5. 아래 **데이터베이스 설정** 에 데이터베이스 이름을 변경 *WideWorldImporters* 를 사용 하 여 대상 버전 및 서비스 목표를 선택 합니다.
6. 클릭 **다음** 하 고 **마침** 배포를 시작 하도록 합니다. P1을 완료 하는 몇 분 정도 됩니다. 더 낮은 가격 책정 하는 경우 계층 필요한 경우 새 P1 데이터베이스를 가져오는 다음 원하는 수준으로 가격 책정 계층을 변경 하는 것이 좋습니다.

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>전체 텍스트 인덱싱

샘플 데이터베이스를 전체 텍스트 인덱싱 사용 가능 합니다. 그러나 해당 기능은 SQL Server를 사용 하 여 기본적으로 설치 되지는-(Azure SQL DB에는 기본적으로 사용은)는 SQL Server 설치 도중 선택 해야 합니다. 따라서 사후 설치 단계는 필요 합니다.

1. SQL Server Management Studio에서 WideWorldImporters 데이터베이스에 연결 하 고 새 쿼리 창을 엽니다.
2. 데이터베이스에서 전체 텍스트 인덱싱이 사용 하도록 설정 하려면 다음 T-SQL 명령을 실행 합니다.  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

적용 대상: SQL Server

SQL Server에서 감사를 사용 하면 서버 구성에 필요 합니다. WideWorldImporters 샘플에 대 한 SQL Server 감사를 사용 하려면 데이터베이스에 다음 문을 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyAuditing]

Azure SQL Database에서 감사를 통해 구성 됩니다 합니다 [Azure portal](https://portal.azure.com/)합니다.

### <a name="row-level-security"></a>행 수준 보안

적용 대상: Azure SQL 데이터베이스

행 수준 보안 WideWorldImporters bacpac 다운로드에서는 기본적으로 사용 되지 않습니다. 데이터베이스에서 행 수준 보안을 사용 하려면 다음 저장된 프로시저를 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

