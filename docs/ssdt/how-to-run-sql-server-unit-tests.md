---
title: SQL Server 단위 테스트 실행
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 3ee95885dc1696fd7fba80342dc8c582a79056cc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244277"
---
# <a name="how-to-run-sql-server-unit-tests"></a>방법: SQL Server 단위 테스트 실행

다양한 창 및 명령 프롬프트 창을 사용하는 등 여러 방법 중 하나로 SQL Server 단위 테스트를 실행할 수 있습니다.  
  
> [!NOTE]  
> 단위 테스트를 원격으로 실행할 수는 없습니다.  
  
사용할 수 있는 방법은 [SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)에 설명된 대로 설치한 소프트웨어에 따라 달라집니다.  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>테스트 뷰를 사용하여 SQL Server 단위 테스트를 실행하려면(Visual Studio 2010)  
  
1.  **테스트** 메뉴에서 **창**을 가리킨 후 **테스트 뷰**를 클릭합니다.  
  
    **테스트 뷰** 창이 열립니다.  
  
2.  **테스트 뷰** 창에서 실행하려는 테스트를 클릭합니다. Ctrl 키 또는 Shift 키를 사용하여 불연속 또는 연속된 테스트 블록을 지정할 수 있습니다.  
  
3.  다음 중 하나를 수행합니다.  
  
    -   **테스트 뷰** 창의 표면을 마우스 오른쪽 단추로 클릭한 후 **선택 항목 실행**을 클릭합니다.  
  
    -   **테스트 뷰** 도구 모음에서 **선택 항목 실행**을 클릭합니다.  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>테스트 탐색기를 사용하여 SQL Server 단위 테스트를 실행하려면(Visual Studio 2012)  
  
1.  **테스트** 메뉴에서 **창**을 가리킨 다음, **테스트 탐색기**를 클릭합니다.  
  
    **테스트 탐색기** 창이 열립니다.  
  
2.  **테스트 탐색기**에서 실행하려는 테스트를 클릭합니다. Ctrl 키 또는 Shift 키를 사용하여 불연속 또는 연속된 테스트 블록을 지정할 수 있습니다.  
  
3.  강조 표시된 테스트 중 하나를 마우스 오른쪽 단추로 클릭하고 **선택한 테스트 실행**을 클릭합니다.  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>SQL Server 단위 테스트 디자이너에서 SQL Server 단위 테스트를 실행하려면(Visual Studio 2010)  
  
-   **테스트 도구** 도구 모음의 단추를 클릭하여 디버거를 사용하거나 사용하지 않고 프로젝트를 시작합니다.  
  
이 단계에서는 현재 테스트 실행에 포함된 모든 테스트를 실행합니다. 테스트 실행을 시작하는 즉시 **테스트 결과** 창이 나타나고 테스트 실행 진행률이 표시됩니다. 여기에는 실행 중인 테스트 및 완료된 테스트가 포함됩니다. 자세한 내용은 [SQL Server 단위 테스트 결과 해석](../ssdt/interpreting-sql-server-unit-test-results.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)  
[방법: Microsoft Visual Studio 2010에서 자동화된 테스트 실행](https://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[명령줄에서 자동화된 테스트 실행(Visual Studio 2010)](https://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[애플리케이션 테스트(Visual Studio 2012)](https://msdn.microsoft.com/library/ms182409.aspx)  
  
