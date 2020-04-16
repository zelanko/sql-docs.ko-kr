---
title: SQL Server Notebook 관리
description: Azure Data Studio에서 Notebook을 관리하는 방법을 알아봅니다. 여기에는 Notebook 열기, Notebook 저장, 빅 데이터 클러스터 연결 변경이 포함됩니다.
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531596"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Azure Data Studio에서 Notebook을 관리하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server를 사용하여 Azure Data Studio에서 Notebook 파일을 열고 저장하는 방법을 보여 줍니다. SQL Server 연결을 변경하는 방법도 보여 줍니다.

## <a name="open-a-notebook"></a>Notebook 열기

**Notebook 열기** 대화 상자를 여는 방법에는 여러 가지가 있습니다. 파일 메뉴, 대시보드 및 명령 팔레트를 사용할 수 있습니다. 다음 섹션에서는 각 방법을 설명합니다.

### <a name="file-menu"></a>파일 메뉴

파일 메뉴에서 **파일 열기**를 선택합니다(Windows의 경우 Ctrl+O, Mac의 경우 Cmd+O).

![파일 열기를 선택하여 파일 열기 대화 상자 열기](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>대시보드

대시보드에서 **Notebook 열기**를 클릭하여 파일 열기 대화 상자를 엽니다.

![대시보드에서 Notebook 열기를 선택하여 파일 열기 대화 상자 열기](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>명령 팔레트

명령 팔레트에서 Ctrl+Shift+P(Windows) 및 Cmd+Shift+P(Mac)를 입력하여 **파일: 열기** 명령을 사용합니다.

![명령 팔레트에서 파일: 열기를 입력하여 파일 열기 대화 상자 열기](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>Notebook 저장

현재 Notebook을 저장하는 방법은 하나뿐입니다. Notebook 도구 모음에서 **저장**을 선택합니다.

![Notebook 도구 모음에서 저장을 선택하여 파일 저장](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> 현재 다음 방법은 Notebook에 변경 내용을 저장하지 않습니다.
>
> - 파일 메뉴의 **파일 저장**, **다른 이름으로 파일 저장...** 및 **파일 모두 저장**
> - 명령 팔레트에서 입력한 **파일: 저장** 명령을 입력하여 Notebook을 저장할 수 있습니다.

## <a name="change-the-connection"></a>연결 변경

Notebook 연결을 변경하려면 다음을 수행합니다.

1. Notebook 도구 모음에서 **연결 대상** 메뉴를 선택하고 **연결 변경**을 선택합니다.

   ![Notebook 도구 모음에서 연결 대상 메뉴 클릭](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. 이제 최근 연결 서버를 선택하거나 새 연결 정보를 입력하여 연결할 수 있습니다.

   ![연결 대상 메뉴에서 서버 선택](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>다음 단계

Azure Data Studio의 Notebooks에 대한 자세한 내용은 [SQL Server 2019에서 Notebooks를 사용하는 방법](notebooks-guidance.md)을 참조하세요.
