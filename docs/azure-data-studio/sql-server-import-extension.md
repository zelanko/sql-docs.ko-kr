---
title: SQL Server 가져오기 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio에 대한 SQL Server 가져오기 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 012c2c880e81c095e90086cf26ebffd6117d534e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959127"
---
# <a name="sql-server-import-extension-preview"></a>SQL Server 가져오기 확장(미리 보기)

SQL Server 가져오기 확장(미리 보기)은 .txt 및 .csv 파일을 SQL 테이블로 변환합니다. 이 마법사는 [PROSE(Program Synthesis using Examples)](https://microsoft.github.io/prose/)라는 Microsoft Research 프레임워크를 활용하여 최소한의 사용자 입력으로 파일을 지능적으로 구문 분석합니다. 이 기능은 데이터 랭글링을 위한 강력한 프레임워크로, Microsoft Excel의 빠른 채우기를 지원하는 것과 동일한 기술입니다.

이 기능의 SSMS 버전에 대해 자세히 알아보려면 [이 문서](https://docs.microsoft.com/sql/relational-databases/import-export/import-flat-file-wizard)를 참조하세요.


## <a name="install-the-sql-server-import-extension"></a>SQL Server 가져오기 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

   ![가져오기 확장 관리자](media/sql-server-import-extension/import-wizard-install.png)

1. 원하는 확장을 선택하고 **설치**합니다.
2. **다시 로드**를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).

## <a name="start-import-wizard"></a>가져오기 마법사 시작

1. SQL Server 가져오기를 시작하려면 먼저 서버 탭에서 서버에 연결합니다.
2. 연결한 후에는 파일을 SQL 테이블로 가져올 대상 데이터베이스로 드릴다운합니다.
3. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **가져오기 마법사**를 클릭합니다.
    ![가져오기 마법사 열기](media/sql-server-import-extension/open-import-wizard.png)

## <a name="importing-a-file"></a>파일 가져오기
1. 마우스 오른쪽 단추를 클릭하여 마법사를 시작하면 서버와 데이터베이스가 미리 자동으로 채워져 있습니다. 다른 활성 연결이 있는 경우 드롭다운에서 선택할 수 있습니다. 
    
    **찾아보기**를 클릭하여 파일을 선택합니다. 파일 이름에 따라 테이블 이름을 자동으로 채워지지만 직접 변경할 수도 있습니다.

    기본적으로 스키마는 dbo가 되지만 변경할 수 있습니다. 계속 진행하려면 **다음** 을 클릭합니다.
    ![입력 파일](media/sql-server-import-extension/import-wizard-input-file.png)
1. 이 마법사는 처음 50개 행을 기준으로 미리 보기를 생성합니다. 이 페이지에서는 데이터가 정확하게 표시되는지 확인하는 것 외에는 다른 작업을 수행할 필요가 없습니다. 계속 진행하려면 **다음** 을 클릭합니다.
    ![가져오기 마법사 열기](media/sql-server-import-extension/import-wizard-preview-data.png)
2. 이 페이지에서 열 이름, 데이터 형식 및 기본 키인지 여부, null을 허용하지 여부를 변경할 수 있습니다. 원하는 대로 변경 작업을 수행할 수 있습니다. **데이터 가져오기**를 클릭하여 계속 진행합니다.
    ![가져오기 마법사 열기](media/sql-server-import-extension/import-wizard-modify-columns.png)
3. 이 페이지에서는 선택한 작업에 대한 요약 정보를 제공합니다. 테이블이 성공적으로 삽입되었는지 여부를 확인할 수도 있습니다. 

    변경해야 하는 경우 **완료, 이전**을 클릭하고, 다른 파일을 빠르게 가져오려면 **새 파일 가져오기**를 클릭할 수 있습니다.
    ![가져오기 마법사 열기](media/sql-server-import-extension/import-wizard-summary.png)
1. 대상 데이터베이스를 새로 고치거나 테이블 이름에 대해 SELECT 쿼리를 실행하여 테이블을 성공적으로 가져왔는지 확인합니다.

## <a name="next-steps"></a>다음 단계
- 가져오기 마법사에 대한 자세한 내용은 [블로그 게시물](https://cloudblogs.microsoft.com/sqlserver/2018/08/30/the-august-release-of-sql-operations-studio-is-now-available/)을 참조하세요.
- PROSE에 대한 자세한 내용은 [설명서](https://microsoft.github.io/prose/)를 참조하세요.
