---
title: WideWorldImportersDW-ETL 워크플로 | Microsoft Docs
description: SQL Server Integration Services (SSIS)에서 ETL 패키지를 사용 하 여 주기적으로 WideWorldImporters 데이터베이스에서 WideWorldImportersDW로 데이터를 마이그레이션합니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1dfba407449b9517af2ed899f49387732c48353b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718527"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 워크플로
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
데이터가 변경 되 면 *WWI_Integration* ETL 패키지를 사용 하 여 WideWorldImporters 데이터베이스에서 WideWorldImportersDW 데이터베이스로 데이터를 마이그레이션합니다. 패키지가 정기적으로 실행 됩니다 (일반적으로 매일).

패키지는 SQL Server Integration Services을 사용 하 여 대량 T-sql 작업을 오케스트레이션 (Integration Services의 개별 변환 대신) 하 여 높은 성능을 보장 합니다.

차원이 먼저 로드 된 다음 팩트 테이블이 로드 됩니다. 오류가 발생 한 후 언제 든 지 패키지를 다시 실행할 수 있습니다.

워크플로는 다음과 같습니다.

 ![WideWorldImporters ETL 워크플로](media/wide-world-importers/wideworldimporters-etl-workflow.png)

워크플로는 적절 한 구분 시간을 결정 하는 식 작업으로 시작 합니다. 컷오프 시간은 현재 시간에서 몇 분을 뺀 값입니다. 이 접근 방식은 현재 시간에 대 한 데이터를 요청 하는 것 보다 더 강력 합니다. 시간에서 밀리초가 잘립니다.

주 처리는 날짜 차원 테이블을 채워서 시작 합니다. 처리를 수행 하면 현재 연도의 모든 날짜가 테이블에 채워집니다.

그런 다음 일련의 데이터 흐름 태스크가 각 차원을 로드 합니다. 그런 다음 각 팩트를 로드 합니다.

## <a name="prerequisites"></a>전제 조건

- WideWorldImporters 및 WideWorldImportersDW 데이터베이스를 사용 하는 SQL Server 2016 이상 (같거나 다른 SQL Server 인스턴스의)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Integration Services 카탈로그를 만들어야 합니다. Integration Services 카탈로그를 만들려면 SQL Server Management Studio 개체 탐색기에서 **Integration Services**을 마우스 오른쪽 단추로 클릭 한 다음 **추가 카탈로그**를 선택 합니다. 기본 옵션을 그대로 둡니다. SQLCLR을 사용 하도록 설정 하 고 암호를 제공 하 라는 메시지가 표시 됩니다.


## <a name="download"></a>다운로드

예제의 최신 릴리스는 [와이드-가져오기-릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)를 참조 하세요. *.Ispac* Integration Services 패키지 파일을 다운로드 합니다.

샘플 데이터베이스를 다시 만들기 위한 원본 코드는 [와이드-가져오기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis)를 참조 하세요.

## <a name="install"></a>설치

1. Integration Services 패키지를 배포 합니다.
   1. Windows 탐색기에서 *.ispac* 패키지를 엽니다. 그러면 SQL Server Integration Services 배포 마법사가 시작 됩니다.
   2. **원본 선택**에서 프로젝트 배포에 대 한 기본값을 따르고 *.ispac* 패키지를 가리키는 경로를 사용 합니다.
   3. **대상 선택**에서 Integration Services 카탈로그를 호스트 하는 서버의 이름을 입력 합니다.
   4. 예를 들어 이름이 *WideWorldImporters*인 새 폴더에서 Integration Services 카탈로그 아래에 있는 경로를 선택 합니다.
   5. **배포** 를 선택 하 여 마법사를 완료 합니다.

2. ETL 프로세스에 대 한 SQL Server 에이전트 작업을 만듭니다.
   1. Management Studio에서 **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭 한 다음 **새**  >  **작업**을 선택 합니다.
   2. 이름을 입력 합니다 (예: *WIDEWORLDIMPORTERS ETL*).
   3. **SQL Server Integration Services 패키지**형식의 **작업 단계** 를 추가 합니다.
   4. Integration Services 카탈로그가 있는 서버를 선택 하 고 *매일 ETL* 패키지를 선택 합니다.
   5. **구성**  >  **연결 관리자**에서 원본 및 대상에 대 한 연결이 올바르게 구성 되어 있는지 확인 합니다. 기본값은 로컬 인스턴스에 연결 하는 것입니다.
   6. **확인** 을 선택 하 여 작업을 만듭니다.

3. 작업을 실행 하거나 예약 합니다.
