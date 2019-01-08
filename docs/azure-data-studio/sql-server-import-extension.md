---
title: SQL Server 가져오기 확장
titleSuffix: Azure Data Studio
description: 설치 하 고 Azure Data Studio 용 SQL Server 가져오기 확장 (미리 보기) 사용
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8248404353674f8139a26cfc75f37363557136b9
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030747"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 가져오기 확장 (미리 보기)

SQL Server 가져오기 확장 (미리 보기)는 SQL 테이블에.csv 및.txt 파일을 변환합니다. 이 마법사는 라고 하는 Microsoft Research 프레임 워크를 활용 [Program Synthesis using 예제 (PROSE)](https://microsoft.github.io/prose/) 지능적으로 최소한의 사용자 입력을 사용 하 여 파일 구문 분석 합니다. 이 데이터 랭 글 링을 위한 강력한 프레임 워크 이며 Microsoft Excel에서 채우기 플래시를 구동 하는 동일한 기술을

이 기능은 SSMS 버전에 대 한 자세한 내용은 읽어보세요 [이 문서에서는](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)합니다.


## <a name="install-the-sql-server-import-extension"></a>SQL Server 가져오기 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스를 하려면 확장 아이콘을 선택 하거나 선택 **Extensions** 에 **보기** 메뉴.
2. 해당 정보를 보려면 사용 가능한 확장을 선택 합니다.

   ![확장 관리자 가져오기](media/sql-server-import-extension/import-wizard-install.png)

1. 원하는 확장을 선택 하 고 **설치** 것입니다.
2. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.

## <a name="start-import-wizard"></a>가져오기 마법사 시작

1. SQL Server 가져오기를 시작 하려면 먼저 서버 탭에서 서버에 연결을 확인 합니다.
2. 연결 후, 대상 데이터베이스를 SQL 테이블에는 파일을 가져올으로 드릴 다운 합니다.
3. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 클릭 **가져오기 마법사**합니다.
    ![열기 마법사](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>파일 가져오기
1. 마법사를 시작 하려면 마우스 오른쪽 단추로 서버 및 데이터베이스를 이미 자동으로 채워집니다. 다른 활성 연결의 경우 드롭다운 목록에서 선택할 수 있습니다. 
    
    클릭 하 여 파일을 선택 **찾아보기.** 자동 채우기 테이블 이름은 파일 이름에 기반 해야 하지만 변경할 수 있습니다도 직접.

    기본적으로 스키마 dbo 수 있지만 변경할 수 있습니다. 계속 진행하려면 **다음** 을 클릭합니다.
    ![입력된 파일](media/sql-server-import-extension/import-wizard-input-file.png)
1. 마법사가 처음 50 개 행을 기반으로 하는 미리 보기를 생성 합니다. 작업은 없습니다 추가 페이지 이외의 데이터가 정확 하 게 표시 확인 합니다. 계속 진행하려면 **다음** 을 클릭합니다.
    ![열기 마법사](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 이 페이지에서 변경할 수 있습니다 열 이름에 데이터 형식, 것이 기본 키가 아니면 null을 허용 하도록 합니다. 원하는 수 만큼 많은 변경 사항을 만들 수 있습니다. 클릭 **데이터 가져오기** 진행 합니다.
    ![열기 마법사](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 이 페이지는 선택한 작업의 요약을 제공 합니다. 테이블에 성공적으로 삽입 여부를 확인할 수 있습니다. 

    클릭 하거나 **끝나면** **이전** 변경 해야 할 경우 또는 **새 파일 가져오기** 신속 하 게 다른 파일을 가져오려면.
    ![열기 마법사](media/sql-server-import-extension/import-wizard-summary.png)
1. 대상 데이터베이스를 새로 고치거 나 테이블 이름에서 SELECT 쿼리를 실행 하 여 테이블에 성공적으로 가져온 경우를 확인 합니다.

## <a name="next-steps"></a>다음 단계
- 가져오기 마법사에 대 한 자세한 내용은 합니다 [블로그 게시물](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)합니다.
- PROSE에 대 한 자세한 내용은 참조는 [설명서.](https://microsoft.github.io/prose/)
