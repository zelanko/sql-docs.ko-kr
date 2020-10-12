---
title: DW WideWorldImporters 샘플 데이터베이스 설치 & 구성
description: SQL Server Management Studio를 사용 하 여 WideWorldImportersDW 예제 데이터베이스를 다운로드, 설치 및 구성 하려면 다음 지침을 따르세요.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 18d4e9c18c4848a0857c1afb146b0d0405f418ce
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956564"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW 설치 및 구성
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 데이터베이스에 대 한 설치 및 구성 지침을 설명 합니다.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 이상 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)합니다. 전체 버전의 샘플을 사용 하려면 SQL Server Evaluation/Developer/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 위해 6 월 2016 릴리스 이상을 사용 합니다.

## <a name="download"></a>다운로드

예제의 최신 릴리스는 다음과 같습니다.

[와이드-가져오기-릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server 또는 Azure SQL Database 버전에 해당 하는 샘플 WideWorldImportersDW database backup/bacpac를 다운로드 합니다.

예제 데이터베이스를 다시 만드는 소스 코드는 다음 위치에서 사용할 수 있습니다. 데이터 채우기는 OLTP 데이터베이스 (WideWorldImporters)의 ETL을 기반으로 합니다.

[와이드-가져오기-소스](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>설치


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스에 백업을 복원 하려면 Management Studio를 사용할 수 있습니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스 복원**을 선택 합니다.
3. **장치** 를 선택 하 **고 단추를 클릭 합니다.**
4. 대화 상자에서 **백업 장치를 선택**하 고, **추가**를 클릭 하 고, 서버의 파일 시스템에 있는 데이터베이스 백업으로 이동 하 고, 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 **파일** 창에서 데이터 및 로그 파일의 대상 위치를 변경 합니다. 데이터와 로그 파일을 서로 다른 드라이브에 저장 하는 것이 가장 좋습니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원이 시작 됩니다. 완료 되 면 데이터베이스 WideWorldImporters이 SQL Server 인스턴스에 설치 됩니다.

### <a name="azure-sql-database"></a>Azure SQL Database

Bacpac를 새 SQL Database 가져오려면 Management Studio를 사용할 수 있습니다.

1. 필드 Azure에 아직 SQL Server 없는 경우 [Azure Portal](https://portal.azure.com/) 로 이동 하 여 새 SQL Database를 만듭니다. 데이터베이스를 만드는 과정에서 서버를 만듭니다. 서버를 기록해 둡니다.
   - 몇 분만에 데이터베이스를 만들려면 [이 자습서](/azure/azure-sql/database/single-database-create-quickstart) 를 참조 하세요.
2. SQL Server Management Studio를 열고 Azure에서 서버에 연결 합니다.
3. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **Data-Tier 응용 프로그램 가져오기**를 선택 합니다.
4. **가져오기 설정** 에서 **로컬 디스크에서 가져오기** 를 선택 하 고 파일 시스템에서 샘플 데이터베이스의 bacpac를 선택 합니다.
5. **데이터베이스 설정** 에서 데이터베이스 이름을 *WideWorldImportersDW* 로 변경 하 고 사용할 대상 버전 및 서비스 목표를 선택 합니다.
6. **다음** 을 클릭 하 고 **마침** 을 클릭 하 여 배포를 시작 합니다. 작업을 완료하는 데 몇 분 정도 걸립니다. S2 보다 낮은 서비스 목표를 지정 하는 경우 시간이 오래 걸릴 수 있습니다.

## <a name="configuration"></a>구성

[SQL Server 2016 이상) Developer/Evaluation/Enterprise Edition에 적용 됩니다.

예제 데이터베이스는 PolyBase를 사용 하 여 Hadoop 또는 Azure blob 저장소에서 파일을 쿼리할 수 있습니다. 그러나이 기능은 기본적으로 SQL Server와 함께 설치 되지 않으므로 SQL Server 설치 하는 동안 선택 해야 합니다. 따라서 사후 설치 단계가 필요 합니다.

1. SQL Server Management Studio에서 WideWorldImportersDW 데이터베이스에 연결 하 고 새 쿼리 창을 엽니다.
2. 다음 T-sql 명령을 실행 하 여 데이터베이스에서 PolyBase를 사용 하도록 설정 합니다.

   [응용 프로그램]을 실행 합니다. [Configuration_ApplyPolyBase]