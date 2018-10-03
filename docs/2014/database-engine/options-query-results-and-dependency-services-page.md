---
title: 옵션 (쿼리 결과 및 종속성 서비스 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
author: mashamsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f587ee792809f9612ca9fca1264794e843172a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118623"
---
# <a name="options-query-results-and-dependency-services-page"></a>옵션(쿼리 결과 및 종속성 서비스 페이지)
  이 페이지를 사용하여 종속성 서비스를 위해 연결할 서버를 지정할 수 있습니다. 종속성 서비스를 사용하면 서로 다른 서버에 저장된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체 간의 종속성에 대한 정보를 추출할 수 있습니다. 사용 하 여 개체 종속성을 확인 합니다 **개체 종속성** 대화 상자 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]합니다.  
  
 **수행 작업**  
  
1.  [옵션 (쿼리 결과/종속성 서비스 페이지) 대화 상자를 열려면](#open_dialog)  
  
2.  [옵션 구성](#options)  
  
##  <a name="open_dialog"></a> 옵션 (쿼리 결과/종속성 서비스 페이지) 대화 상자를 열려면  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], 클릭 **옵션** 에 **도구** 메뉴.  
  
2.  **쿼리 결과**를 확장하고 **종속성 서비스**를 클릭합니다.  
  
##  <a name="options"></a> 옵션 구성  
  
### <a name="options"></a>변수  
 **종속성 서비스 서버**  
 종속성 서비스가 설치된 서버를 지정합니다.  
  
 **인증**  
 Microsoft Windows 사용자 계정을 사용하여 로그온하려면 Windows 인증을 선택하고, 그렇지 않으면 SQL Server 인증을 선택합니다.  
  
 사용자가 트러스트되지 않은 연결에서 지정한 로그인 이름과 암호를 사용하여 연결하면 SQL Server에서는 SQL Server 로그인 계정이 설정되었는지 여부와 지정한 암호가 이전에 기록한 암호와 일치하는지 여부를 확인하여 인증을 수행합니다. SQL Server에서 로그인 계정을 찾을 수 없으면 인증이 실패하고 사용자에게 오류 메시지가 표시됩니다.  
  
 **사용자 이름**  
 SQL Server 인증을 사용하는 경우 사용자 이름을 입력합니다.  
  
 **암호**  
 SQL Server 인증을 사용하는 경우 암호를 입력합니다.  
  
 **테스트**  
 연결을 테스트하려면 클릭합니다.  
  
  
