---
title: Management Studio에 사용자 지정 보고서 추가 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a860db611154f9f7a130ee6be90dd43a96b50af5
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618130"
---
# <a name="add-a-custom-report-to-management-studio"></a>Management Studio에 사용자 지정 보고서 추가
  이 항목에서는 .rdl 파일로 저장되는 간단한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 만든 다음 이 rdl 파일을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 사용자 지정 보고서로 추가하는 방법에 대해 설명합니다. [!INCLUDE[ssRS](../../includes/ssrs.md)] 다양한 고급 보고서를 만들 수 있습니다. 이 항목을 사용하여 보고서를 만들려면 컴퓨터에 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 가 설치되어 있어야 합니다. [!INCLUDE[ssRS](../../includes/ssrs.md)] 를 사용하여 사용자 지정 보고서를 실행하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 설치할 필요는 없습니다.  
  
  
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>.rdl 파일로 저장되는 간단한 보고서를 만들려면  
  
1.  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server**를 차례로 가리킨 후 **SQL Server Data Tools**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
3.  **프로젝트 형식** 목록에서 **비즈니스 인텔리전스 프로젝트**를 클릭합니다.  
  
4.  **템플릿** 목록에서 **보고서 서버 프로젝트 마법사**를 클릭합니다.  
  
5.  **이름**에 **ConnectionsReport**를 입력한 다음 **확인**을 클릭합니다.  
  
6.  **보고서 마법사** 시작 페이지에서 **다음**을 클릭합니다.  
  
7.  **데이터 원본 선택** 페이지의 이름 입력란에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 이 연결의 이름을 입력한 다음 **편집**을 클릭합니다.  
  
8.  **연결 속성** 대화 상자의 **서버 이름** 입력란에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스 이름을 입력합니다.  
  
9. **데이터베이스 이름 선택 또는 입력** 상자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 있는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]등의 데이터베이스 이름을 입력한 다음 **확인**을 클릭합니다.  
  
10. **데이터 원본 선택** 페이지에서 **다음**을 클릭합니다.  
  
11. **쿼리 디자인** 페이지의 **쿼리 문자열** 입력란에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대한 현재 연결을 나열하는 다음 [!INCLUDE[ssDE](../../includes/ssde-md.md)]문을 입력한 후 **다음**을 클릭합니다. 보고서 마법사 쿼리 문자열 입력란에는 보고서 매개 변수를 사용할 수 없습니다. 더 복잡한 사용자 지정 보고서는 수동으로 만들어야 합니다.  
  
     `SELECT session_id, net_transport FROM sys.dm_exec_connections;`  
  
12. **보고서 유형 선택** 페이지에서 **테이블 형식**을 선택한 다음 **마침**을 클릭합니다.  
  
13. **마법사 완료** 페이지의 **보고서 이름** 입력란에 **ConnectionsReport**를 입력한 다음 **마침** 을 클릭하여 보고서를 만들고 저장합니다.  
  
14. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 닫습니다.  
  
15. 사용자 지정 보고서를 위해 데이터베이스 서버에 만든 폴더에 **ConnectionsReport.rdl** 을 복사합니다.  
  
### <a name="to-add-a-report-to-management-studio"></a>Management Studio에 보고서를 추가하려면  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 개체 탐색기의 노드를 마우스 오른쪽 단추로 클릭하고 **보고서**를 가리킨 다음 **사용자 지정 보고서**를 클릭합니다. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾고 **ConnectionsReport.rdl** 파일을 선택한 다음 **열기**를 클릭합니다.  
  
     개체 탐색기 노드에서 새 사용자 지정 보고서를 처음으로 열면 해당 노드의 바로 가기 메뉴에 있는 **사용자 지정 보고서** 의 가장 최근에 사용한 목록에 이 보고서가 추가됩니다. 표준 보고서를 처음으로 열면 이 보고서도 **사용자 지정 보고서**의 가장 최근에 사용한 목록에 표시됩니다. 사용자 지정 보고서 파일을 삭제하면 다음에 이 항목을 선택할 때 가장 최근에 사용한 목록에서 해당 항목을 삭제하라는 메시지가 표시됩니다.  
  
    1.  최근에 사용한 목록에 표시되는 파일 수를 변경하려면 **도구** 메뉴에서 **옵션** 을 클릭하고 **환경** 폴더를 확장한 다음 **일반**을 클릭합니다.  
  
    2.  **최근 사용 목록에 n개 파일 표시**의 개수를 조정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Management Studio의 사용자 지정 보고서](custom-reports-in-management-studio.md)   
 [개체 탐색기 노드 속성과 함께 사용자 지정 보고서 사용](use-custom-reports-with-object-explorer-node-properties.md)   
 [사용자 지정 보고서 실행된 경으십시오](unsuppress-run-custom-report-warnings.md)   
 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
