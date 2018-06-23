---
title: 코드 서식 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indenting code [SQL Server]
- displaying URLs
- code formatting [SQL Server Management Studio]
- collapsing text
- formats [SQL Server], code formatting in SQL Server Management Studio
- hiding text
- formats [SQL Server]
- text [SQL Server], code formats
- automatic indentation
- converting text to lower case
- Query Editor [SQL Server Management Studio], managing code formats
- URL displayed in code [SQL Server Management Studio]
- converting text to upper case
- text [SQL Server]
- unindenting code
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f57e209ec0bc4417af90b4d257d6be566cccb731
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185376"
---
# <a name="manage-code-formatting"></a>코드 서식 관리
  편집기를 사용하면 들여쓰기, 숨겨진 텍스트, URL 등으로 코드의 서식을 지정할 수 있습니다. 또한 스마트 들여쓰기를 사용하여 입력 시에 코드의 서식을 자동으로 지정할 수 있습니다.  
  
## <a name="indenting"></a>들여쓰기  
 세 가지 다른 스타일의 텍스트 들여쓰기 중에서 선택할 수 있습니다. 또한 단일 들여쓰기나 탭을 구성하는 공백 수와 들여쓰기 시에 편집기에서 탭이나 공백 문자를 사용하는지 여부를 지정할 수 있습니다.  
  
#### <a name="to-choose-an-indenting-style"></a>들여쓰기 스타일을 선택하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **텍스트 편집기**를 클릭합니다.  
  
3.  폴더를 클릭하고 **모든 언어** 를 선택하여 모든 언어에 들여쓰기를 설정합니다.  
  
4.  **탭**을 클릭합니다.  
  
5.  다음 옵션 중 하나를 클릭합니다.  
  
    -   **없음**. 커서를 다음 줄의 시작으로 이동합니다.  
  
    -   **블록**. 커서가 다음 줄을 이전 줄에 맞춥니다.  
  
    -   **스마트** (기본값). 사용할 적절할 들여쓰기 스타일을 언어 서비스로 결정합니다.  
  
    > [!NOTE]  
    >  모든 언어에서 세 가지 들여쓰기 옵션이 모두 제공되는 것은 아닙니다.  
  
#### <a name="to-change-indent-tab-settings"></a>들여쓰기 탭 설정을 변경하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **텍스트 편집기**를 클릭합니다.  
  
3.  **모든 언어** 에 대한 폴더를 선택하여 모든 언어에 들여쓰기를 설정합니다.  
  
4.  **탭**을 클릭합니다.  
  
5.  탭 및 들여쓰기 작업에 대한 탭 문자를 지정하려면 **탭 유지**를 클릭합니다. 공백 문자를 지정하려면 **공백 삽입**을 선택합니다.  
  
     **공백 삽입**을 선택한 경우 각 탭이나 들여쓰기가 나타내는 공백 문자 수를 각각 **탭 크기** 또는 **들여쓰기 크기**아래에 입력합니다.  
  
#### <a name="to-indent-code"></a>코드를 들여쓰려면  
  
1.  들여쓸 텍스트를 선택합니다.  
  
2.  Tab 키를 누르거나 표준 도구 모음에서 **들여쓰기** 단추를 클릭합니다.  
  
#### <a name="to-unindent-code"></a>코드를 내어쓰려면  
  
1.  내어쓸 텍스트를 선택합니다.  
  
2.  Shift+Tab 키를 누르거나 표준 도구 모음에서 **내어쓰기** 단추를 클릭합니다.  
  
#### <a name="to-automatically-indent-all-of-your-code"></a>모든 코드를 자동으로 들여쓰려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **텍스트 편집기**를 클릭합니다.  
  
3.  **모든 언어**를 클릭합니다.  
  
4.  **탭**을 클릭합니다.  
  
5.  **스마트**를 클릭합니다.  
  
> [!NOTE]  
>  일부 언어에서는 **스마트** 옵션을 사용할 수 없습니다.  
  
#### <a name="to-convert-white-space-to-tabs"></a>공백을 탭으로 변환하려면  
  
1.  탭으로 변환할 공백이 있는 텍스트를 선택합니다.  
  
2.  **편집** 메뉴에서 **고급**을 가리킨 다음 **선택 영역의 공백을 탭으로**를 클릭합니다.  
  
#### <a name="to-convert-tabs-to-spaces"></a>탭을 공백으로 변환하려면  
  
1.  공백으로 변환할 탭이 있는 텍스트를 선택합니다.  
  
2.  **편집** 메뉴에서 **고급**을 가리킨 다음 **선택 영역의 탭을 공백으로**를 클릭합니다.  
  
 이러한 명령의 동작은 **옵션** 대화 상자의 탭 설정에 따라 달라집니다. 예를 들어 탭 설정이 4이면 **선택 영역의 공백을 탭으로** 는 4개의 연속된 공백마다 탭을 만들고 **선택 영역의 탭을 공백으로** 는 모든 탭마다 4개의 공백을 만듭니다.  
  
## <a name="converting-text-to-upper-and-lower-case"></a>텍스트를 대문자 및 소문자로 변환  
 명령을 사용하여 텍스트를 모두 대문자나 소문자로 변환할 수 있습니다.  
  
#### <a name="to-switch-text-to-upper-or-lower-case"></a>텍스트를 대문자나 소문자로 변환하려면  
  
1.  변환할 텍스트를 선택합니다.  
  
2.  텍스트를 대문자로 변환하려면 Ctrl+Shift+U를 누르거나 **편집** 메뉴의 **고급** 하위 메뉴에서 **대문자로** 를 클릭합니다.  
  
3.  텍스트를 소문자로 변환하려면 Ctrl+Shift+L을 누르거나 **편집** 메뉴의 **고급** 하위 메뉴에서 **소문자로** 를 클릭합니다.  
  
> [!NOTE]  
>  바로 가기 키의 전체 목록을 보려면 [SQL Server Management Studio 바로 가기 키](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)를 참조하세요.  
  
## <a name="displaying-and-linking-to-urls"></a>URL 표시 및 연결  
 코드에서 클릭 가능한 URL을 만들고 표시할 수 있습니다. 기본적으로 URL은 다음과 같습니다.  
  
-   밑줄이 그어집니다.  
  
-   마우스 포인터를 위로 이동하면 손 모양으로 바뀝니다.  
  
-   클릭하면 URL이 열립니다(URL이 유효한 경우).  
  
#### <a name="to-display-a-clickable-url"></a>클릭 가능한 URL을 표시하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **텍스트 편집기**를 클릭합니다.  
  
3.  특정 언어에 대한 옵션만 변경하려면 해당 언어 폴더를 클릭한 다음 **일반**을 클릭합니다. 모든 언어에 대한 옵션을 변경하려면 **모든 언어** 를 클릭한 다음 **일반**을 클릭합니다.  
  
4.  **한 번 클릭으로 URL 탐색**을 선택합니다.  
  
  