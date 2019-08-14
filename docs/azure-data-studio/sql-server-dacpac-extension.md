---
title: SQL Server dacpac 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio용 SQL Server dacpac 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959195"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 확장(미리 보기)

**데이터 계층 애플리케이션 마법사**는 .dacpac 파일을 배포 및 추출하고 .bacpac 파일을 가져오고 내보내기 위한 간편한 환경을 제공합니다.

이 환경은 현재 최초 미리 보기로 제공됩니다. [여기](https://github.com/microsoft/azuredatastudio/issues)서 문제 및 기능 요청을 보고하세요.

![데이터 작업](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>요구 사항
 * 이 마법사를 시작하려면 SQL Server 인스턴스에 대한 활성 연결이 필요합니다.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>데이터 계층 애플리케이션 마법사를 시작하는 방법
 * 마법사의 주 진입점은 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **데이터 계층 애플리케이션 마법사**를 클릭하는 것입니다.
 * SQL Server 인스턴스에 연결된 사용자는 **데이터 계층 애플리케이션 마법사**를 검색하여 명령 팔레트(Ctrl+Shift+P)에서 마법사를 시작할 수도 있습니다.

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>데이터 계층 애플리케이션 마법사를 사용해야 하는 이유
 이 마법사는 .dacpac 파일을 추출 및 배포하고 Azure Data Studio에서 .bacpac 파일을 가져오고 내보내는 기능을 추가하기 위해 만든 것입니다.

## <a name="install-the-sql-server-dacpac-extension"></a>SQL Server dacpac 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. SQL Server dacpac 확장을 선택하고 **설치**를 클릭합니다.
1. **다시 로드**를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).
2. 서버 또는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **관리**를 선택하여 관리 대시보드로 이동합니다.
3. 설치된 확장은 관리 대시보드에 탭으로 표시됩니다.

## <a name="next-steps"></a>다음 단계

dacpac에 대한 자세한 내용은 [설명서](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)를 참조하세요.