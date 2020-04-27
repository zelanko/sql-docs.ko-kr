---
title: 옵션 (텍스트 편집기-모든 언어-탭 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: bd715d6b-f873-41d4-aa10-57b7098b61cc
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 377ca16075a86c366fcfa8d9d96bcfa989efec4b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089908"
---
# <a name="options-text-editor---all-languages--tabs-page"></a>옵션(텍스트 편집기 - 모든 언어 - 탭 페이지)
  이 대화 상자를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 포함된 5개 편집기 모두의 탭 이동 동작을 설정할 수 있습니다. 이 옵션을 표시하려면 **도구** 메뉴에서 **옵션** 을 클릭하고 **텍스트 편집기** 폴더를 선택한 다음 **모든 언어** 폴더를 확장하고 **탭**을 클릭합니다.  
  
## <a name="tabbing-options-by-editor"></a>편집기별 탭 이동 옵션  
 DMX, MDX 및 SQL Server Compact 편집기에 대해 옵션을 설정하려면 **모든 언어** 대화 상자를 사용해야 합니다. 여기서 설정한 옵션은 일반 텍스트, Transact-SQL 및 XML 편집기에도 적용되지만 이러한 언어에 대한 하위 폴더를 확장하고 해당 옵션 페이지를 선택하여 각 편집기에 대해 옵션을 별도로 설정할 수도 있습니다. 일부 탭 이동 옵션만 지원하는 언어도 있습니다.  
  
> [!CAUTION]  
>  이 대화 상자에서 옵션을 설정하되 일반 텍스트, Transact-SQL 또는 XML 편집기에는 다른 설정을 지정하려면 **모든 언어** 대화 상자에서 선택 항목을 적용한 후에 해당 편집기에 대한 옵션을 설정해야 합니다.  
  
 특정 편집기에 대해 다른 설정을 선택한 경우 "개별 텍스트 형식에 대한 들여쓰기(또는 탭) 설정이 서로 충돌합니다."라는 메시지가 표시됩니다. 예를 들어 **일반 텍스트**에 대해서는 **들여쓰기 차단** 옵션을 선택하고 **XML**에 대해서는 **없음**을 선택하면 이 메시지가 표시됩니다.  
  
## <a name="indenting"></a>들여쓰기  
 **없음**  
 이 옵션을 선택하면 Enter 키를 누를 때 생성되는 새 줄을 들여쓰지 않습니다. 커서는 새 줄의 첫 번째 열에 배치됩니다.  
  
 **거부**  
 이 옵션을 선택하면 Enter 키를 누를 때 생성되는 새 줄을 자동으로 앞 줄과 동일하게 들여씁니다.  
  
 **스마트**  
 이 옵션을 선택하면 Enter 키를 누를 때 생성되는 새 줄의 위치가 컨텍스트에 따라 지정됩니다.  
  
## <a name="tabs"></a>탭  
 **탭 크기**  
 탭 정지 간의 거리를 공백 수로 설정합니다. 기본값은 공백 4개입니다.  
  
 **들여쓰기 크기**  
 자동 들여쓰기의 크기를 공백 수로 설정합니다. 기본값은 공백 4개입니다. 탭 문자나 공백 문자 또는 두 가지 문자 모두를 삽입하여 지정한 크기를 채웁니다.  
  
 **공백 삽입**  
 이 옵션을 선택하면 들여쓰기 작업에서 탭 문자 대신 공백 문자만 삽입합니다. 예를 들어 **들여쓰기 크기**를 5로 설정하면 Tab 키를 누르거나 기본 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 창에서 도구 모음의 **들여쓰기** 단추를 클릭할 때마다 5개의 공백 문자가 삽입됩니다.  
  
 **탭 유지**  
 이 옵션을 선택하면 들여쓰기 작업에서 가능한 한 많은 탭 문자를 삽입합니다. 각 탭 문자는 **탭 크기**에 지정된 공백 수를 채웁니다. **들여쓰기 크기** 가 **탭 크기**의 짝수 배수가 아니면 공백 문자가 추가되어 차이를 메웁니다.  
  
  
