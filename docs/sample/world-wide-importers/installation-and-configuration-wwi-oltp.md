---
title: "설치 및 구성 | Microsoft Docs"
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dd1f09b-dcff-4627-899a-eca5162d9e5b
caps.latest.revision: "4"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: ef13bdeef7991953bf910b97a220a3edc824ce4f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="installation-and-configuration"></a>설치 및 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wide World Importers OLTP 데이터베이스 설치 및 구성 지침입니다.

## <a name="prerequisites"></a>필수 구성 요소

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) (또는 이상) 또는 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/)합니다. 샘플의 전체 버전에 대 한 SQL Server 평가/개발자/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md). 2016 년 6 월 릴리스를 사용 하는 최상의 결과 대 한 이후 버전입니다.

## <a name="download"></a>다운로드

샘플의 최신 버전:

[wide world-가져오기 도구 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)

Bacpac를 다운로드 샘플 WideWorldImporters 데이터베이스 백업/해당 하는 SQL Server 또는 Azure SQL 데이터베이스의 버전입니다.

샘플 데이터베이스를 다시 만드는 소스 코드를 다음 위치에서 사용할 수 있습니다. 샘플을 다시 만드는 발생 않을 것임 데이터에서 약간의 차이가 데이터 생성에는 임의 요인을 이므로 참고:

[wide world-importer](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스를 백업을 복원 하려면 Management Studio를 사용할 수 있습니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드를 선택한 **데이터베이스 복원**합니다.
3. 선택 **장치** 단추를 클릭 하 고 **...**
4. 대화 상자에서 **백업 장치 선택**, 클릭 **추가**서버의 파일 시스템에 데이터베이스 백업으로 이동 하 고 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 데이터에 대 한 대상 위치를 변경 하 고 로그 파일에는 **파일** 창. 데이터 배치 및 로그 파일은 서로 다른 드라이브에 가장 좋은 방법은 임을 note 합니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원을 시작 합니다. 완료 되 면 SQL Server 인스턴스에 설치 된 WideWorldImporters 데이터베이스를 해야 합니다.

### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

새 SQL 데이터베이스를 bacpac로 가져오려면 Management Studio를 사용할 수 있습니다.

1. (선택 사항) Azure에서 SQL Server를 없는 수행 하는 경우 이동할는 [Azure 포털](https://portal.azure.com/) 새 SQL 데이터베이스를 만듭니다. 데이터베이스를 만드는 중,에서 서버를 만듭니다. 서버를 기록해 둡니다.
   - 참조 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 분 후에 데이터베이스를 만들려면
2. SQL Server Management Studio를 열고 Azure의 서버에 연결 합니다.
3. 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드를 선택한 **데이터 계층 응용 프로그램 가져오기**합니다.
4. 에 **설정 가져오기** 선택 **로컬 디스크에서 가져오기** 파일 시스템에서 예제 데이터베이스의 bacpac를 선택 합니다.
5. 아래 **데이터베이스 설정** 에 데이터베이스 이름을 변경 *WideWorldImporters* 하 고 사용 하려면 대상 버전 및 서비스 목표를 선택 합니다.
6. 클릭 **다음** 및 **마침** 배포를 시작 하기. 에 P1를 완료 하는 데 몇 분 정도 됩니다. 더 낮은 가격 책정 계층은 원하는, 새 P1 데이터베이스로 가져올 한 다음 원하는 수준으로 가격 책정 계층을 변경 하는 것이 좋습니다.

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>전체 텍스트 인덱싱

예제 데이터베이스의 전체 텍스트 인덱싱을 사용 하 여 만들 수 있습니다. 그러나 해당 기능이 SQL Server와 함께 기본적으로 설치 되어 있지은-(Azure SQL DB에서 기본적으로 사용은)는 SQL Server 설치 도중 선택 해야 합니다. 따라서 사후 설치 단계는 필요 합니다.

1. SQL Server Management Studio에서 WideWorldImporters 데이터베이스에 연결 하 고 새 쿼리 창을 엽니다.
2. 데이터베이스 전체 텍스트 인덱싱을 사용 하도록 설정 하려면 다음 T-SQL 명령을 실행 합니다.`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

적용 대상: SQL Server

SQL Server의 감사를 사용 하면 서버 구성이 필요 합니다. WideWorldImporters 샘플에 대 한 SQL Server audit를 사용 하려면 데이터베이스에 다음 문을 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyAuditing]

Azure SQL 데이터베이스 감사를 통해 구성 된는 [Azure 포털](https://portal.azure.com/)합니다.

### <a name="row-level-security"></a>행 수준 보안

적용 대상: Azure SQL 데이터베이스

행 수준 보안은 WideWorldImporters의 bacpac 다운로드에는 기본적으로 사용할 수 없습니다. 데이터베이스에서 행 수준 보안을 사용 하려면 다음 저장된 프로시저를 실행 합니다.

    EXECUTE [Application].[Configuration_ApplyAuditing]

