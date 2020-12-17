---
title: 편집기 및 보기 모드 관리
description: SQL Server Management Studio의 두 가지 보기 모드 중 하나를 선택하는 방법을 알아봅니다. 탭 문서 모드 또는 다중 문서 인터페이스 모드. 분할 뷰, 자동 줄 바꿈, 가상 공간 모드, 줄 번호 표시, 전체 화면 모드, 모두 자동 숨기기에 대해서도 알아봅니다.
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], managing window behavior
- workbench view modes [SQL Server Management Studio]
- full screen mode [SQL Server Management Studio]
- fonts [SQL Server Management Studio]
- word wraps [SQL Server Management Studio]
- virtual space mode [SQL Server Management Studio]
- splitting document views
- displaying line numbers
- view modes [SQL Server Management Studio]
ms.assetid: 25c58a14-9f94-4296-9770-7d84c6bc3969
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65ca95f3aa2cef72b49a9f80bdbf615e890a85d0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478774"
---
# <a name="manage-the-editor-and-view-mode"></a>편집기 및 보기 모드 관리

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

편집기에서 여러 가지 방법으로 코드 보기를 제어할 수 있습니다.  

## <a name="changing-the-view-mode"></a>보기 모드 변경  

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 **탭 문서** 라는 보기 모드가 있는데 이 기능을 사용하면 여러 개의 편집기와 문서를 동시에 열어서 편집기 상단 탭을 통해 액세스할 수 있습니다. 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 MDI(다중 문서 인터페이스) 모드로 열 수도 있습니다. 이 모드에서는 탭이 없는 창을 여러 개 열어 바둑판식으로 배열하거나 창 크기를 최소화할 수도 있습니다.  
  
#### <a name="to-switch-between-view-modes"></a>보기 모드를 전환하려면  
  
1.  **도구** 메뉴에서 **옵션** 을 클릭합니다.  
  
2.  **환경** 을 클릭하고 **일반** 을 클릭합니다.  
  
3.  **탭 문서** 또는 **MDI 환경** 을 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 다시 시작할 때까지 변경 내용이 적용되지 않습니다.  
  
## <a name="splitting-the-view"></a>보기 분할  
 보다 손쉽게 편집하기 위해 편집기 창을 두 부분으로 분할할 수 있습니다.  
  
#### <a name="to-split-a-window"></a>창을 분할하려면  
  
1.  스크롤 막대 위에 있는 분할 막대를 클릭합니다.  
  
2.  분할 막대를 아래로 끕니다.  
  
3.  단일 창으로 돌아가려면 두 창을 분할하는 분할 막대를 두 번 클릭합니다.  
  
 새 창에는 동일한 문서가 포함되어 있습니다. 두 창에 동일한 문서 위치를 표시하고 한 창에서 내용을 변경하면 해당 내용이 다른 창에도 반영됩니다.  
  
## <a name="word-wrap"></a>자동 줄 바꿈  
 자동 줄 바꿈을 활성화하면 가로 스크롤 막대가 제거되고 편집기 창 너비를 초과하는 코드 줄은 창 밖으로 스크롤되지 않고 다음 줄로 자동 줄 바꿈되어 표시됩니다.  
  
#### <a name="to-activate-word-wrap"></a>자동 줄 바꿈을 활성화하려면  
  
1.  **도구** 메뉴에서 **옵션** 을 클릭합니다.  
  
2.  **텍스트 편집기** 를 클릭합니다.  
  
3.  해당 언어 폴더(모든 언어에 적용하려면 **모든 언어** )를 엽니다.  
  
4.  **자동 줄 바꿈** 을 선택합니다.  
  
## <a name="enabling-virtual-space-mode"></a>가상 공간 모드 설정  
 **가상 공간** 모드로 편집기를 열면 각 줄의 끝을 넘어서는 공간은 무한한 공간처럼 보이기 때문에 표시되는 화면 영역 밖으로 코드 줄이 계속 이어집니다.  
  
#### <a name="to-enable-virtual-space-mode"></a>가상 공간 모드를 활성화하려면  
  
1.  **도구** 메뉴에서 **옵션** 을 클릭합니다.  
  
2.  **텍스트 편집기** 를 클릭합니다.  
  
3.  해당 언어 폴더(모든 언어에 적용하려면 **모든 언어** )를 엽니다.  
  
4.  **가상 공간 활성화** 를 선택합니다.  
  
 가상 공간 모드를 활성화하지 않은 경우 커서는 한 줄의 끝에서 다음 줄의 첫 번째 문자로 또는 그 반대로 줄 바꿈됩니다.  
  
## <a name="displaying-line-numbers"></a>줄 번호 표시  
 코드에 줄 번호 매기기를 설정할 수 있습니다. 줄 번호는 코드를 이동할 때 유용합니다. 자세한 내용은 [코드 및 텍스트 이동](./navigate-code-and-text.md)을 참조하세요.  
  
> [!NOTE]  
>  줄 번호 매기기를 설정하더라도 문서에 자동으로 줄 번호가 표시되어 출력되지는 않습니다. 줄 번호를 출력하려면 **파일** 메뉴의 **페이지 설정** 명령에서 **줄 번호** 확인란을 선택해야 합니다.  
  
#### <a name="to-display-line-numbers-in-code"></a>코드에 줄 번호를 표시하려면  
  
1.  **도구** 메뉴에서 **옵션** 을 클릭합니다.  
  
2.  **텍스트 편집기** 를 클릭합니다.  
  
3.  **모든 언어** 를 클릭합니다.  
  
4.  **일반** 을 클릭합니다.  
  
5.  **줄 번호** 를 선택합니다.  
  
 일부 프로그래밍 언어에만 줄 번호 매기기를 지정하려면 해당 폴더에서 **줄 번호** 를 선택합니다.  
  
## <a name="enabling-full-screen-mode"></a>전체 화면 모드 설정  
 전체 화면 모드를 설정하면 모든 도구 창을 숨기고 문서 창만 볼 수 있습니다.  
  
#### <a name="to-enable-full-screen-mode"></a>전체 화면 모드를 설정하려면  
  
1.  Alt+Shift+Enter를 눌러 전체 화면 모드를 설정/해제합니다.  
  
## <a name="using-auto-hide-all"></a>모두 자동 숨기기 사용  
  
#### <a name="to-hide-all-the-tool-windows-at-once"></a>모든 도구 창을 한 번에 숨기려면  
  
1.  **창** 메뉴에서 **모두 자동 숨기기** 를 선택합니다.  
  
