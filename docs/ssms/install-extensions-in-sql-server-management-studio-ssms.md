---
description: SSMS(SQL Server Management Studio)에서 확장 설치
title: SSMS(SQL Server Management Studio)에서 확장 설치
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- 확장
- vsix
- 확장 설치
- vsix 설치
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 07/29/2020
ms.openlocfilehash: bf4c9ee5287a2e0fdecf8455334561ce130499bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492053"
---
# <a name="install-extensions-in-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)에서 확장 설치

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

SSMS(SQL Server Management Studio) 확장은 C#을 사용하여 Visual Studio의 "Visual Studio 확장 개발" 워크로드를 통해 생성됩니다. SSMS 18.x는 Visual Studio 2017 셸을 기반으로 하며 해당 환경의 제한 사항이 적용됩니다.

SSMS 18.x에서는 Visual Studio 또는 독립적인 관리되는 패키지 설치 관리자를 통해 VSIX를 배포하여 확장을 설치할 수 있습니다.  Visual Studio 배포에 대해서는 아래에서 설명합니다.

> [!NOTE]
> SQL Server Management Studio 확장은 SSMS 18.x의 VSIXInstaller를 통해 설치할 수 없습니다.
  
## <a name="visual-studio-deployment-of-an-extension-for-ssms-18x"></a>SSMS 18.x용 확장의 Visual Studio 배포

수동으로 확장을 설치하려면 연결된 확장 파일(VSIX)을 기본 SSMS 확장 폴더에 복사합니다.  SSMS는 시작 시 이 폴더에서 확장을 자동으로 확인합니다.  VSIX 배포는 프로젝트 빌드 시 Visual Studio에서 완료할 수 있습니다. 

  
1.  SSMS 설치 및 기본 확장 폴더를 찾습니다.  기본 SSMS 설치 설정에서는 폴더 위치가 ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\```입니다.  


2. 관리자 권한으로 Visual Studio를 시작합니다.

3.  프로젝트 속성 창의 VSIX 탭에서 "VSIX 콘텐츠를 다음 위치에 복사" 확인란을 선택하면 빌드 시 Visual Studio에서 파일 복사 프로세스를 완료할 수 있습니다. 확인란 아래의 텍스트 상자에 위의 폴더 위치에 이 확장의 폴더를 추가한 경로를 입력합니다.  ```C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\Extensions\SampleExtension```
  
![3개의 확인란과 1개의 텍스트 상자가 있는 프로젝트 속성 창 VSIX 설정](./media/install-extensions/vsix_ssms.png)

4. 확장 프로젝트를 빌드합니다. 빌드에 성공하면 확장 파일이 SSMS 확장 폴더로 전송됩니다.

5.  SSMS를 실행하고 확장의 기능을 테스트합니다.
  
