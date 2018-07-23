---
title: '방법: 테이블의 데이터 보기 및 편집 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a52c3875e5b6368a8f5f229dd3309f60bd078fe7
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085335"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>방법: 테이블의 데이터 보기 및 편집
시각적 데이터 편집기를 사용하여 기존 테이블의 데이터를 보고 편집하고 삭제할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 사용합니다.  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>데이터 편집기를 사용하여 테이블의 데이터를 시각적으로 편집하려면  
  
1.  **SQL Server 개체 탐색기**에서 **Products** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.  
  
2.  데이터 편집기가 시작됩니다. 이전 절차에서 테이블에 추가한 행을 살펴봅니다.  
  
3.  SQL Server 개체 탐색기에서 **Fruits** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.  
  
4.  데이터 편집기에서 **Id** 및 **Perishable**에 **1** 및 **True**를 각각 입력한 후 Enter 키나 Tab 키를 눌러 포커스를 새 행의 바깥쪽으로 이동하여 변경 내용을 데이터베이스에 커밋합니다.  
  
5.  위의 단계를 반복하여 테이블에 **2**, **False** 및 **3**, **False**를 입력합니다.  
  
    행을 편집하는 동안 Esc 키를 누르면 항상 셀의 변경 내용을 되돌릴 수 있습니다.  
  
6.  도구 모음의 **스크립트** 단추를 클릭하여 편집 내용을 스크립트로 볼 수 있습니다. 또는 **파일로 스크립트** 단추를 사용하여 편집 내용을 .sql 스크립트 파일에 저장한 후 나중에 실행할 수 있습니다.  
  
7.  **SQL Server 개체 탐색기**에서 **Trade** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**을 선택합니다. 편집기에서 `select * from dbo.PerishableFruits`를 입력하고 **쿼리 실행** 단추를 눌러 `PerishableFruits` 뷰로 표시된 데이터를 반환합니다.  
  
