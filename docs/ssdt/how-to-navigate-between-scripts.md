---
title: '방법: 스크립트 간 이동 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.editor.howto.navigate
ms.assetid: 8664bde5-86ff-4e8b-b5a6-af003316f6ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5ff9e02b15c70d08151384bb46332e8b4ea550a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035161"
---
# <a name="how-to-navigate-between-scripts"></a>방법: 스크립트 간 이동
오프라인 개발을 위한 Transact\-SQL 편집기는 Visual Studio 개발자에게 익숙한 다음 두 개의 유용한 탐색 도구를 제공합니다. 정의로 이동 및 모든 참조 찾기. 예를 들어 테이블 이름을 마우스 오른쪽 단추로 클릭하고 "모든 참조 찾기"를 사용하여 프로젝트의 테이블에 대한 모든 참조를 나열할 수 있습니다. 검색 결과를 두 번 클릭하면 특정 코드 파일로 이동할 수 있습니다. 이 파일에서 테이블 이름을 다시 마우스 오른쪽 단추로 클릭하고 "정의로 이동"을 선택하면 테이블 정의로 다시 이동할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-navigate-between-scripts"></a>스크립트 간을 이동하려면  
  
1.  **솔루션 탐색기**에서 **함수** 폴더를 확장하고 **GetProductsBySupplier.sql**을 두 번 클릭합니다.  
  
2.  이 코드 줄에서 `Products`를 마우스 오른쪽 단추로 클릭하고 **정의로 이동**을 선택합니다.  
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql이 자동으로 열리고 `Products` 형식이 정의된 위치가 표시됩니다.  
  
4.  다시 GetProductsBySupplier.sql로 이동합니다. 이번에는 `Products`의 상황에 맞는 메뉴에서 **모든 참조 찾기**를 선택합니다. **기호 찾기 결과** 창에 `Products` 테이블을 참조하는 위치의 목록이 표시됩니다. 검색 결과를 두 번 클릭하면 참조 위치가 표시됩니다.  
  
