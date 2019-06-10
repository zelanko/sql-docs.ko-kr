---
title: SQL Server dacpac 확장
titleSuffix: Azure Data Studio
description: 설치 하 고 Azure Data Studio 용 SQL Server dacpac 확장 (미리 보기) 사용
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 70b06749d1cbecc2127c70fee28b60f49583d5ce
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797990"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 확장(미리 보기)

**데이터 계층 응용 프로그램 마법사** 배포 및.dacpac 파일을 추출 하 고 가져올.bacpac 파일 내보내기에 사용 하기 쉬운 환경을 제공 합니다.

이 환경은 현재 초기 미리 보기 중입니다. 문제를 보고 하 고 기능 요청 하십시오 [여기 있습니다.](https://github.com/microsoft/azuredatastudio/issues)

![data-actions](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>요구 사항
 * 이 마법사는 SQL Server 인스턴스를 시작 하는 활성 연결이 필요 합니다.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>데이터 계층 응용 프로그램 마법사를 시작 하려면 어떻게 해야 하나요?
 * 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 클릭 하는 마법사에 대 한 주 진입점 **데이터 계층 응용 프로그램 마법사**합니다.
 * 사용자는 SQL Server 인스턴스에 연결 되어 사용자도 마법사를 시작할 수 명령 팔레트 (Ctrl + Shift + P)에서 검색 하 여 **데이터 계층 응용 프로그램 마법사.**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>데이터 계층 응용 프로그램 마법사를 왜 사용 해야 합니까?
 추출 및.dacpac 파일 배포, 가져오기 및 Azure Data Studio에.bacpac 파일 내보내기 하는 기능을 추가 하려면이 마법사를 만들었습니다.

## <a name="install-the-sql-server-dacpac-extension"></a>SQL Server dacpac 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스를 하려면 확장 아이콘을 선택 하거나 선택 **Extensions** 에 **보기** 메뉴.
2. SQL Server dacpac 확장을 선택 하 고 클릭 **설치**합니다.
1. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.
2. 서버 또는 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 관리 대시보드로 이동 **관리**합니다.
3. 설치 된 확장 관리 대시보드에서 탭으로 나타납니다.

## <a name="next-steps"></a>다음 단계

Dacpac에 대 한 자세한 내용은 [설명서를 확인 합니다.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)