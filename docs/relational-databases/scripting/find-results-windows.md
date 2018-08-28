---
title: 찾기 결과 창 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.findresults1
- findresultswindow
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 721da2d2aa2731427455a30a1d691f1a644d95a0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067551"
---
# <a name="find-results-windows"></a>찾기 결과 창
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  두 개의 찾기 결과 창에는 **찾기 및 바꾸기** 대화 상자의 **파일에서 찾기** 또는 **파일에서 바꾸기** 탭을 사용하여 찾은 항목이 표시됩니다. **파일에서 찾기** 와 **파일에서 바꾸기** 의 **결과 옵션** 명령을 사용하여 항목을 표시할 찾기 결과 창을 선택할 수 있습니다.  
  
 이렇게 하면 항목을 찾을 때마다 자동으로 선택한 찾기 결과 창이 열립니다. 찾기 결과 창을 수동으로 표시하려면 **보기** 메뉴에서 **다른 창** 을 클릭한 다음 **찾기 결과 1** 이나 **찾기 결과 2**를 클릭합니다.  
  
 코드 파일을 표시하고 항목이 있는 줄로 이동하려면 결과 목록에서 해당 줄을 두 번 클릭합니다. 그러면 코드 편집기에 원본 파일이 표시되고 삽입 지점은 일치하는 텍스트가 시작하는 위치에 표시됩니다. 편집기의 표시기 여백에는 일치하는 항목이 있는 줄을 표시하는 기호가 나타나고 상태 표시줄에는 전체 텍스트가 표시됩니다.  
  
## <a name="toolbar-buttons"></a>도구 모음 단추  
 다음 도구 모음 단추를 사용하여 결과 목록을 검색하고 항목이 있는 코드 줄로 이동할 수 있습니다.  
  
 **페이지 플래그+위쪽 화살표**  
 선택한 항목이 있는 줄로 이동합니다.  
  
 **페이지+왼쪽 화살표**  
 이전 항목이 있는 줄로 이동합니다.  
  
 **페이지+오른쪽 화살표**  
 다음 항목이 있는 줄로 이동합니다.  
  
 **모두 지우기**  
 **결과** 목록에서 항목을 모두 제거합니다.  
  
## <a name="shortcut-keys"></a>바로 가기 키  
 다음 바로 가기 키를 사용하여 항목 간에 빠르게 이동할 수 있습니다.  
  
 Ctrl+Home  
 찾기 결과 창 맨 위로 스크롤합니다.  
  
 Ctrl+End  
 찾기 결과 창 맨 아래로 스크롤합니다.  
  
 Page Up  
 다음 항목 그룹까지 위로 스크롤합니다.  
  
 Page Down  
 다음 항목 그룹까지 아래로 스크롤합니다.  
  
 위쪽 화살표  
 이전 항목을 선택합니다.  
  
 아래쪽 화살표  
 다음 항목을 선택합니다.  
  
## <a name="search-result-entries"></a>검색 결과 항목  
 결과 목록의 각 항목은 다음 정보를 제공합니다.  
  
-   전체 경로  
  
-   파일 이름   
  
-   줄 번호  
  
-   항목이 있는 줄의 전체 텍스트  
  
> [!TIP]  
>  **빠른 찾기** 를 사용하여 길이가 긴 결과 목록을 검색할 수 있습니다. 찾기 결과 창을 열어 도킹한 다음 **찾기** 탭의 삼각형 **보기** 단추를 클릭하고 **빠른 찾기**로 전환합니다. 검색의 **찾는 위치** 필드를 **활성 창**으로 설정하고 **찾을 내용** 문자열을 입력한 후 **다음 찾기**를 클릭합니다. 이렇게 하면 결과 목록에서 특정 폴더나 파일에서 찾은 항목이나 다른 중요한 용어가 포함된 코드 줄을 검색할 수 있습니다.  
  
## <a name="summary-lines"></a>요약 줄  
 각 검색 결과 집합은 검색 매개 변수를 나타내는 줄로 시작하여 통계 줄로 끝납니다. 예를 들어 **파일에서 찾기** 검색 기능을 사용하여 열려 있는 모든 문서에서 "`var[1-3]&par`" 정규식과 일치하는 문자열이 있는지 검색한 결과 목록은 다음과 같은 검색 매개 변수 줄로 시작합니다.  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 그리고 다음과 같은 통계 줄로 끝납니다.  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 **파일에서 바꾸기** 검색 기능을 사용하여 열려 있는 모든 문서에서 "`var[1-3]&par`" 정규식과 일치하는 일치하는 문자열을 "`sample`" 문자열로 바꾼 결과 목록은 다음 검색 매개 변수 줄로 시작합니다.  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 그리고 다음과 같은 통계 줄로 끝납니다.  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
  
  
