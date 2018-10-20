---
title: Azure Data Studio에 대 한 확장 프로그램을 만들어 | Microsoft Docs
description: Azure Data Studio에 확장 추가
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7d778eb4df52d28a44ec8127ebc9f657a9f0dde
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355885"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>기능을 확장 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

확장 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 자료에 기능을 추가 하는 쉬운 방법을 제공 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설치 합니다.

확장 (있습니다!) 타사 당사자 커뮤니티와 Azure Data Studio 팀 (Microsoft)에서 제공 됩니다.


## <a name="author-an-extension"></a>확장 작성

Azure Data Studio를 확장 하려는 경우 사용자 고유의 확장 만들고 확장 갤러리에 게시할 수 있습니다.

**확장 작성**

***필수 구성 요소***

확장을 개발 하려면 설치 하 고 프로그램 $PATH에서 사용할 수 있는 Node.js 필요 합니다. Node.js npm, 확장 생성기를 설치 하는 데 사용할 Node.js 패키지 관리자를 포함 합니다.

새 확장 프로그램을 시작 하려면 Azure 데이터 Studio 확장 생성기를 사용할 수 있습니다. Yeoman [확장 생성기](https://www.npmjs.com/package/generator-sqlops) 매우 쉽게 단순 확장 프로젝트를 만들 수 있도록 합니다. 생성기를 시작 하려면 명령 프롬프트에서 다음을 입력 합니다.

`npm install -g yo generator-sqlops`

`yo sqlops`


**확장성 참조**

Azure 데이터 Studio 확장성 참조에 대해 자세히 알아보려면 [확장성 개요](extensibility.md)합니다. 또한 기존 API를 사용 하는 방법의 예제를 볼 수 있습니다 [샘플](https://github.com/Microsoft/azuredatastudio/tree/master/samples)합니다.


## <a name="debug-an-extension"></a>확장 디버그

Visual Studio Code 확장을 사용 하 여 새 확장 프로그램을 디버깅할 수 있습니다 [Azure 데이터 Studio 디버그](https://github.com/kevcunnane/sqlops-debug)합니다.

단계
- 사용 하 여 확장 프로그램을 열고 [Visual Studio Code](https://code.visualstudio.com/)
- Azure 데이터 Studio 디버그 확장 설치
- 키를 눌러 **F5** 또는 디버그 아이콘을 클릭 하 고 클릭 **시작**합니다.
- Azure Data Studio의 새 인스턴스를 특수 모드 (확장 개발 호스트)에서 시작 하 고이 새 인스턴스를 확장 프로그램의 인식 이제 키를 누릅니다.


## <a name="create-an-extension-package"></a>확장 패키지를 만듭니다

확장 프로그램을 작성 한 후 Azure Data Studio에 설치 하려면 VSIX 패키지를 만들 해야 합니다. 사용할 수 있습니다 [vsce](https://github.com/Microsoft/vscode-vsce) VSIX 패키지를 만듭니다.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>확장 게시

Azure Data Studio에 새 확장 프로그램을 게시할:

1. 사용자 지정 확장을 추가 합니다. https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 에서는 현재 없는 호스트 타사 확장을 지원 하므로 확장을 다운로드 하는 대신 Azure Data Studio에 다운로드 페이지로 이동 하는 옵션입니다. 확장 프로그램에 대 한 다운로드 페이지를 설정 하려면 "Microsoft.AzureDataStudio.DownloadPage" 자산의 값을 설정 합니다.
3. 릴리스/확장 지점에 대 한 PR을 만듭니다.
4. 팀에 검토 요청을 보냅니다.

확장 프로그램을 검토 하 고 확장 갤러리에 추가 됩니다.

**확장 업데이트를 게시** 업데이트를 게시 하는 프로세스를 확장 게시 비슷합니다. Package.json에서 버전이 업데이트 되 고 있는지 확인 하십시오
