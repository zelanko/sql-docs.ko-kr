---
title: Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e348fba8c391b438c0429c8a32e167fd810b53d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102068"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행
Transact\-SQL 편집기에서는 스크립트 작업에 사용할 수 있는 다양한 기능의 편집 및 디버깅 환경을 제공합니다. 이 편집기는 **코드 보기** 상황에 맞는 메뉴를 사용하여 연결된 데이터베이스 또는 프로젝트의 데이터베이스 엔터티를 열 때 호출됩니다. SQL Server 개체 탐색기의 **새 쿼리** 상황에 맞는 메뉴를 사용하거나 데이터베이스 프로젝트에 새 스크립트 개체를 추가하는 경우에도 이 편집기가 자동으로 열립니다.  
  
데이터베이스에 연결되어 있지 않지만 데이터베이스에 쿼리를 실행하려면 **SQL** -> **Transact\-SQL** 편집기 메뉴 옵션의 **새 쿼리 연결** 대화 상자를 사용하여 데이터베이스에 연결하고 Transact\-SQL 편집기를 시작할 수 있습니다.  
  
Transact\-SQL 편집기에는 Transact\-SQL 스크립트를 작성하고 편집하는 데 사용할 수 있는 주 **T-SQL** 창이 포함되어 있습니다. 이 편집기에서는 IntelliSense뿐 아니라 복잡한 문을 보기 쉽게 하기 위한 구문 색 구분 표시도 지원합니다. 또한 찾기 및 바꾸기, 대량 주석 달기, 사용자 지정 글꼴 및 색, 줄 번호 매기기를 지원합니다. 편집기의 스크립트를 실행할 대상 데이터베이스를 변경할 수도 있습니다. 자세한 내용은 [방법: 기존 데이터베이스 복제](../ssdt/how-to-clone-an-existing-database.md)를 참조하세요. **결과** 창에는 쿼리 결과가 표나 텍스트로 표시됩니다. 쿼리 결과를 파일로 리디렉션할 수도 있습니다. **메시지** 창에는 스크립트가 실행될 때 반환된 오류, 경고 및 정보 메시지가 표시됩니다. 클라이언트 통계를 사용하도록 설정한 경우 **통계** 창에는 쿼리 실행에 대한 정보가 범주별로 그룹화되어 표시됩니다. **실행 계획** 창에는 SQL Server가 선택한 데이터 검색 방법과 특정 문 및 쿼리의 실행 비용이 표시됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|---------|---------------|  
|[방법: 코드 조각 개요 표시 및 Transact-SQL 스크립트에 코드 조각 추가](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|코드 조각 선택기를 사용하여 만들어 둔 Transact\-SQL 코드를 쿼리에 삽입합니다.|  
|[방법: 스크립트 간 이동](../ssdt/how-to-navigate-between-scripts.md)|정의로 이동 및 모든 참조 찾기를 사용하여 스크립트 간을 이동합니다.|  
|[방법: 이름 바꾸기 및 리팩터링을 사용하여 데이터베이스 개체 변경](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|모든 스크립트에서 개체의 이름을 바꾸고 변경 내용을 미리 봅니다.|  
|[방법: 부분 쿼리 실행](../ssdt/how-to-execute-a-partial-query.md)|스크립트의 특정 세그먼트를 강조 표시하고 이를 단일 쿼리로 실행합니다.|  
|[방법: 저장된 프로시저 디버깅](../ssdt/how-to-debug-stored-procedures.md)|Transact\-SQL 저장 프로시저를 만들고 이를 한 단계씩 실행하여 디버그합니다.|  
|[스크립트 성능 분석](../ssdt/analyze-script-performance.md)|실행 계획, 클라이언트 통계 및 코드 분석을 사용하여 쿼리, 저장 프로시저 또는 스크립트의 성능을 향상시킬 수 있는지 여부를 확인합니다.|  
  
## <a name="see-also"></a>참고 항목  
[방법: 쿼리를 사용하여 새 데이터베이스 개체 만들기](../ssdt/how-to-create-new-database-objects-using-queries.md)  
  
