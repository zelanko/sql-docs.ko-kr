---
title: mssql-cli
description: mssql-cli는 Windows, macOS 또는 Linux에서 실행되는 SQL Server를 위한 대화형 명령줄 쿼리 도구입니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein, maghan
ms.custom: tools|mssql-cli
ms.date: 02/22/2018
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 03bc52a6f8941bbc8d04f8f795876b0ca664f08c
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462287"
---
# <a name="mssql-cli-command-line-query-tool-for-sql-server-preview"></a>SQL Server를 위한 mssql-cli 명령줄 쿼리 도구(미리 보기)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

mssql-cli는 SQL Server 쿼리를 위한 대화형 명령줄 쿼리 도구로서, Windows, macOS 또는 Linux에서 실행됩니다.

## <a name="install-mssql-cli"></a>mssql-cli 설치

자세한 설치 지침은 [설치 가이드](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)를 참조하세요. 아래에 가장 일반적인 설치 시나리오가 요약되어 있습니다.

### <a name="windows-and-macos-installation"></a>Windows 및 macOS 설치

mssql-cli는 `pip`를 사용하여 Windows 및 macOS에 설치됩니다.

```$ pip install mssql-cli```

자세한 지침은 [설치 가이드](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)를 참조하세요.

### <a name="linux-installation"></a>Linux 설치

Microsoft 리포지토리를 등록한 후에는 몇 가지 Linux 배포판의 패키지 관리자를 통해 mssql cli를 설치하고 업그레이드할 수 있습니다.

다음 예제는 Ubuntu 18.04(Bionic)에 적용됩니다. 다른 배포판에 대한 자세한 내용 및 예제는 [설치 가이드](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)에서 확인할 수 있습니다.

```
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod

# Update the list of products
sudo apt-get update

# Install mssql-cli
sudo apt-get install mssql-cli

# Install missing dependencies
sudo apt-get install -f
```

## <a name="mssql-cli-documentation"></a>mssql-cli 설명서

Mssql-cli 설명서는 [mssql-cli GitHub 리포지토리](https://github.com/dbcli/mssql-cli)에 있습니다.

- [기본 페이지/추가 정보](https://github.com/dbcli/mssql-cli)
- [설치 가이드](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)
- [사용 가이드](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)

추가 설명서는 [doc 폴더](https://github.com/dbcli/mssql-cli/tree/master/doc)에 있습니다.
