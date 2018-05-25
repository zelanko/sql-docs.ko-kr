---
title: WideWorldImportersDW-ETL 워크플로 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36638c4cc2bda58ac277822d5c4a4ce5421ab8b4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 워크플로
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
사용 하 여는 *WWI_Integration* ETL 패키지에서에서 데이터를 마이그레이션하도록 WideWorldImporters 데이터베이스 WideWorldImportersDW 데이터베이스에 데이터가 변경 합니다. 패키지를 정기적으로 실행 됩니다 (일반적으로 매일)입니다.

패키지를 Integration Services에서 별도 변환) 하는 경우 (대신 T-SQL 대량 작업을 오케스트레이션 하 SQL Server Integration Services를 사용 하 여 고성능을 확인 합니다.

차원 먼저 로드 되 고 팩트 테이블이 로드 되는 다음 합니다. 실패 후 언제 든 지 패키지를 실행할 수 있습니다.

워크플로 다음과 같습니다.

 ![WideWorldImporters ETL 워크플로](media/wide-world-importers/wideworldimporters-etl-workflow.png)

워크플로에 적절 한 마감 시간을 결정 하는 식 작업으로 시작 합니다. 구분 기준 시간은 현재 시간 몇 분에서 뺀입니다. (이 방법은 요청 하는 데이터 오른쪽을 현재 시간 보다 더 강력 합니다.) 모든 시간 (밀리초) 시점부터 잘립니다.

날짜 차원 테이블을 채우는 방법으로 주 처리를 시작 합니다. 처리는 현재 연도 대 한 모든 날짜 테이블에 채워져 있는지 확인 합니다.

다음으로, 일련의 데이터 흐름 태스크는 각 차원을 로드합니다. 그런 다음 각 팩트를 로드 합니다.

## <a name="prerequisites"></a>필수 구성 요소

- SQL Server 2016 (이상), WideWorldImporters 및 WideWorldImportersDW 데이터베이스 (동일 또는 다른 SQL Server 인스턴스)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Integration Services 카탈로그를 만드는 것을 확인 합니다. SQL Server Management Studio 개체 탐색기에서 Integration Services 카탈로그를 만들려는 마우스 오른쪽 단추로 클릭 **Integration Services**를 선택한 후 **카탈로그 추가**합니다. 기본 옵션을 그대로 둡니다. SQLCLR를 사용 하도록 설정 하 고 암호를 입력 하 라는 메시지가 표시 됩니다.


## <a name="download"></a>다운로드

샘플의 최신 버전에서는 [world importers 릴리스 와이드](http://go.microsoft.com/fwlink/?LinkID=800630)합니다. 다운로드는 *매일 ETL.ispac* Integration Services 패키지 파일입니다.

예제 데이터베이스를 다시 만들려고 소스 코드를 보려면 [wide world-importer](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)합니다.

## <a name="install"></a>설치

1. Integration Services 패키지를 배포 합니다.
   1. Windows 탐색기를 열고는 *매일 ETL.ispac* 패키지 합니다. SQL Server Integration Services 배포 마법사가 시작 됩니다.
   2. 아래 **원본 선택**를 가리키는 경로와 프로젝트 배포에 대 한 기본값을 따릅니다는 *매일 ETL.ispac* 패키지 합니다.
   3. 아래 **대상 선택**, Integration Services 카탈로그를 호스팅하는 서버의 이름을 입력 합니다.
   4. 예를 들어 라는 새 폴더에서 Integration Services 카탈로그 아래에서 경로 선택 *WideWorldImporters*합니다.
   5. 선택 **배포** 마법사를 마칩니다.

2. ETL 프로세스에 대 한 SQL Server 에이전트 작업을 만듭니다.
   1. Management Studio에서 마우스 오른쪽 단추로 클릭 **SQL Server 에이전트**를 선택한 후 **새로** > **작업**합니다.
   2. 예를 들어 이름을 입력 *WideWorldImporters ETL*합니다.
   3. 추가 **작업 단계** 형식의 **SQL Server Integration Services 패키지**합니다.
   4. Integration Services 카탈로그에 있는 서버를 선택한 다음 선택에서 *일일 ETL* 패키지 합니다.
   5. 아래 **구성** > **연결 관리자**, 원본 및 대상에 대 한 연결을 올바르게 구성 되어 있는지 확인 합니다. 기본값은 로컬 인스턴스에 연결할 수 있습니다.
   6. 선택 **확인** 작업을 만들어야 합니다.

3. 실행 하거나 작업을 예약 합니다.
