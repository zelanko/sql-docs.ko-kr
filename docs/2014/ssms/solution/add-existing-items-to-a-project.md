---
title: 프로젝트에 기존 항목 추가 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58d94afea9c6801d75a67f6f9136441d536eb696
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62956165"
---
# <a name="add-existing-items-to-a-project"></a>프로젝트에 기존 항목 추가
  프로젝트에 새 항목을 추가하여 애플리케이션 기능을 확장할 수 있습니다. 기존 항목은 쿼리나 기타 파일이 될 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 프로젝트 및 Analysis Services 스크립트 프로젝트의 두 가지 프로젝트 형식이 있습니다. 프로젝트 형식에 따라 프로젝트에 추가할 수 있는 쿼리 파일이 결정됩니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 프로젝트에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리(확장명이 .sql인 파일)를 추가할 수 있지만 Analysis Services 스크립트 프로젝트에는 추가할 수 없습니다. 추가 파일 확장명을 프로젝트 형식에 연결 하려면 [파일 확장명을 코드 편집기에 연결](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)을 참조 하세요.  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>기존 쿼리나 기타 파일을 프로젝트에 추가하려면  
  
1.  솔루션 탐색기에서 대상 프로젝트를 선택합니다.  
  
2.  **프로젝트** 메뉴에서 **기존 항목 추가**를 클릭합니다.  
  
     **Look in**  
     이 목록에서 프로젝트에 추가할 파일 또는 폴더를 찾습니다. XML 웹 서비스와 ASP.NET 웹 애플리케이션의 경우에는 파일이 웹 서버에 있습니다.  
  
     **바탕 화면**  
     바탕 화면에 있는 파일과 폴더를 표시합니다.  
  
     **내 프로젝트**  
     기본 **내 프로젝트** 위치에 있는 파일과 폴더를 표시합니다.  
  
     **내 컴퓨터**  
     **내 컴퓨터** 폴더의 내용을 표시합니다.  
  
     **파일 이름**  
     표시되는 파일과 폴더를 필터링하려면 이 옵션을 사용합니다. 필터링할 파일 이름 전체를 입력하거나 와일드카드 문자로 별표(`*`)를 사용하여 파일 이름 일부를 입력합니다.  
  
    > [!NOTE]  
    >  **파일 이름** 상자에 URL이나 네트워크 경로를 입력하여 웹 및 네트워크 위치로 이동할 수 있습니다. 예를 들어 **http://mywebsite** 를 입력하면 mywebsite 웹 위치에서 사용 가능한 파일이 표시되고 **\\myserver\myshare**의 myserver 위치에서 사용 가능한 파일이 표시됩니다.  
  
     **파일 형식**  
     파일 확장명을 기준으로 파일을 필터링하려면 이 옵션을 사용합니다. 각 제품별로 가장 일반적인 파일 형식에 대한 기본 필터가 나열됩니다.  
  
     **추가**  
     이 드롭다운 단추를 사용하여 프로젝트에 항목을 추가하고 기본 편집기에서 이 항목을 열 수 있습니다.  
  
    -   **추가**  
  
         기존 항목을 디스크의 프로젝트 폴더에 복사하고 솔루션 탐색기에서 선택한 프로젝트에 추가합니다. 항목에서 변경한 내용은 원래 위치에 있는 항목에는 적용되지 않습니다. 이 파일 형식에 대한 기본 편집기입니다.  
  
    -   **링크로 추가**  
  
         선택한 파일을 프로젝트에 추가하고 파일 형식에 대한 기본 편집기로 엽니다. 이 옵션은 원래 선택한 파일을 열고 파일을 프로젝트 폴더로 복사하지 않습니다.  
  
3.  쿼리 파일을 추가하는 경우 쿼리의 연결을 지정하라는 메시지가 연결 대화 상자에 표시됩니다. 연결을 쿼리에 연결하지 않으려는 경우 연결 대화 상자에서 **취소** 를 클릭합니다.  
  
4.  파일은 프로젝트의 **쿼리** 또는 **기타 파일** 폴더에 추가됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [솔루션 탐색기](solution-explorer.md)   
 [프로젝트에 새 항목 추가](add-new-items-to-a-project.md)   
 [항목이나 프로젝트 제거 또는 삭제](remove-or-delete-an-item-or-project.md)  
  
  
