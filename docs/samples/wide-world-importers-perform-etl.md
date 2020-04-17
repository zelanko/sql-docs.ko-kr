---
title: 와이드월드수입업체DW - ETL 워크플로우 | 마이크로 소프트 문서
description: SQL 서버 통합 서비스(SSIS)가 있는 ETL 패키지를 사용하여 정기적으로 와이드월드Importers 데이터베이스에서 와이드월드ImportersDW로 데이터를 마이그레이션합니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487432"
---
# <a name="wideworldimportersdw-etl-workflow"></a>와이드월드임프러스DW ETL 워크플로우
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
*WWI_Integration* ETL 패키지를 사용하여 데이터가 변경될 때 와이드월드Importers 데이터베이스에서 와이드월드ImportersDW 데이터베이스로 데이터를 마이그레이션합니다. 패키지는 주기적으로 실행됩니다(일반적으로 매일).

이 패키지는 SQL Server 통합 서비스를 사용하여 통합 서비스에서 별도의 변환 대신 대량 T-SQL 작업을 오케스트레이션하여 높은 성능을 보장합니다.

차원이 먼저 로드된 다음 팩트 테이블이 로드됩니다. 오류가 발생한 후 언제든지 패키지를 다시 실행할 수 있습니다.

워크플로는 다음과 같습니다.

 ![와이드월드임포트ETL 워크플로우](media/wide-world-importers/wideworldimporters-etl-workflow.png)

워크플로는 적절한 차단 시간을 결정하는 표현식 작업으로 시작합니다. 컷오프 시간은 현재 시간에서 몇 분을 뺀 값입니다. 이 방법은 현재 시간에 대한 데이터 권리를 요청하는 것보다 더 강력합니다. 모든 밀리초는 시간에서 잘립니다.

기본 처리는 Date 차원 테이블을 채우는 것으로 시작합니다. 처리는 현재 연도의 모든 날짜가 테이블에 채워졌도록 합니다.

다음으로 일련의 데이터 흐름 작업이 각 차원을 로드합니다. 그런 다음 각 팩트를 로드합니다.

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server 2016(또는 그 이상) 와이드월드Importers 및 와이드월드ImportersDW 데이터베이스(SQL Server의 동일또는 다른 인스턴스)에서
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 통합 서비스 카탈로그를 만들어야 합니다. 통합 서비스 카탈로그를 만들려면 SQL Server 관리 스튜디오 개체 탐색기에서 **통합 서비스를**마우스 오른쪽 단추로 클릭한 다음 **카탈로그 추가를**선택합니다. 기본 옵션을 그대로 둡니다. SQLCLR을 사용하도록 설정하고 암호를 제공하라는 메시지가 표시됩니다.


## <a name="download"></a>다운로드

샘플의 최신 릴리스는 [전 세계 수입업체 릴리스를](https://go.microsoft.com/fwlink/?LinkID=800630)참조하십시오. 일일 *ETL.ispac* 통합 서비스 패키지 파일을 다운로드하십시오.

소스 코드가 샘플 데이터베이스를 다시 만들려면 [와이드 월드 가져오기](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis)를 참조하십시오.

## <a name="install"></a>설치

1. 통합 서비스 패키지 배포:
   1. Windows 탐색기에서 *일일 ETL.ispac* 패키지를 엽니다. 그러면 SQL 서버 통합 서비스 배포 마법사가 시작됩니다.
   2. **소스 선택에서** *일일 ETL.ispac* 패키지를 가리키는 경로와 함께 프로젝트 배포의 기본값을 따릅니다.
   3. **대상 선택**에서 통합 서비스 카탈로그를 호스트 하는 서버의 이름을 입력합니다.
   4. 예를 들어 *와이드월드인더스*라는 새 폴더에서 통합 서비스 카탈로그 에서 경로를 선택합니다.
   5. 마법사를 완료하려면 **배포를** 선택합니다.

2. ETL 프로세스에 대한 SQL 서버 에이전트 작업 만들기:
   1. 관리 스튜디오에서 **SQL 서버 에이전트를**마우스 오른쪽 단추로 클릭한 다음 **새** > **작업을**선택합니다.
   2. 예를 *들어, 와이드월드인더ETL의 이름을 입력합니다.*
   3. SQL Server 통합 서비스 패키지 형식의 **작업 단계를** **추가합니다.**
   4. 통합 서비스 카탈로그가 있는 서버를 선택한 다음 *일일 ETL* 패키지를 선택합니다.
   5. **구성** > **연결 관리자에서**원본 및 대상에 대한 연결이 올바르게 구성되었는지 확인합니다. 기본값은 로컬 인스턴스에 연결하는 것입니다.
   6. 작업을 만들려면 **확인을** 선택합니다.

3. 작업을 실행하거나 예약합니다.
