---
title: '방법: 기존 데이터베이스 복제 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: aad3594a-11cf-4e68-a622-071a93d43875
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d32b782c8508952a85f0a9a22b55d32dab096d6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017621"
---
# <a name="how-to-clone-an-existing-database"></a>방법: 기존 데이터베이스 복제
이 작업에서는 이전 절차에서 배운 단계 중 일부를 사용하여 새 데이터베이스를 만들고 기존 데이터를 이식합니다. 또한 [방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)에 설명된 단계를 사용하여 소스 및 프로젝트 데이터베이스의 스키마를 동기화합니다.  
  
이러한 단계를 사용하면 프로덕션 데이터베이스에서 스키마 및 데이터가 동일한 개발 또는 테스트 데이터베이스를 손쉽게 만들 수 있습니다. 그런 다음 프로덕션 데이터베이스의 작업을 전혀 방해하지 않고 연결된 모드에서 테스트 데이터베이스를 계속해서 개발하거나 오프라인 개발 및 테스트를 위한 데이터베이스 프로젝트를 만들 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 사용합니다.  
  
### <a name="to-create-a-development-database"></a>개발 데이터베이스를 만들려면  
  
1.  **SQL Server 개체 탐색기**의 **SQL Server** 노드에서 연결된 서버 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스 추가**를 선택합니다.  
  
3.  새 데이터베이스의 이름을 **TradeDev**로 바꿉니다.  
  
4.  **SQL Server 개체 탐색기**에서 **Trade** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **스키마 비교**를 선택합니다. [방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md) 항목의 단계에 따라 원래 **Trade** 데이터베이스를 소스로 선택하고 새 **TradeDev** 데이터베이스를 대상으로 선택합니다. 그러면 **TradeDev**가 **Trade**의 스키마로 업데이트됩니다.  
  
### <a name="to-replicate-data"></a>데이터를 복제하려면  
  
1.  이전 단계에서는 프로덕션 데이터베이스의 스키마만 개발 데이터베이스로 복제했습니다. 이 절차에서는 프로덕션 데이터를 개발 데이터베이스로 복제합니다.  
  
    **Trade** 데이터베이스의 **Suppliers** 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다. 데이터 편집기가 열립니다.  
  
2.  도구 모음에서 **최대 행 수** 옆의 **스크립트** 단추를 클릭합니다.  
  
3.  스크립트 창이 열리면 Transact\-SQL 스크립트 창 아래의 상태 표시줄에 연결됨이 표시되는지 확인합니다. 연결 끊김이 표시된 경우 도구 모음의 가장 왼쪽에 있는 **연결** 단추를 클릭하고 서버 정보 및 자격 증명을 입력합니다.  
  
4.  **연결**/**연결 끊기** 단추 옆의 **데이터베이스** 드롭다운 메뉴에서 **TradeDev**를 선택합니다. 이 방법은 Transact\-SQL `USE` 문을 사용하는 것과 비슷하며, 코드 편집기의 스크립트가 **TradeDev** 데이터베이스에 대해 실행되도록 합니다.  
  
5.  **쿼리 실행** 단추를 클릭하여 `INSERT` 문을 실행합니다. 그러면 `Suppliers` 데이터베이스의 `Trade` 테이블에 있는 모든 행이 `Suppliers` 데이터베이스의 `TradeDev` 테이블에 삽입됩니다.  
  
6.  `Trade` 데이터베이스의 모든 테이블에 대해 위의 단계를 반복하여 모든 테이블을 `TradeDev` 데이터베이스로 복제합니다.  
  
7.  데이터 편집기를 사용하여 새 `TradeDev` 데이터베이스의 모든 테이블이 채워졌는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
