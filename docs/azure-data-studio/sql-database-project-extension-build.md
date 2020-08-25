---
title: 프로젝트 빌드 및 게시
description: SQL Server 데이터베이스 프로젝트 확장을 사용하여 빌드 및 게시
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 191b10fd32d7c49c3f4a4e81c109e52fb2a1a81c
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88171372"
---
# <a name="build-and-publish-a-project"></a>프로젝트 빌드 및 게시

Azure Data Studio용 SQL 데이터베이스 프로젝트 확장의 빌드 프로세스를 통해 Windows, macOS 및 Linux 환경에서 *dacpac*을 만들 수 있습니다. 프로젝트는 게시 프로세스를 사용하여 로컬 또는 클라우드 환경에 배포할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소
- [Azure Data Studio용 SQL 데이터베이스 프로젝트 확장을 설치 및 구성](sql-database-project-extension.md)합니다.


## <a name="build-a-database-project"></a>데이터베이스 프로젝트 빌드

 **탐색기** 아래 **프로젝트** 뷰렛에서 *.sqlproj* 루트 노드를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다.

 출력 창이 빌드 프로세스의 출력과 함께 자동으로 표시됩니다.  빌드가 성공하면 다음과 같은 메시지로 종료됩니다. 

 ``` ... exited with code: 0 ```

## <a name="publish-a-database-project"></a>데이터베이스 프로젝트 게시

빌드 프로세스를 통해 프로젝트를 성공적으로 컴파일한 후에는 데이터베이스를 SQL Server 인스턴스에 게시할 수 있습니다. 데이터베이스 프로젝트를 게시하려면 **탐색기** 아래 **프로젝트** 뷰렛에서 *.sqlproj* 루트 노드를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.

표시되는 **데이터베이스 게시** 대화 상자에서 서버 연결을 지정하고 만들 데이터베이스 이름을 지정합니다.

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio용 SQL 데이터베이스 프로젝트 확장](sql-database-project-extension.md)
- [명령줄에서 SQL Database Projects 빌드](sql-database-project-extension-build-from-command-line.md)
