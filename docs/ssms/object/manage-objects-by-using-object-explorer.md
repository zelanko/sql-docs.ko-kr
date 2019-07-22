---
title: 개체 탐색기를 사용하여 개체 관리 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb52261160cc693193e4cc983a4c2e28baa28686
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264101"
---
# <a name="manage-objects-by-using-object-explorer"></a>개체 탐색기를 사용하여 개체 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
개체 탐색기를 사용하여 데이터베이스, 테이블 및 저장 프로시저와 같은 개체를 관리할 수 있습니다.  
  
## <a name="viewing-objects-in-object-explorer"></a>개체 탐색기에서 개체 보기  
개체 탐색기는 트리 구조를 사용하여 정보를 폴더로 그룹화합니다. 폴더를 확장하려면 더하기 기호(+)를 클릭하거나 폴더를 두 번 클릭합니다. 폴더를 확장하여 더 자세한 정보를 표시합니다. 일반적인 태스크를 수행하려면 폴더나 개체를 마우스 오른쪽 단추로 클릭하고, 가장 일반적인 태스크를 수행하려면 개체를 두 번 클릭합니다.  
  
폴더를 처음 확장하면 개체 탐색기는 서버에 트리를 채우기 위한 정보를 쿼리합니다. 트리가 채워지는 동안 다른 기능을 수행할 수 있습니다. 개체 탐색기가 트리를 채우는 동안 **중지** 를 클릭하여 프로세스를 중단할 수 있습니다. 채우기를 다시 시작하도록 폴더를 새로 고치지 않을 경우 추가 동작(예: 목록 필터링)을 수행하면 채워진 폴더의 일부분에 대해서만 해당 작업이 적용됩니다.  
  
개체가 많을 경우 리소스를 절약하기 위해 개체 탐색기 트리의 폴더는 콘텐츠 목록을 자동으로 새로 고치지 않습니다. 폴더의 개체 목록을 새로 고치려면 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새로 고침**을 클릭합니다.  
  
개체 탐색기는 최대 65,536개의 개체만 표시할 수 있습니다. 표시되는 개체가 65,536개를 초과하면 개체 탐색기 트리 뷰에서 추가 개체를 스크롤할 수 없습니다. 개체 탐색기에서 추가 개체를 보려면 사용하지 않는 노드를 닫거나 필터링을 적용하여 개체 수를 줄입니다.  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>개체 탐색기에서 개체 목록 필터링  
폴더에 개체가 많이 있으면 개체를 찾는 것이 어려울 수 있습니다. 이러한 경우에는 개체 탐색기의 필터 기능을 사용하여 목록의 크기를 줄입니다. 예를 들어 수백 개의 개체가 포함된 목록에서 특정 데이터베이스 사용자나 가장 최근에 만든 테이블을 찾을 수 있습니다. 이러한 경우에는 필터링할 폴더를 클릭한 다음 필터 단추를 클릭하여 **필터 설정** 대화 상자를 엽니다. 이름, 만든 날짜, 스키마 등으로 목록을 필터링할 수 있으며 **시작**, **포함**, **사이**등의 추가 필터링 연산자를 제공할 수 있습니다.  
  
## <a name="multi-select"></a>다중 선택  
개체 탐색기에서는 한 번에 하나의 개체만 선택할 수 있습니다. 여러 항목을 선택하려면 **F7** 키를 눌러 **개체 탐색기 정보 페이지**를 엽니다. **개체 탐색기 정보 페이지** 에서는 다중 선택이 지원됩니다.  
  
## <a name="register-a-server-from-object-explorer"></a>개체 탐색기에서 서버 등록  
서버에 연결되면 이후에 사용할 수 있도록 서버를 쉽게 등록할 수 있습니다. 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **등록**을 클릭합니다. **서버 등록** 대화 상자에서 서버를 배치할 서버 그룹 트리 내 위치를 지정합니다. **서버 이름** 상자에서 서버 이름을 보다 알기 쉬운 이름으로 대체할 수 있습니다. 예를 들어 **APSQL02** 서버를 "**Accounts Payable**"과 같은 보다 알기 쉬운 이름으로 등록할 수 있습니다.  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>개체 탐색기 노드에서 동작 수행  
개체를 나타내는 개체 탐색기 노드를 마우스 오른쪽 단추로 클릭하여 개체에 대한 동작을 수행할 수 있습니다. 각 개체 유형은 고유한 마우스 오른쪽 단추 클릭 동작 집합을 지원합니다. 오른쪽 클릭 메뉴를 사용하여 수행할 수 있는 동작 유형에는 다음이 포함됩니다.  
  
### <a name="open-a-connected-query-editor"></a>연결된 쿼리 편집기 열기  
개체 탐색기가 서버에 연결되면 개체 탐색기의 연결 설정을 사용하여 새 코드 편집기 창을 열 수 있습니다. 새 코드 편집기 창을 열려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다. 특정 데이터베이스를 사용하여 코드 편집기 창을 열려면 데이터베이스 이름을 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다. Analysis Services 서버에 대한 새 쿼리를 열 경우 DMX, MDX 또는 XMLA 쿼리를 선택할 수 있습니다.  
  
### <a name="start-powershell"></a>PowerShell 시작  
개체 탐색기 트리에서 대부분의 폴더 및 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하면 PowerShell 세션을 시작할 수 있습니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 지원이 활성화되고 개체 탐색기에서 마우스 오른쪽 단추로 클릭한 개체로 경로가 설정되어 PowerShell 세션이 시작됩니다. 그러면 대화형 PowerShell 환경에서 PowerShell 명령을 입력할 수 있습니다. 자세한 내용은 [SQL Server PowerShell](https://msdn.microsoft.com/89b70725-bbe7-4ffe-a27d-2a40005a97e7)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[개체 탐색기](../../ssms/object/object-explorer.md)  
[개체 탐색기 열기 및 구성](../../ssms/object/open-and-configure-object-explorer.md)  
[개체 탐색기에서 인스턴스에 연결](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[개체 탐색기 세부 정보 창](../../ssms/object/object-explorer-details-pane.md)  
[Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)  
  
