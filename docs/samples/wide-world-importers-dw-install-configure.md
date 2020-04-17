---
title: 설치 & DW 와이드월드인더 샘플 데이터베이스 구성
description: SQL Server 관리 스튜디오를 사용하여 WideWorldImportersDW 샘플 데이터베이스를 다운로드, 설치 및 구성하려면 다음 지침을 따르십시오.
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
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488556"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>와이드월드수입업체DW 설치 및 구성
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
와이드월드ImportersDW 데이터베이스에 대한 설치 및 구성 지침.

- [SQL Server 2016(이상)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 또는 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/). 전체 버전의 샘플을 사용하려면 SQL 서버 평가/개발자/엔터프라이즈 버전을 사용합니다.
- [SQL 서버 관리 스튜디오](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 얻으려면 2016년 6월 릴리스 또는 그 이후를 사용하십시오.

## <a name="download"></a>다운로드

샘플의 최신 릴리스:

[전 세계 수입업체 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server 또는 Azure SQL 데이터베이스 버전에 해당하는 와이드월드ImportersDW 데이터베이스 백업/bacpac 샘플을 다운로드합니다.

샘플 데이터베이스를 다시 만드는 소스 코드는 다음 위치에서 사용할 수 있습니다. 데이터 모집단은 OLTP 데이터베이스(와이드월드인포터)의 ETL을 기반으로 합니다.

[세계적인 수입업자-소스](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>설치


### <a name="sql-server"></a>SQL Server

SQL Server 인스턴스에 백업을 복원하려면 관리 스튜디오를 사용할 수 있습니다.

1. SQL Server 관리 Studio를 열고 대상 SQL Server 인스턴스에 연결합니다.
2. 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원을** **선택합니다.**
3. **장치를** 선택하고 버튼을 클릭 **...**
4. 대화 상자 백업 **장치 선택에서** **추가를**클릭하고 서버의 파일 시스템에서 데이터베이스 백업으로 이동한 다음 백업을 선택합니다. **확인**을 클릭합니다.
5. 필요한 경우 **파일** 창에서 데이터 및 로그 파일의 대상 위치를 변경합니다. 데이터를 배치하고 파일을 다른 드라이브에 기록하는 것이 좋습니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원이 시작됩니다. 완료되면 SQL Server 인스턴스에 데이터베이스 와이드월드Importers가 설치됩니다.

### <a name="azure-sql-database"></a>Azure SQL Database

bacpac을 새 SQL 데이터베이스로 가져오려면 관리 스튜디오를 사용할 수 있습니다.

1. (선택 사항) Azure에 아직 SQL Server가 없는 경우 [Azure 포털로](https://portal.azure.com/) 이동하여 새 SQL Database를 만듭니다. 데이터베이스를 만드는 과정에서 서버를 만듭니다. 서버를 기록해 둡을 기록합니다.
   - 몇 분 안에 데이터베이스를 만들려면 [이 자습서를](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 참조하십시오.
2. SQL Server 관리 Studio를 열고 Azure의 서버에 연결합니다.
3. 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **데이터 계층 응용 프로그램 가져오기를** **선택합니다.**
4. 가져오기 **설정에서** **로컬 디스크에서 가져오기를** 선택하고 파일 시스템에서 샘플 데이터베이스의 bacpac을 선택합니다.
5. **데이터베이스 설정에서** 데이터베이스 이름을 *와이드월드ImportersDW로* 변경하고 사용할 대상 버전 및 서비스 목표를 선택합니다.
6. **다음** 및 **완료를** 클릭하여 배포를 시작합니다. 작업을 완료하는 데 몇 분 정도 걸립니다. S2보다 낮은 서비스 목표를 지정할 때 더 오래 걸릴 수 있습니다.

## <a name="configuration"></a>Configuration

[SQL Server 2016(이후) 개발자/평가/엔터프라이즈 에디션에 적용]

샘플 데이터베이스는 PolyBase를 사용하여 Hadoop 또는 Azure Blob 저장소의 파일을 쿼리할 수 있습니다. 그러나 이 기능은 SQL Server에 기본적으로 설치되지 않으며 SQL Server 설정 중에 선택해야 합니다. 따라서 설치 후 단계가 필요합니다.

1. SQL 서버 관리 스튜디오에서 WideWorldImportersDW 데이터베이스에 연결하고 새 쿼리 창을 엽니다.
2. 다음 T-SQL 명령을 실행하여 데이터베이스에서 PolyBase를 사용할 수 있습니다.

   [응용 프로그램]을 실행합니다. 【Configuration_ApplyPolyBase】
