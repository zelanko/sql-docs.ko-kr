---
title: "ETL 워크플로 | Microsoft Docs"
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 06/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 679e58fe-b062-4934-a94c-9bb916b0bcb0
caps.latest.revision: "5"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 3b81a6494458f7d9f2e89b120119e402786e21ea
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 워크플로
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]WWI_Integration ETL 패키지에서에서 데이터를 마이그레이션하도록 WideWorldImporters 데이터베이스 WideWorldImportersDW 데이터베이스에 데이터 변경 내용으로 사용 됩니다. 패키지를 정기적으로 실행 (가장 일반적으로 매일)입니다.

## <a name="overview"></a>개요

패키지 사용 하 여 Integration Services SSIS (SQL Server) T-SQL 대량 작업을 오케스트레이션 하의 (아닌 s 별도 변환) 디자인 높은 성능을 보장 합니다.

차원, 팩트 테이블 하 여 뒤에 로드 됩니다. 언제 든 지 오류가 발생 한 후 패키지를 다시 실행할 수 있습니다.

워크플로 다음과 같습니다.

 ![WideWorldImporters ETL 워크플로](../../sample/world-wide-importers/media/wideworldimporters-etl-workflow.png)

적절 한 마감 시간 초과 작동 하는 식 작업으로 시작 합니다. 이 시간은 현재 시간 덜 몇 분입니다. (이 현재 시간으로 직접 데이터를 요청 하는 보다 더 강력). 그런 다음 모든 밀리초를 시간에서 자릅니다.

날짜 차원 테이블을 채우는 방법으로 주 처리를 시작 합니다. 현재 연도의 모든 날짜 테이블에 채워져 있는지 확인 합니다.

이후 부터는 각 차원의 다음 각 팩트는 일련의 데이터 흐름 태스크를 로드합니다.

## <a name="prerequisites"></a>필수 구성 요소

- SQL Server 2016 (또는 이상) WideWorldImporters 및 WideWorldImportersDW 데이터베이스와 함께 합니다. SQL Server의 동일한 또는 다른 인스턴스에서 수 있습니다.
- SSMS(SQL Server Management Studio)
- SQL Server 2016 Integration Services (SSIS).
  - SSIS 카탈로그를 만든 있는지 확인 합니다. 그렇지 않은 경우 마우스 오른쪽 단추로 클릭 하 여 **Integration Services** SSMS 개체 탐색기에서 선택 하 고 **카탈로그 추가**합니다. 기본값을 따릅니다. Sqlclr 하 고 암호를 제공 하려면 요청 합니다.


## <a name="download"></a>다운로드

샘플의 최신 버전:

[wide world-가져오기 도구 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)

SSIS 패키지 파일을 다운로드 **매일 ETL.ispac**합니다.

샘플 데이터베이스를 다시 만드는 소스 코드를 다음 위치에서 사용할 수 있습니다.

[wide world-importer](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Install

1. SSIS 패키지를 배포 합니다.
   - Windows 탐색기에서 "매일 ETL.ispac" 패키지를 엽니다. Integration Services 배포 마법사 시작 됩니다.
   - "원본 선택"에서 "매일 ETL.ispac" 패키지를 가리키는 경로을 기본 프로젝트 배포를 수행 합니다.
   - "대상 선택"에서 SSIS 카탈로그를 호스팅하는 서버의 이름을 입력 합니다.
   - SSIS 카탈로그의 새 폴더 "WideWorldImporters" 아래 예를 들어 아래의 경로 선택 합니다.
   - 배포를 클릭 하 여 마법사를 완료 합니다.

2. ETL 프로세스에 대 한 SQL Server 에이전트 작업을 만듭니다.
   - SSMS에서 마우스 오른쪽 단추로 클릭 "" SQL Server 에이전트 및 선택 새로 만들기-> 작업입니다.
   - 이름, 예를 들어 "WideWorldImporters ETL"를 선택 합니다.
   - "SQL Server Integration Services 패키지" 유형의 작업 단계를 추가 합니다.
   - SSIS 카탈로그를 사용 하 여 서버를 선택 하 고 "일일 ETL" 패키지를 선택 합니다.
   - 구성-> 연결 관리자는 원본 및 대상에 대 한 연결을 올바르게 구성 되었는지 확인 합니다. 기본값은 로컬 인스턴스에 연결할 수 있습니다.
   - 확인 작업을 만들려면 클릭 합니다.

3. 실행 하거나 작업을 예약 합니다.
