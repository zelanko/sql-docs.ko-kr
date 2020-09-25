---
title: SQL Server 중앙 관리 서버 확장
description: SQL Server 중앙 관리 서버 확장을 설치하고 사용하는 방법을 알아봅니다. 서버를 그룹화하고 그룹에 작업을 적용하기 위한 확장입니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/06/2019
ms.openlocfilehash: ca200de903675da9fdfbd2549d3ee1b5bd192907
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123269"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>SQL Server 중앙 관리 서버 확장(미리 보기)

중앙 관리 서버 확장을 사용하면 사용자가 하나 이상으로 구성된 SQL Server 인스턴스 목록을 저장할 수 있습니다. CMS 그룹을 사용하여 수행되는 동작은 서버 그룹의 모든 서버에서 적용됩니다.

이 환경은 현재 최초 미리 보기로 제공됩니다. [여기](https://github.com/microsoft/azuredatastudio/issues)서 문제 및 기능 요청을 보고하세요.

![CMS 확장](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>SQL Server 중앙 관리 서버 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.
3. 원하는 확장(SQL Server 중앙 관리 서버)을 선택하고 **설치**합니다.

### <a name="how-do-i-start-central-management-servers"></a>중앙 관리 서버를 어떻게 시작하나요?

 중앙 관리 서버는 연결 아이콘(Ctrl/Cmd + G)을 클릭하여 볼 수 있습니다. 확장을 처음 다운로드하면 CMS 보기가 최소화되며 **중앙 관리 서버**를 클릭하여 열 수 있습니다.

## <a name="next-steps"></a>다음 단계

중앙 관리 서버를 개념적으로 자세히 알아보려면 [여기를 참조하세요.](../../ssms/register-servers/create-a-central-management-server-and-server-group.md)