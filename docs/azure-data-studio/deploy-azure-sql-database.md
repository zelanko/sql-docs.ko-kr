---
title: Notebook을 통해 Azure SQL Database 배포
description: 이 자습서에서는 Azure SQL Database를 만드는 방법을 보여 줍니다.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, markingmyname
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/16/2020
ms.openlocfilehash: 5b68bda566bdd28c8dd2e70f036dd8e17643f776
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155024"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Azure Data Studio를 사용하여 Azure SQL Database 만들기

배포 마법사 및 Notebook을 통해 Azure Data Studio를 사용하여 Azure SQL Database를 만들 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

 - [Azure Data Studio](download-azure-data-studio.md)가 설치되어 있음
 - 활성 Azure 계정 및 구독. 아직 Azure 구독이 없는 경우 [무료 계정을 만듭니다](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>배포 마법사 사용

간단한 UI 환경에서 필요한 설정을 안내하는 배포 마법사를 사용하려면 다음 단계를 수행합니다.

먼저 배포 마법사에서 Azure SQL Database를 찾아 선택합니다.

 1. Azure Data Studio에서 왼쪽 탐색에 있는 연결 뷰렛을 선택합니다.
 2. 연결 패널 맨 위에 있는 **...** 단추를 선택하고 **새 배포...** 를 선택합니다.
 3. 배포 마법사에서 **Azure SQL Database** 타일을 선택하고 동의함 확인란을 선택합니다.
 4. 리소스 종류 드롭다운에서 만들려는 항목(데이터베이스, 데이터베이스 서버 또는 탄력적 풀)을 선택합니다. Azure에 SQL 데이터베이스가 없는 경우 먼저 데이터베이스를 만드는 것이 좋습니다.
 5. 서버 또는 풀을 만들도록 선택한 경우 **Azure Portal에서 만들기**를 선택하고, 데이터베이스를 만들도록 선택한 경우 **선택**을 선택합니다.

데이터베이스를 만들도록 선택한 경우 아래 단계를 수행합니다.

 1. 아직 Azure 계정에 로그인하지 않은 경우 로그인합니다. 이 마법사 페이지에 문제가 있는 경우 연결을 새로 고칠 수 있습니다.
 2. 원하는 구독과 서버를 선택합니다. 그런 후 **다음**을 선택합니다.
 3. 데이터베이스 이름을 입력합니다.
 4. 방화벽 규칙 이름과 Azure Data Studio를 실행하는 로컬 클라이언트 머신의 IP 범위를 입력합니다. 생성된 후 바로 ADS에서 서버 및 데이터베이스에 연결할 수 있도록 하기 위한 과정입니다.
 5. **다음**을 선택합니다.
 6. 입력한 매개 변수를 검토한 후 **Notebook으로 스크립트**를 선택합니다.

Notebook이 열리면 콘텐츠와 코드를 검토하고 원하는 경우 변경할 수 있습니다. 특히, 특정 성능 또는 비용 기본 설정이 있는 경우에는 기본값에서 컴퓨팅 및 스토리지 설정을 변경할 수 있습니다. 그러나 Notebook에서 변경한 내용이 있으면 유효성 검사 오류가 발생할 수 있습니다.

마지막 단계는 **모두 실행**을 선택하여 Notebook의 모든 셀을 실행하는 것입니다. 이 작업이 완료되면 ADS에 연결하고 ADS에서 쿼리할 수 있는 완전히 생성되고 실행 중인 SQL Database가 생깁니다.

## <a name="next-steps"></a>다음 단계

데이터베이스, 서버 또는 풀을 만든 후 Azure Data Studio에서 데이터베이스에 [연결하여 쿼리](quickstart-sql-database.md)할 수 있습니다.
