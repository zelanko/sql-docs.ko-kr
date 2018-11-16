---
title: WideWorldImportersDW-ETL 워크플로 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d17cc2ccc46733c857f884f78a1b0c9b3f980586
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674112"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 워크플로
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
사용 된 *WWI_Integration* WideWorldImporters 데이터베이스에서 데이터가 변경 될 때 WideWorldImportersDW 데이터베이스로 데이터를 마이그레이션할 ETL 패키지 있습니다. 패키지는 정기적으로 실행 됩니다 (일반적으로 매일)입니다.

패키지 (Integration Services에서 별도 변환) 하는 대신 T-SQL 대량 작업을 오케스트레이션 하기 위해 SQL Server Integration Services를 사용 하 여 고성능을 보장 합니다.

차원 먼저 로드 되 고 팩트 테이블이 로드 되는 다음입니다. 실패 후 언제 든 지 패키지에 다시 실행할 수 있습니다.

워크플로 다음과 같습니다.

 ![WideWorldImporters ETL 워크플로](media/wide-world-importers/wideworldimporters-etl-workflow.png)

워크플로 적절 한 차단 시간을 결정 하는 식 작업을 시작 합니다. 차단 시간은 현재 시간에서 몇 분을 뺀 값입니다. (이 방식은 현재 시간으로 직접 데이터를 요청 하는 보다 더 강력 합니다.) 모든 시간 (밀리초)는 시간에서 잘립니다.

주 처리 날짜 차원 테이블을 채우는 방법으로 시작 합니다. 처리 하는 테이블의 모든 날짜는 현재 연도를 채워져 있는지 확인 합니다.

다음으로, 일련의 데이터 흐름 작업을 각 차원을 로드합니다. 그런 다음 각 팩트를 로드 합니다.

## <a name="prerequisites"></a>필수 구성 요소

- SQL Server 2016 (이상), WideWorldImporters 및 WideWorldImportersDW 데이터베이스 (동일한 또는 다른 인스턴스의 SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Integration Services 카탈로그를 만드는 것을 확인 합니다. SQL Server Management Studio 개체 탐색기에서 Integration Services 카탈로그를 만들려면 마우스 오른쪽 단추로 클릭 **Integration Services**를 선택한 후 **카탈로그 추가**합니다. 기본 옵션을 그대로 둡니다. SQLCLR을 사용 하도록 설정 하 고 암호를 제공 하 라는 메시지가 표시 됩니다.


## <a name="download"></a>다운로드

샘플의 최신 릴리스를 참조 하세요 [wide world-importers 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다. 다운로드 합니다 *일일 ETL.ispac* Integration Services 패키지 파일입니다.

샘플 데이터베이스를 다시 만들려면 소스 코드를 보려면 [importers-world wide-](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)합니다.

## <a name="install"></a>설치

1. Integration Services 패키지를 배포 합니다.
   1. Windows 탐색기에서 엽니다는 *일일 ETL.ispac* 패키지 있습니다. SQL Server Integration Services 배포 마법사가 시작 됩니다.
   2. 아래 **원본 선택**을 가리키는 경로 사용 하 여 프로젝트 배포에 대 한 기본값을 따릅니다 합니다 *일일 ETL.ispac* 패키지 합니다.
   3. 아래 **대상 선택**, Integration Services 카탈로그를 호스팅하는 서버의 이름을 입력 합니다.
   4. 예를 들어 라는 새 폴더에서 Integration Services 카탈로그에서 경로 선택 *WideWorldImporters*합니다.
   5. 선택 **배포** 마법사를 마칩니다.

2. ETL 프로세스에 대 한 SQL Server 에이전트 작업을 만듭니다.
   1. Management studio에서 마우스 오른쪽 단추로 클릭 **SQL Server 에이전트**를 선택한 후 **새로 만들기** > **작업**합니다.
   2. 예를 들어, 이름을 입력 *WideWorldImporters ETL*합니다.
   3. 추가 된 **작업 단계** 형식의 **SQL Server Integration Services 패키지**합니다.
   4. Integration Services 카탈로그에 있는 서버를 선택 하 고 다음을 선택 합니다 *일일 ETL* 패키지 있습니다.
   5. 아래 **Configuration** > **연결 관리자**, 원본 및 대상에 대 한 연결이 올바르게 구성 되어 있는지 확인 합니다. 기본 로컬 인스턴스에 연결 하는 것입니다.
   6. 선택 **확인** 작업을 만듭니다.

3. 실행 하거나 작업을 예약 합니다.
