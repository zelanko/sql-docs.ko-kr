---
title: SQL Server dacpac 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio용 SQL Server dacpac 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 10/21/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 769e6157e7d84702716dfce79d0217efeee83076
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783319"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 확장(미리 보기)

**데이터 계층 애플리케이션 마법사** 는 dacpac 파일을 배포 및 추출하고 bacpac 파일을 가져오고 내보내기 위한 간편한 마법사 환경을 제공합니다.

이 환경은 현재 최초 미리 보기로 제공됩니다. [여기](https://github.com/microsoft/azuredatastudio/issues)서 문제 및 기능 요청을 보고하세요.


## <a name="features"></a>기능

* SQL Server 인스턴스에 dacpac 배포
* dacpac으로 SQL Server 인스턴스 추출
* bacpac에서 데이터베이스 만들기
* 스키마 및 데이터를 bacpac으로 내보내기

![dacpac 확장 데모 gif](media/extensions/sql-server-dacpac-extension/dacpac-extension-demo.gif)


## <a name="why-would-i-use-the-data-tier-application-wizard"></a>데이터 계층 애플리케이션 마법사를 사용해야 하는 이유

마법사를 사용하면 dacpac 및 bacpac 파일을 보다 쉽게 관리할 수 있으므로 애플리케이션을 지원하는 데이터 계층 요소를 간편하게 개발하고 배포할 수 있습니다. 데이터 계층 애플리케이션을 사용하는 방법에 대해 자세히 알아보려면 [설명서](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)를 참조하세요.


## <a name="install-the-extension"></a>확장 설치

1. 확장 아이콘을 선택하여 사용 가능한 확장을 표시합니다.

    ![확장 관리자 아이콘](media/extensions/extension-manager-icon.png)

2. **SQL Server dacpac** 확장을 검색하고 선택하여 세부 정보를 확인합니다. **설치**를 클릭하여 확장을 추가합니다.

3. 설치가 완료되면 확장을 **다시 로드하여** Azure Data Studio에서 사용하도록 설정합니다(확장을 처음 설치하는 경우에만 필요).


## <a name="launch-the-data-tier-application-wizard"></a>데이터 계층 애플리케이션 마법사 시작

마법사를 시작하려면 Databases 폴더를 마우스 오른쪽 단추로 클릭하거나 개체 탐색기에서 특정 데이터베이스를 마우스 오른쪽 단추로 클릭합니다. 그런 다음 **데이터 계층 애플리케이션 마법사**를 클릭합니다.

![dacpac 확장 시작 메뉴](media/extensions/sql-server-dacpac-extension/dacpac-extension-launch.png)


## <a name="next-steps"></a>다음 단계

dacpac에 대한 자세한 내용은 [설명서](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)를 참조하세요.