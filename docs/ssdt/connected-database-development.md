---
title: 연결된 데이터베이스 개발 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLSERVEROBJECTEXPLORER
ms.assetid: 21f7f959-7b8e-4335-8681-bebcd957692c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 536dbcddf73d8b6af5e1106a7eb279cc1db22f47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655891"
---
# <a name="connected-database-development"></a>연결된 데이터베이스 개발
이 섹션에서는 SQL Server Data Tools에서 연결된 데이터베이스를 디자인하고 쿼리하는 용도로 제공되는 기능에 대해 설명합니다.  
  
이제 개발자는 Visual Studio의 SQL Server 개체 탐색기를 사용하여 SQL Server 2008 또는 Microsoft SQL Server 2012와 같은 내부 데이터베이스 서버나 SQL Azure의 외부 데이터베이스 서버에서 데이터베이스 개체를 만들고 편집하고 탐색할 수 있습니다. 또한 손쉽게 기존 프로덕션 데이터베이스를 테스트 인스턴스에 복제하고, 이 인스턴스에서 추가 개발 작업을 수행한 다음, 변경 내용을 다시 프로덕션 데이터베이스에 게시할 수 있습니다.  
  
> [!NOTE]  
> 이 섹션의 방법 도움말 항목에는 순서대로 완료할 수 있는 일련의 작업이 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|---------|---------------|  
|[방법: 데이터베이스에 연결 및 기존 개체 찾아보기](../ssdt/how-to-connect-to-a-database-and-browse-existing-objects.md)|데이터베이스에 연결하고 해당 엔터티를 찾습니다.|  
|[방법: 테이블 디자이너를 사용하여 데이터베이스 개체 만들기](../ssdt/how-to-create-database-objects-using-table-designer.md)|새 테이블 디자이너를 사용하여 테이블을 디자인하고 테이블 관계를 관리합니다.|  
|[방법: 파워 버퍼를 사용하여 연결된 데이터베이스 업데이트](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)|ALTER 스크립트를 작성하지 않고 연결된 데이터베이스를 업데이트합니다.|  
|[필터 및 정렬 대화 상자](../ssdt/filter-and-sort-dialog-box.md)|데이터 뷰에 표시되어야 하는 데이터를 지정합니다.|  
|[방법: 쿼리를 사용하여 새 데이터베이스 개체 만들기](../ssdt/how-to-create-new-database-objects-using-queries.md)|Transact\-SQL 편집기를 사용하여 Transact\-SQL 스크립트 편집 및 실행|  
|[방법: 쿼리를 사용하여 기존 테이블 편집](../ssdt/how-to-edit-an-existing-table-using-queries.md)|Transact\-SQL 스크립트를 작성하여 테이블의 정의를 편집하거나 데이터를 채웁니다.|  
|[방법: 테이블의 데이터 보기 및 편집](../ssdt/how-to-view-and-edit-data-in-a-table.md)|데이터 편집기를 사용하여 테이블의 데이터를 보거나 입력합니다.|  
|[방법: 개체 삭제 및 종속성 해결](../ssdt/how-to-delete-objects-and-resolve-dependencies.md)|데이터베이스 엔터티를 이름을 바꾸거나 삭제하고 SQL Server Data Tools에서 자동으로 개체 종속성을 확인할 수 있도록 합니다.|  
|[방법: 기존 데이터베이스 복제](../ssdt/how-to-clone-an-existing-database.md)|프로덕션 데이터베이스에서 개발 데이터베이스를 만듭니다.|  
|[.dacpac 파일 추출, 게시 및 등록](../ssdt/extract-publish-and-register-dacpac-files.md)|.dacpac 파일을 추출하고 게시하는 방법을 보여 줍니다.|  
  
## <a name="related-sections"></a>관련 섹션  
[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
