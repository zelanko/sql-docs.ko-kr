---
title: 예제 데이터베이스 WideWorldImporters OLAP-설치 및 구성-SQL | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6de9d9493178689a29cc90e79e228a9cb07aaace
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW 설치 및 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
WideWorldImportersDW 데이터베이스에 대 한 설치 및 구성 지침은 합니다.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (또는 이상) 또는 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/)합니다. 이 샘플의 전체 버전을 사용 하려면 SQL Server 평가/개발자/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 2016 년 6 월 릴리스를 사용 하는 최상의 결과 대 한 이후 버전입니다.

## <a name="download"></a>다운로드

샘플의 최신 버전:

[wide-world-importers-release](http://go.microsoft.com/fwlink/?LinkID=800630)

Bacpac를 다운로드 샘플 WideWorldImportersDW 데이터베이스 백업/해당 하는 SQL Server 또는 Azure SQL 데이터베이스의 버전입니다.

샘플 데이터베이스를 다시 만드는 소스 코드를 다음 위치에서 사용할 수 있습니다. (WideWorldImporters) OLTP 데이터베이스에서 ETL에 데이터 채우기가 기반 하는 참고:

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>설치


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스를 백업을 복원 하려면 Management Studio를 사용할 수 있습니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드를 선택한 **데이터베이스 복원**합니다.
3. 선택 **장치** 단추를 클릭 하 고 **...**
4. 대화 상자에서 **백업 장치 선택**, 클릭 **추가**서버의 파일 시스템에 데이터베이스 백업으로 이동 하 고 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 데이터에 대 한 대상 위치를 변경 하 고 로그 파일에는 **파일** 창. 데이터 배치 및 로그 파일은 서로 다른 드라이브에 가장 좋은 방법은 임을 note 합니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원을 시작 합니다. 완료 되 면 SQL Server 인스턴스에 설치 된 WideWorldImporters 데이터베이스를 해야 합니다.

### <a name="azure-sql-database"></a>Azure SQL Database

새 SQL 데이터베이스를 bacpac로 가져오려면 Management Studio를 사용할 수 있습니다.

1. (선택 사항) Azure에서 SQL Server를 없는 수행 하는 경우 이동할는 [Azure 포털](https://portal.azure.com/) 새 SQL 데이터베이스를 만듭니다. 데이터베이스를 만드는 중,에서 서버를 만듭니다. 서버를 기록해 둡니다.
   - 참조 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 분 후에 데이터베이스를 만들려면
2. SQL Server Management Studio를 열고 Azure의 서버에 연결 합니다.
3. 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드를 선택한 **데이터 계층 응용 프로그램 가져오기**합니다.
4. 에 **설정 가져오기** 선택 **로컬 디스크에서 가져오기** 파일 시스템에서 예제 데이터베이스의 bacpac를 선택 합니다.
5. 아래 **데이터베이스 설정** 에 데이터베이스 이름을 변경 *WideWorldImportersDW* 하 고 사용 하려면 대상 버전 및 서비스 목표를 선택 합니다.
6. 클릭 **다음** 및 **마침** 배포를 시작 하기. 완료 하는 데 몇 분 정도 걸립니다. S2 보다 낮은 서비스 목표를 지정 하는 경우에 더 오래 걸릴 수 있습니다.

## <a name="configuration"></a>Configuration

[SQL Server 2016 (이상) 개발자/평가/Enterprise Edition에 적용 됩니다]

예제 데이터베이스는 PolyBase에서 Hadoop 또는 Azure blob 저장소 쿼리 파일을 사용 하 여 가능 합니다. 그러나 해당 기능이 SQL Server와 함께 기본적으로 설치 되어 있지-SQL Server 설치 도중 선택 해야 합니다. 따라서 사후 설치 단계는 필요 합니다.

1. SQL Server Management Studio에서 WideWorldImportersDW 데이터베이스에 연결 하 고 새 쿼리 창을 엽니다.
2. 데이터베이스에 PolyBase 사용 하도록 설정 하려면 다음 T-SQL 명령을 실행 합니다.

   [응용 프로그램]을 실행 합니다. [Configuration_ApplyPolyBase]
