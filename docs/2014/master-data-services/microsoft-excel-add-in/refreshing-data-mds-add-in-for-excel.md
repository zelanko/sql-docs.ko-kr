---
title: 데이터 새로 고침(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 58dbe99a-288d-4f1c-9cd5-704d6836c945
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 126c696da22e2b3e483ae7fb4692469d617f125a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089945"
---
# <a name="refreshing-data-mds-add-in-for-excel"></a>데이터 새로 고침(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서는 데이터를 새로 고쳐 새 워크시트를 열지 않고도 MDS 리포지토리에서 최신 정보를 가져올 수 있습니다. 모든 셀이나 선택한 셀을 새로 고칠 수 있습니다. 이 방법은 사용자 지정 수식이나 MDS에서 관리되지 않는 기타 데이터가 포함된 열을 삽입했으며 이를 보존하려는 경우에 유용하게 사용할 수 있습니다.  
  
## <a name="when-you-can-refresh-mds-managed-data"></a>MDS 관리 데이터를 새로 고칠 수 있는 경우  
 활성 워크시트에 MDS 관리 데이터가 이미 포함된 경우 활성 워크시트에서 MDS 관리 데이터를 새로 고칠 수 있습니다. 워크시트에 멤버를 추가했거나 특성 값을 변경한 경우 변경 내용을 새로 고치려면 먼저 변경 내용을 게시해야 합니다.  
  
## <a name="refreshing-a-selection"></a>선택한 내용 새로 고침  
 모든 셀을 새로 고칠 수도 있고 선택한 셀만 새로 고칠 수도 있습니다. 연속된 셀을 선택해야 합니다. 연속된 셀 집합을 선택하면 서버에 현재 저장된 값을 표시하도록 해당 집합의 모든 MDS 관리 셀이 업데이트됩니다. MDS로 관리되지 않는 변경되지 않은 행과 열은 영향을 받지 않습니다.  
  
## <a name="what-happens-when-you-refresh-mds-managed-data"></a>MDS 관리 데이터를 새로 고치는 경우 수행되는 작업  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 데이터를 새로 고칠 때 시트의 MDS 관리 데이터에 대해 수행되는 작업은 마지막으로 데이터를 로드한 후 MDS 리포지토리에서 변경된 내용에 따라 달라집니다.  
  
-   새 멤버가 저장소에 추가된 경우 워크시트의 끝에 추가되고 녹색으로 강조 표시됩니다.  
  
-   멤버가 저장소에서 삭제된 경우 워크시트에서 삭제됩니다.  
  
-   MDS 저장소에서 특성 값이 변경된 경우 워크시트의 값이 MDS 저장소의 값으로 업데이트됩니다. 셀 색은 변경되지 않습니다.  
  
> [!WARNING]  
>  -   활성 워크시트에서 관리되지 않는 데이터가 MDS 관리 데이터 아래의 행에 있으면 관리되지 않는 데이터를 덮어쓸 수 있습니다. 이 경우는 시트를 새로 고치고 관리되지 않는 데이터와 겹치는 MDS 관리 데이터의 새 행이 추가될 때 발생합니다.  
> -   게시하면 MDS 관리 셀에 대한 주석이 삭제됩니다.  
  
## <a name="how-to-refresh-mds-managed-data"></a>MDS 관리 데이터를 새로 고치는 방법  
 리본의 **연결 및 로드** 그룹에서 **새로 고침** 단추에는 **모두 새로 고침** 및 **선택 영역 새로 고침**의 두 가지 옵션이 있습니다. 리본 버튼의 기본 동작은 **모두 새로 고침**입니다. 전체 시트를 서버 값으로 새로 고치려면 **새로 고침** 단추를 클릭하거나 **모두 새로 고침** 옵션을 선택합니다. 시트에서 일부 셀만 새로 고치려면 해당 셀(하나의 연속 선택 영역이어야 함)을 선택하고 **선택 영역 새로 고침** 옵션을 선택합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 대한 연결을 만듭니다.|[MDS 리포지토리에 연결&#40;Excel용 MDS 추가 기능&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|MDS 데이터를 Excel로 로드합니다.|[MDS에서 Excel로 데이터 로드](export-data-to-excel-from-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [연결&#40;Excel용 MDS 추가 기능&#41;](connections-mds-add-in-for-excel.md)  
  
-   [데이터 로드 &#40;MDS 추가 기능에 Excel 용&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Master Data Services 추가 기능을 for Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
  