---
title: '방법: 프로젝트의 스냅샷 만들기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.SqlProjectImportSnapshotSummaryDialog.dialog
- sql.data.tools.SqlProjectImportSnapshotDialog.dialog
ms.assetid: bed670a3-13bd-4d88-91a1-58d5b9524a97
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3fad9b94c83a314ab252ed52377d6fb332e7029e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897202"
---
# <a name="how-to-create-a-snapshot-of-a-project"></a>방법: 프로젝트의 스냅샷 만들기
**데이터 계층 애플리케이션** 파일은 데이터베이스 스키마를 만들 때의 읽기 전용 표현을 제공합니다. 이 파일은 기본적으로 데이터베이스 스키마로 처리되며, 이 스키마의 스키마 개체를 다시 프로젝트로 가져올 수 있습니다. 또한 스냅샷을 데이터베이스 또는 프로젝트의 스키마와 비교하고, 스냅샷에 정의된 스키마를 반영하도록 데이터베이스나 프로젝트를 업데이트할 수도 있습니다.  
  
원본 데이터베이스 프로젝트에서 사용자 오류가 발생할 경우 스냅샷을 생성했을 때의 상태로 원본 프로젝트를 되돌릴 수 있습니다. 기본적인 목적을 위해 다양한 개발 단계에서 스냅샷을 설정할 수도 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 활용합니다.  
  
### <a name="to-create-a-snapshot"></a>스냅샷을 만들려면  
  
1.  **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **데이터 계층 애플리케이션(\*.dacpac)…** 을 선택합니다.  
  
2.  SSDT에서는 먼저 프로젝트를 빌드하려고 시도합니다. 빌드 오류가 없으면 **스냅샷** 폴더가 **솔루션 탐색기**에 만들어집니다. SSDT를 통해 이 폴더 안에 “<Project Name>_YYYYMMDD_HH-MM-SS.dacpac” 형식의 이름을 사용하는 .dacpac 파일이 만들어집니다.  
  
3.  .dacpac 파일을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다. 기본 파일 이름을 "TradeDev1.dacpac"로 바꿉니다.  
  
4.  **솔루션 탐색기**에서 **GetProductsBySupplier** 함수를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택하여 이 함수를 프로젝트에서 제거합니다.  
  
5.  이전 단계에 따라 **TradeDev2.dacpac**라는 새 스냅샷을 만듭니다.  
  
### <a name="to-import-a-snapshot"></a>스냅샷을 가져오려면  
  
1.  **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **가져오기** 및 **데이터 계층 애플리케이션(\*.dacpac)…** 을 차례로 선택합니다.  
  
2.  **데이터 계층 애플리케이션 가져오기** 대화 상자에서 **찾아보기**를 클릭하여 가져오기의 원본으로 사용할 **TradeDev1.dacpac**를 선택합니다.  
  
    현재 프로젝트가 기본 대상이므로 **대상 프로젝트** 섹션은 사용하지 않도록 설정되어 있습니다. **시작**을 클릭하여 가져오기를 시작합니다.  
  
3.  **요약** 페이지에서 **마침**을 클릭합니다. **솔루션 탐색기**에서 삭제된 테이블이 프로젝트에 복원되었는지 확인합니다.  
  
    > [!WARNING]  
    > 스냅샷 가져오기를 수행하면 스냅샷 스키마의 모든 데이터베이스 엔터티를 프로젝트로 가져오게 됩니다. 그 결과 중복 엔터티가 만들어질 수도 있습니다. 예를 들어 각 테이블 및 보기에는 이제 <ObjectName_1>이라는 자체 복사본이 추가로 포함되어 있습니다. **솔루션 탐색기**에서 이러한 각 중복 개체를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택하여 이 개체를 프로젝트에서 제거합니다.  
  
### <a name="to-compare-snapshots"></a>스냅샷을 비교하려면  
  
1.  솔루션 탐색기에서 **TradeDev1.dacpac**를 마우스 오른쪽 단추로 클릭하고 **스키마 비교**를 선택합니다. **스키마 비교** 창이 열립니다.  
  
2.  **데이터 계층 애플리케이션 파일** 옵션을 사용하여 원본 및 대상 스키마를 설정합니다. **원본 스키마**를 **데이터 계층 애플리케이션 파일**의 **TradeDev1.dacpac**로 설정하고 **대상 스키마**를 **TradeDev2.dacpac**로 설정해야 합니다.  
  
3.  **확인**을 클릭하여 비교를 시작합니다. 삭제된 함수가 이전 스냅샷과 새 스냅샷의 차이로 강조 표시됩니다.  
  
    스키마 비교 기능을 사용하면 서로 다른 스냅샷 간의 차이를 쉽게 찾을 수 있습니다. 이 경우 개발 과정 중에 프로젝트가 어떻게 전개되었는지 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
