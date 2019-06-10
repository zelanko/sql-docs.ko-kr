---
title: Azure 리소스 탐색기를 사용 하 여 Azure SQL 리소스 탐색
titleSuffix: Azure Data Studio
description: 탐색 및 Azure SQL Server, Azure SQL Database 및 Azure Resource Explorer를 통해 Azure SQL 관리 되는 인스턴스를 관리 하는 방법에 알아봅니다.
ms.custom: seodec18
author: yanancai
ms.author: yanacai
manager: jroth
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: 91e766fae5dca7a3d9e2dec56af17161d684e145
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66789219"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>탐색 및 Azure 리소스 탐색기를 사용 하 여 Azure SQL 리소스 관리

탐색 하 고 Azure SQL Server, Azure SQL database 및 Azure SQL 관리 되는 인스턴스 리소스에서 Azure Resource Explorer를 통해 관리할 수는 방법을 알아보려면이 문서에서는 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]합니다.

>[!NOTE]
>Azure Resource Explorer는 SQL Server 2019 년 10 월 미리 보기에서 지원 됩니다. 그런 다음을 통해 미리 보기 확장을 설치할 수 있습니다 [확장 관리자](extensions.md) 를 통해 **파일** > **VSIX 패키지에서 패키지 설치**합니다.


## <a name="connect-to-azure"></a>Azure에 연결

SQL 미리 보기 플러그 인을 설치한 후 왼쪽된 메뉴 모음에 Azure 아이콘이 나타납니다. Azure Resource Explorer를 열려면 아이콘을 클릭 합니다. Azure 아이콘에 표시 되지 않으면 왼쪽된 메뉴 모음을 마우스 오른쪽 단추로 클릭 하 고 선택 **Azure Resource Explorer**합니다.

### <a name="add-an-azure-account"></a>Azure 계정 추가

Azure 계정과 연결 된 SQL 리소스를 보려면 먼저 추가 해야 계정을 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]합니다.

1. 오픈 **연결 된 계정** 대화 상자 왼쪽된 아래에서 나를 통해 계정 관리 아이콘을 통해 **Azure에 로그인 하는 중...**  Azure 리소스 탐색기에 링크 합니다.

    ![Azure에 로그인](media/azure-resource-explorer/sign-in-to-azure.png)

2. 에 **연결 된 계정** 대화 상자에서 클릭 **계정 추가**합니다.

    ![Azure 계정 추가](media/azure-resource-explorer/add-an-azure-account.png)

3. 클릭 **복사 하 고 엽니다** 인증에 대 한 브라우저를 엽니다.

    ![브라우저에서 공개 인증 페이지](media/azure-resource-explorer/open-authentication-in-browser.png)

4. 붙여넣기 합니다 **사용자 코드** 웹 페이지를 클릭 **계속** 인증할 수 있습니다.

    ![브라우저에서 인증](media/azure-resource-explorer/authenticate-in-browser.png)

5. [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] 이제 찾아야 로그인에 Azure 계정의 **연결 된 계정** 대화 합니다.

    ![Azure 계정에 로그인](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>더 많은 Azure 계정 추가

여러 Azure 계정에서 지원 됩니다 [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]합니다. 더 많은 Azure 계정에 추가 하려면의 오른쪽 상단에 있는 단추를 클릭 **연결 된 계정** 대화 상자와 동일한 단계에 따라 사용 하 여 더 많은 Azure 계정을 추가 하려면 Azure 계정 섹션을 추가 합니다.

![더 많은 Azure 계정 추가](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Azure 계정 제거

에 기존 Azure 계정 로그인을 제거 합니다.

1. 오픈 **연결 된 계정** 대화 상자 왼쪽된 아래에 있는 계정 관리 아이콘입니다.
2. 클릭 합니다 **X** 제거 하려면 Azure 계정의 오른쪽에 있는 단추입니다.

    ![Azure 계정 제거](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>구독 필터링

Azure 계정에 로그인 한 모든 구독 연관 된 Azure 리소스 탐색기에서를 표시 하는 Azure 계정. 각 Azure 계정에 대 한 구독을 필터링 할 수 있습니다.

1. 클릭 합니다 **구독 선택** Azure 계정의 오른쪽에 있는 단추입니다.

   ![구독 필터링](media/azure-resource-explorer/filter-subscription.png)

2. 찾은 다음 클릭 하려는 계정 구독에 대 한 확인란을 선택 **확인**합니다.

   ![구독 선택](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Azure SQL 리소스 탐색

Azure 리소스 탐색기에서 Azure SQL 리소스를 탐색 하는 Azure 계정 및 리소스 형식 그룹을 확장 합니다.

Azure 리소스 탐색기는 Azure SQL Server, Azure SQL Database 및 Azure SQL 관리 되는 인스턴스를 현재 지원합니다.

## <a name="connect-to-azure-sql-resources"></a>Azure SQL 리소스에 연결

Azure 리소스 탐색기는 SQL 서버와 쿼리 및 관리에 대 한 데이터베이스에 연결할 수 있는 빠른 액세스를 제공 합니다. 

1. 트리 보기에서 사용 하 여 연결 하려는 SQL 리소스를 탐색 합니다.
2. 선택한 리소스를 마우스 오른쪽 단추로 클릭 **Connect**, 리소스의 오른쪽에 있는 연결 단추를 찾을 수도 있습니다.

   ![Azure SQL 리소스에 연결](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. 열린 **연결** 대화 상자에서 암호를 입력 하 고 클릭 **Connect**합니다.

   ![SQL 연결 대화 상자](media/azure-resource-explorer/sql-connection-dialog.png)
4. 합니다 **서버** 창이 새 연결 된 SQL server/database와 연결에 성공한 후 자동으로 열립니다.

## <a name="next-steps"></a>다음 단계

- [사용 하 여 [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] 를 연결 하 여 Azure SQL database 쿼리](quickstart-sql-database.md)
- [사용 하 여 [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] 연결 하 고 Azure SQL Data Warehouse에서 데이터를 쿼리 합니다.](quickstart-sql-dw.md)