---
title: 와이드월드수입업자 샘플 데이터베이스 설치 및 구성
description: 이 지침에 따라 SQL Server 관리 스튜디오를 사용하여 WideWorldImporters 샘플 데이터베이스를 다운로드, 설치 및 구성할 수 있습니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 355eaa254fcc7bb6cd4aa9a39c2cbcb269d88396
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487072"
---
# <a name="installation-and-configuration"></a>설치 및 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
와이드 월드 수입업체 OLTP 데이터베이스 설치 및 구성 지침.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2016(이상)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 또는 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/). 전체 버전의 샘플에서는 SQL 서버 평가/개발자/엔터프라이즈 버전을 사용합니다.
- [SQL 서버 관리 스튜디오](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 얻으려면 2016년 6월 릴리스 또는 그 이후를 사용하십시오.

## <a name="download"></a>다운로드

샘플의 최신 릴리스:

[전 세계 수입업체 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server 또는 Azure SQL 데이터베이스 버전에 해당하는 와이드월드Importers 데이터베이스 백업/bacpac 샘플을 다운로드합니다.

샘플 데이터베이스를 다시 만드는 소스 코드는 다음 위치에서 사용할 수 있습니다. 샘플을 다시 만들면 데이터 생성에 임의 요소가 있기 때문에 데이터에 약간의 차이가 발생합니다.

[세계적인 수입업체](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

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
5. **데이터베이스 설정에서** 데이터베이스 이름을 *와이드월드Importers로* 변경하고 사용할 대상 버전 및 서비스 목표를 선택합니다.
6. **다음** 및 **완료를** 클릭하여 배포를 시작합니다. P1에서 완료하는 데 몇 분 이내입니다. 더 낮은 가격 책정 계층이 필요한 경우 새 P1 데이터베이스로 가져온 다음 가격 책정 계층을 원하는 수준으로 변경하는 것이 좋습니다.

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>전체 텍스트 인덱싱

샘플 데이터베이스는 전체 텍스트 인덱싱을 사용할 수 있습니다. 그러나 이 기능은 기본적으로 SQL Server에 설치되지 않습니다 - SQL Server 설정 중에 선택해야 합니다(Azure SQL DB에서 기본적으로 활성화되어 있음). 따라서 설치 후 단계가 필요합니다.

1. SQL Server 관리 스튜디오에서 WideWorldImporters 데이터베이스에 연결하고 새 쿼리 창을 엽니다.
2. 다음 T-SQL 명령을 실행하여 데이터베이스에서 전체 텍스트 인덱싱을 사용할 수 있습니다.`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

적용 대상: SQL Server

SQL Server에서 감사를 사용하도록 설정하려면 서버 구성이 필요합니다. WideWorldImporters 샘플에 대한 SQL Server 감사를 사용하려면 데이터베이스에서 다음 문을 실행합니다.

    EXECUTE [Application].[Configuration_ApplyAuditing]

Azure SQL 데이터베이스에서 감사는 [Azure 포털을](https://portal.azure.com/)통해 구성됩니다.

### <a name="row-level-security"></a>행 수준 보안

적용 대상: Azure SQL 데이터베이스

와이드월드인더스의 bacpac 다운로드에서는 행 수준 보안이 기본적으로 활성화되지 않습니다. 데이터베이스에서 행 수준 보안을 사용하려면 다음 저장 절차를 실행합니다.

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

