---
title: Azure Resource Explorer를 사용하여 Azure SQL 리소스 살펴보기
titleSuffix: Azure Data Studio
description: Azure Resource Explorer를 통해 Azure SQL Server, Azure SQL Database 및 Azure SQL Managed Instance를 살펴보고 관리하는 방법을 알아봅니다.
ms.custom: seodec18
author: yanancai
ms.author: yanacai
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.date: 09/24/2018
ms.openlocfilehash: 2a1f62ed9266b0575f037dfe9541a026a4c1ed29
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73801141"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>Azure Resource Explorer를 사용하여 Azure SQL 리소스 살펴보기 및 관리

이 문서에서는 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]에서 Azure Resource Explorer를 통해 Azure SQL Server, Azure SQL Database 및 Azure SQL Managed Instance 리소스를 살펴보고 관리하는 방법을 알아봅니다.

>[!NOTE]
>Azure Resource Explorer는 SQL Server 2019에서 지원됩니다. 그런 다음, [확장 관리자](extensions.md) 또는 **파일** > **VSIX 패키지에서 파일 설치**를 통해 확장을 설치할 수 있습니다.

## <a name="connect-to-azure"></a>Azure에 연결

SQL 플러그 인을 설치하면 왼쪽 메뉴 모음에 Azure 아이콘이 표시됩니다. 이 아이콘을 클릭하여 Azure Resource Explorer를 엽니다. Azure 아이콘이 표시되지 않으면 왼쪽 메뉴 모음을 마우스 오른쪽 단추로 클릭하고 **Azure Resource Explorer**를 선택합니다.

### <a name="add-an-azure-account"></a>Azure 계정 추가

Azure 계정과 연결된 SQL 리소스를 보려면 먼저 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]에 계정을 추가해야 합니다.

1. 왼쪽 아래의 계정 관리 아이콘 또는 Azure Resource Explorer의 **Azure에 로그인...** 링크를 통해 **연결된 계정** 대화 상자를 엽니다.

    ![Azure에 로그인](media/azure-resource-explorer/sign-in-to-azure.png)

2. **연결된 계정** 대화 상자에서 **계정 추가**를 클릭합니다.

    ![Azure 계정 추가](media/azure-resource-explorer/add-an-azure-account.png)

3. **복사 및 열기**를 클릭하여 인증을 위해 브라우저를 엽니다.

    ![브라우저에서 인증 페이지 열기](media/azure-resource-explorer/open-authentication-in-browser.png)

4. 웹 페이지에 **사용자 코드**를 붙여넣고 **계속**을 클릭하여 인증을 받습니다.

    ![브라우저에서 인증](media/azure-resource-explorer/authenticate-in-browser.png)

5. 이제 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]의 **연결된 계정** 대화 상자에서 로그인한 Azure 계정을 찾을 수 있습니다.

    ![로그인한 Azure 계정](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>더 많은 Azure 계정 추가

[!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]에서는 여러 Azure 계정이 지원됩니다. Azure 계정을 더 추가하려면 **연결된 계정** 대화 상자의 오른쪽 상단에 있는 단추를 클릭하고 Azure 계정 추가 섹션의 동일한 단계를 수행하여 더 많은 Azure 계정을 추가합니다.

![더 많은 Azure 계정 추가](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Azure 계정 제거

기존에 로그인한 Azure 계정을 제거하려면

1. 왼쪽 하단의 계정 관리 아이콘을 통해 **연결된 계정** 대화 상자를 엽니다.
2. Azure 계정 오른쪽의 **X** 단추를 클릭하여 제거합니다.

    ![Azure 계정 제거](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>구독 필터링

Azure 계정에 로그인하면 해당 Azure 계정과 연결된 모든 구독이 Azure Resource Explorer에 표시됩니다. 각 Azure 계정에 대한 구독을 필터링할 수 있습니다.

1. Azure 계정 오른쪽에 있는 **구독 선택** 단추를 클릭합니다.

   ![구독 필터링](media/azure-resource-explorer/filter-subscription.png)

2. 검색하려는 계정 구독의 확인란을 선택하고 **확인**을 클릭합니다.

   ![구독 선택](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Azure SQL 리소스 살펴보기

Azure Resource Explorer에서 Azure SQL 리소스를 살펴보려면 Azure 계정 및 리소스 유형 그룹을 확장합니다.

Azure Resource Explorer는 현재, Azure SQL Server, Azure SQL Database 및 Azure SQL Managed Instance를 지원합니다.

## <a name="connect-to-azure-sql-resources"></a>Azure SQL 리소스에 연결

Azure Resource Explorer는 쿼리 및 관리를 위해 SQL Server 및 데이터베이스에 연결하는 데 도움이 되는 빠른 액세스를 제공합니다.

1. 트리 보기에서 연결하려는 SQL 리소스를 찾습니다.
2. 리소스를 마우스 오른쪽 단추로 클릭하고 **연결**을 선택하여 리소스의 오른쪽에 있는 연결 단추를 찾을 수도 있습니다.

   ![Azure SQL 리소스에 연결](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 열린 **연결** 대화 상자에서 암호를 입력하고 **연결**을 클릭합니다.

   ![SQL 연결 대화 상자](media/azure-resource-explorer/sql-connection-dialog.png)
4. 연결이 성공하면 **서버** 창이 자동으로 열리고 새로 연결된 SQL Server/Database가 표시됩니다.

## <a name="next-steps"></a>다음 단계

- [[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)
- [[!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)]를 사용하여 Azure SQL Data Warehouse에서 데이터 연결 및 쿼리](quickstart-sql-dw.md)