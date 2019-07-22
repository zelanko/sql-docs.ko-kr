---
title: '방법: 기능 확장 설치 및 관리 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9cdc8cd5-c36f-4bee-a191-87ed457803e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a7d2f4fa27623a75bd49a32a7ce800801f63e9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929599"
---
# <a name="how-to-install-and-manage-feature-extensions"></a>방법: 기능 확장 설치 및 관리
데이터베이스 코드를 분석하기 위한 규칙, 데이터베이스 단위 테스트의 조건 및 빌드/배포 참가자를 추가하여 SQL Server Data Tools가 포함된 Visual Studio 버전에서 제공하는 기능을 늘릴 수 있습니다. 그러나 사용자가 확장을 만들었든지 다른 사람이 만든 확장을 설치하려는 것이든지 관계없이 기능 확장을 사용하려면 먼저 이를 설치해야 합니다.  
  
확장을 설치할 위치는 확장 유형 및 확장을 사용하려는 위치에 따라 다릅니다. 최신 버전의 Visual Studio에서 일부 구성 요소의 설치 위치가 SQL Server 설치 디렉터리에서 Visual Studio 디렉터리 내부로 이동했습니다. 이 설정을 사용하면 서로 다른 버전의 소프트웨어를 더욱 쉽게 함께 실행할 수 있지만 서로 다른 버전의 SQL Server Data Tools에서 명령줄로부터 확장을 사용하려는 경우 여러 위치에 확장을 설치해야 할 수 있습니다.  
  
### <a name="installing-extensions-for-use-inside-visual-studio"></a>Visual Studio 내에서 사용하기 위해 확장 설치  
  
|확장 유형|설치 위치|  
|------------------|--------------------|  
|SQL Server 단위 테스트의 사용자 지정 테스트 조건|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\TestConditions|  
|빌드 참가자<br /><br />배포 참가자<br /><br />정적 코드 분석 규칙|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions|  
  
<Visual Studio Install Dir>은 사용하고 있는 Visual Studio의 버전과 선택한 설치 위치에 따라 다릅니다. Visual Studio 2012의 경우 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 11.0입니다. Visual Studio 2013의 경우 일반적으로 C:\Program Files (x86)\\MicrosoftVisual Studio 12.0입니다.  
  
확장은 명령줄 서비스의 일부로 실행될 수 있습니다.  
  
|확장 유형|명령줄 서비스|설치 폴더|  
|------------------|------------------------|------------------|  
|SQL Server 단위 테스트의 사용자 지정 테스트 조건|MSBuild/MSTest를 사용하여 Visual Studio 2013용 개발자 명령 프롬프트 및 유사한 명령줄 도구에서 단위 테스트를 실행할 수 있습니다.|Visual Studio 내에서 실행되는 경우와 동일합니다.|  
|빌드 참가자<br /><br />배포 참가자|[SqlPackage.exe](../tools/sqlpackage.md) 또는 데이터베이스 프로젝트를 빌드할 때 MSBuild 배포 또는 게시 대상 사용|MSBuild: Visual Studio 내에서 실행되는 경우와 동일합니다.<br /><br />[SqlPackage.exe](../tools/sqlpackage.md): Visual Studio 디렉터리 내에 있는 경우 이전과 동일합니다.<br /><br />SqlPackage.exe 및 기타 DacFx DLL이 해당 디렉터리 외부에 있는 경우 확장은 동일한 디렉터리나 C:\Program Files (x86)\\\MicrosoftSQL Server\120\DAC\bin\Extensions에 배치되어야 합니다.|  
|정적 코드 분석 규칙|MSBuild를 사용하여 프로젝트를 빌드하고 정적 코드 분석을 실행할 수 있습니다.<br /><br />또한 사용자 고유의 애플리케이션에서 CodeAnalysisService API를 사용하여 코드 분석을 실행할 수 있습니다. 이 경우에 확장 조회 규칙은 SqlPackage.exe가 사용되는 경우와 동일하게 작동합니다.|빌드 및 배포 참가자의 경우와 동일|  
  
> [!NOTE]  
> Program Files 폴더 아래의 설치 디렉터리에 액세스하려면 사용 중인 컴퓨터에 대한 관리자 권한이 있어야 합니다. 적절한 권한이 없으면 네트워크 관리자에게 문의하세요.  
  
**Security Considerations**  
  
사용자가 만들지 않은 확장을 설치하려면 먼저 다음과 같은 위험 요소를 이해하고 있어야 합니다.  
  
-   확장의 설치 프로그램은 설치 권한을 기반으로 보호되는 리소스에 액세스하려고 하는 악의적 프로그램일 수 있습니다.  
  
-   확장 자체가 확장을 사용하는 사용자에게 충분한 사용 권한이 있는 경우 보호되는 리소스를 제어하려고 하는 악의적 프로그램일 수 있습니다.  
  
위험을 최소화하려면 출처를 알 수 있는 경우에만 확장을 설치해야 합니다. 확장의 출처를 신뢰할 수 없는 경우에는 확장을 설치 및 사용하기 전에 확장의 소스 코드와 해당 설치 프로그램(있는 경우)을 검사해야 합니다.  
  
## <a name="to-install-a-custom-feature-extension"></a>사용자 지정 기능 확장을 설치하려면  
서명된 어셈블리(.dll)를 올바른 설치 폴더에 복사합니다. Visual Studio를 닫았다가 다시 엽니다. 이제 확장을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 기능 확장](../ssdt/extending-the-database-features.md)  
  
