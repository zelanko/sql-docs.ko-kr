---
title: Notebook을 통해 Azure SQL Database 배포
description: 이 자습서에서는 Azure SQL Database를 만드는 방법을 보여 줍니다.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060918"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Azure Data Studio를 사용하여 Azure SQL Database 만들기

배포 마법사 및 Notebook을 통해 Azure Data Studio를 사용하여 Azure SQL Database를 만들 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

 - [Azure Data Studio](download-azure-data-studio.md)가 설치되어 있음
 - 활성 Azure 계정 및 구독. 아직 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.

## <a name="use-the-deployment-wizard"></a>배포 마법사 사용

간단한 UI 환경에서 필요한 설정을 안내하는 배포 마법사를 사용하려면 다음 단계를 수행합니다.

먼저 배포 마법사에서 Azure SQL Database를 찾아 선택합니다.

 1. Azure Data Studio에서 왼쪽 탐색에 있는 연결 뷰렛을 선택합니다.
 2. 연결 패널 맨 위에 있는 **...** 단추를 선택하고 **새 배포...** 를 선택합니다.
 3. 배포 마법사에서 **Azure SQL Database** 타일을 선택하고 동의함 확인란을 선택합니다.
 4. 리소스 종류 드롭다운에서 만들려는 항목(데이터베이스, 데이터베이스 서버 또는 탄력적 풀)을 선택합니다. Azure에 SQL Database가 없는 경우 데이터베이스부터 만드는 것이 좋습니다.
 5. **Azure Portal에서 만들기**를 선택합니다.

데이터베이스, 서버 또는 풀을 만드는 데 필요한 모든 기본 설정을 입력합니다. 해당 설정을 구성하는 방법에 대한 몇 가지 지침은 [Azure SQL 설명서](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal)에서 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

데이터베이스, 서버 또는 풀을 만든 후 Azure Data Studio에서 데이터베이스에 [연결하여 쿼리](quickstart-sql-database.md)할 수 있습니다.
