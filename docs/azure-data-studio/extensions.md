---
title: 확장 추가
titleSuffix: Azure Data Studio
description: 확장 Marketplace에서 Azure Data Studio로 확장 추가
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 10/03/2019
ms.openlocfilehash: 6f0a2ab021873a2a9414bfbcdb7aed63c2d31056
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72166725"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기능 확장

[!INCLUDE[name-sos](../includes/name-sos-short.md)]의 확장을 사용하면 기본 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설치에 더 많은 기능을 쉽게 추가할 수 있습니다. 

확장은 Azure Data Studio 팀(Microsoft) 및 타사 커뮤니티(사용자)가 제공합니다. 확장을 만드는 방법에 대한 자세한 내용은 [확장 작성](extension-authoring.md)을 참조하세요.


## <a name="add-azure-data-studio-extensions"></a>Azure Data Studio 확장 추가

1. 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택하여 사용 가능한 확장에 액세스합니다.

    ![확장 관리자 아이콘](media/extensions/extension-manager-icon.png)

    `Ctrl+Shift+X`(Windows/Linux) 또는 `Command+Shift+X`(Mac)를 눌러 확장 관리자에 신속하게 액세스할 수도 있습니다.

2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.
    ![확장 정보](media/extensions/extension-details.png)

3. 원하는 확장을 선택하고 **설치**합니다.

4. 설치가 완료되면 확장을 **다시 로드하여** Azure Data Studio에서 사용하도록 설정합니다(확장을 처음 설치하는 경우에만 필요).

Azure Data Studio에서 확장 관리자에 액세스하는 데 문제가 있는 경우 [GitHub Wiki](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions)에서 필요한 확장을 다운로드할 수 있습니다.


## <a name="access-installed-azure-data-studio-extensions"></a>설치된 Azure Data Studio 확장 액세스

각 확장은 다른 방식으로 Azure Data Studio의 작업 환경을 향상시킵니다. 따라서 확장의 진입점은 다를 수 있습니다. 설치한 후 확장의 기능에 액세스하는 방법에 대한 내용은 설치된 확장의 개별 설명서를 참조하세요.
