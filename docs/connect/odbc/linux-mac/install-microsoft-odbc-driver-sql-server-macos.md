---
title: Microsoft ODBC Driver for SQL Server 설치(macOS)
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
author: rothja
ms.author: v-jizho2
manager: jroth
ms.openlocfilehash: 7ad2b810092fae850a667a1611880f4b03b6a9a8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79078956"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-macos"></a>Microsoft ODBC Driver for SQL Server 설치(macOS)

이 문서에서는 macOS에 Microsoft ODBC Driver for SQL Server를 설치하는 방법을 설명합니다. SQL Server용 선택적 명령줄 도구(`bcp` 및 `sqlcmd`)와 unixODBC 개발 헤더에 대한 지침도 포함되어 있습니다.

이 문서에서는 bash 셸에서 ODBC 드라이버를 설치하기 위한 명령을 제공합니다. 패키지를 직접 다운로드하려면 [ODBC Driver for SQL Server 다운로드](../download-odbc-driver-for-sql-server.md)를 참조하세요.

## <a name="microsoft-odbc-17"></a>Microsoft ODBC 17

macOS에 Microsoft ODBC Driver 17 for SQL Server를 설치하려면 다음 명령을 실행합니다.

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=Y brew install msodbcsql17 mssql-tools
```

> [!IMPORTANT]
> 일시적으로 사용할 수 있었던 v17 `msodbcsql` 패키지를 설치한 경우 `msodbcsql17` 패키지를 설치하기 전에 제거하는 것이 좋습니다. 그래야 충돌이 방지됩니다. `msodbcsql17` 패키지는 `msodbcsql` v13 패키지와 병렬로 설치할 수 있습니다.

## <a name="previous-versions"></a>이전 버전

다음 섹션에서는 macOS에 이전 버전의 Microsoft ODBC Driver를 설치하는 방법을 설명합니다.

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

OS X 10.11(El Capitan) 및 macOS 10.12(Sierra)에 Microsoft ODBC Driver 13.1 for SQL Server를 설치하려면 다음 명령을 사용합니다.

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="driver-files"></a>드라이버 파일

macOS 기반 ODBC 드라이버는 다음 구성 요소를 포함합니다.

|구성 요소|Description|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib 또는 libmsodbcsql.13.dylib|드라이버 기능이 모두 포함된 동적 라이브러리(`dylib`) 파일입니다. 이 파일은 `/usr/local/lib/`에 설치됩니다.|  
|`msodbcsqlr17.rll` 또는 `msodbcsqlr13.rll`|드라이버 라이브러리에 대한 해당 리소스 파일입니다. 이 파일은 드라이버 17의 경우 `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` 및 드라이버 13의 경우 `[driver .dylib directory]../share/msodbcsql/resources/en_US/`에 설치됩니다. | 
|msodbcsql.h|드라이버를 사용하는 데 필요한 새 정의를 모두 포함하는 헤더 파일입니다.<br /><br /> **참고:**  동일한 프로그램에서 msodbcsql.h 및 odbcss.h를 참조할 수 없습니다.<br /><br /> msodbcsql.h는 드라이버 17의 경우 `/usr/local/include/msodbcsql17/` 및 드라이버 13의 경우 `/usr/local/include/msodbcsql/`에 설치됩니다. |
|LICENSE.txt|최종 사용자 사용권 계약의 사용 약관을 포함하는 텍스트 파일입니다. 이 파일은 드라이버 17의 경우 `/usr/local/share/doc/msodbcsql17/` 및 드라이버 13의 경우 `/usr/local/share/doc/msodbcsql/`에 저장됩니다. |
|RELEASE_NOTES|릴리스 정보를 포함하는 텍스트 파일입니다. 이 파일은 드라이버 17의 경우 `/usr/local/share/doc/msodbcsql17/` 및 드라이버 13의 경우 `/usr/local/share/doc/msodbcsql/`에 저장됩니다. |

## <a name="resource-file-loading"></a>리소스 파일 로드

드라이버가 작동하려면 리소스 파일을 로드해야 합니다. 이 파일의 이름은 드라이버 버전에 따라 `msodbcsqlr17.rll` 또는 `msodbcsqlr13.rll`입니다. `.rll` 파일의 위치는 위의 표에서 설명했듯이 드라이버 자체(`so` 또는 `dylib`)의 위치에 대한 상대 위치입니다. 버전 17.1 현재 `.rll`을 상대 경로에서 로드하는 데 실패한 경우 기본 디렉터리에서도 로드를 시도합니다. macOS의 기본 리소스 파일 경로는 `/usr/local/share/msodbcsql17/resources/en_US/`입니다.

## <a name="troubleshooting"></a>문제 해결

ODBC 드라이버를 사용하여 SQL Server에 연결할 수 없는 경우 [연결 문제 해결](known-issues-in-this-version-of-the-driver.md#connectivity)에서 알려진 문제 문서를 참조하세요.

## <a name="next-steps"></a>다음 단계

드라이버를 설치한 후 [C++ ODBC 예제 애플리케이션](../../odbc/cpp-code-example-app-connect-access-sql-db.md)을 사용해 볼 수 있습니다. ODBC 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [애플리케이션 개발](../../../odbc/reference/develop-app/developing-applications.md)을 참조하세요.

자세한 내용은 ODBC 드라이버 [릴리스 정보](release-notes-odbc-sql-server-linux-mac.md) 및 [시스템 요구 사항](system-requirements.md)을 참조하세요.
