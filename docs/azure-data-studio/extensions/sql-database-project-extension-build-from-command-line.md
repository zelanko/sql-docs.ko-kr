---
title: 명령줄에서 프로젝트 빌드
description: 명령줄에서 SQL Server Database Projects 빌드
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 08/07/2020
ms.openlocfilehash: a6849f13f8182285749c7a95801ee111e7ba0130
ms.sourcegitcommit: c4d6804bde7eaf72d9233d6d43f77d77d1b17c4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91624680"
---
# <a name="build-a-database-project-from-command-line"></a>명령줄에서 데이터베이스 프로젝트 빌드

Azure Data Studio용 SQL Database 프로젝트 확장에서 [데이터베이스 프로젝트를 빌드](sql-database-project-extension-build.md)하는 그래픽 사용자 인터페이스를 제공하지만 Windows, macOS 및 Linux 환경의 경우 명령줄 빌드 환경도 사용할 수 있습니다. 이 문서에서는 명령줄에서 dacpac에 대해 SQL 프로젝트를 빌드하는 데 필요한 필수 조건과 구문을 간략하게 설명합니다.

## <a name="prerequisites"></a>필수 구성 요소

1. [Azure Data Studio용 SQL 데이터베이스 프로젝트 확장을 설치 및 구성](sql-database-project-extension.md)합니다.

2. 다음 .NET Core dll 및 대상 파일 `Microsoft.Data.Tools.Schema.SqlTasts.targets`는 SQL Database Projects용 Azure Data Studio 확장에서 지원하는 모든 플랫폼의 명령줄에서 SQL 데이터베이스 프로젝트를 빌드하는 데 필요합니다. 이러한 파일은 Azure Data Studio 인터페이스에서 완료되는 첫 번째 빌드 중에 확장에서 만들어지며 `BuildDirectory`의 확장 폴더에 배치됩니다.  예를 들어 Linux에서는 이러한 파일이 `~\.azuredatastudio\extensions\microsoft.sql-database-projects-x.x.x\BuildDirectory\`에 배치됩니다.  다음 10개 파일을 액세스할 수 있는 새 폴더에 복사하거나 해당 위치를 적어 둡니다.  이 문서에서는 해당 위치가 `DotNet Core build folder`입니다.

    - Microsoft.Data.Tools.Schema.Sql.dll
    - Microsoft.Data.Tools.Schema.Tasks.Sql.dll
    - Microsoft.Data.Tools.Utilities.dll
    - System.Io.Packaging.dll
    - Microsoft.SqlServer.Dac.dll
    - Microsoft.SqlServer.Dac.Extensions.dll
    - Microsoft.SqlServer.TransactSql.ScriptDom.dll
    - Microsoft.SqlServer.Types.dll
    - Microsoft.Data.Tools.Schema.SqlTasks.targets
    - System.ComponentModel.Composition.dll
    - Microsoft.Data.SqlClient.dll

3. Azure Data Studio에서 프로젝트를 만든 경우 [명령줄에서 프로젝트 빌드](#build-the-project-from-the-command-line)로 건너뜁니다. SSDT(SQL Server Data Tools)에서 프로젝트를 만든 경우 Azure Data Studio SQL Database 프로젝트 확장에서 프로젝트를 엽니다.  Azure Data Studio에서 프로젝트를 열면 아래 설명된 대로 세 가지 편집을 통해 `sqlproj` 파일을 자동으로 업데이트합니다.

    1. 가져오기 조건

    ```console
    <Import Condition="'$(NetCoreBuild)' == 'true'" Project="$(NETCoreTargetsPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' != ''" Project="$(SQLDBExtensionsRefPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' == ''" Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    ```

    2. 패키지 참조

    ```console
    <ItemGroup>
        <PackageReference Condition="'$(NetCoreBuild)' == 'true'" Include="Microsoft.NETFramework.ReferenceAssemblies" Version="1.0.0" PrivateAssets="All"/>
    </ItemGroup>
    ```

    3. SSDT(SQL Server Data Tools) 및 Azure Data Studio에서 이중 편집을 지원하는 데 필요한 정리 대상

        ```console
        <Target Name="AfterClean">
            <Delete Files="$(BaseIntermediateOutputPath)\project.assets.json"/>
        </Target>
        ```

## <a name="build-the-project-from-the-command-line"></a>명령줄에서 프로젝트 빌드

전체 .NET 폴더에서 다음 명령을 사용합니다.

```console
dotnet build "<sqlproj file path>" /p:NetCoreBuild=true /p:NETCoreTargetsPath="<DotNet Core build folder>"
```

예를 들어 Linux의 경우 `/usr/share/dotnet`에서 다음 명령을 사용합니다.

```console
dotnet build "/home/myuser/Documents/DatabaseProject1/DatabaseProject1.sqlproj" /p:NetCoreBuild=true /p:NETCoreTargetsPath="/home/myuser/.azuredatastudio-insiders/extensions/microsoft.sql-database-projects-0.1.2/BuildDirectory"  
```

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio용 SQL 데이터베이스 프로젝트 확장](sql-database-project-extension.md)
- [SQL Database Projects 게시](sql-database-project-extension-build.md#publish-a-database-project)
