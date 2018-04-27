---
title: 병합 충돌(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0764aa9c7ff87d7fbbc0ac85fc39132fdcb6029f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="merge-conflicts-mds-add-in-for-excel"></a>병합 충돌(Excel용 MDS 추가 기능)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Excel용 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 추가 기능에서는 서버의 데이터를 다른 사용자가 변경한 경우 충돌 오류로 인해 게시에 실패합니다. 이 오류를 해결하려면 병합 충돌을 수행하고 변경 내용을 다시 게시합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   업데이트할 엔터티의 리프 모델 개체에 대한 업데이트 이상의 권한이 있어야 합니다.  
  
-   활성 워크시트에는 MDS 관리 데이터가 있어야 합니다.  
  
-   활성 워크시트에는 변경 내용의 게시를 시도한 후 충돌 오류가 있어야 합니다.  
  
### <a name="to-merge-conflicts"></a>충돌 내용을 병합하려면  
  
1.  워크시트에서 충돌 오류가 있는 행 또는 셀을 선택합니다.  
  
2.  **게시 및 유효성 검사** 메뉴 그룹에서 **병합 충돌** 을 선택하면 **병합 충돌** 대화 상자가 열립니다.  
  
3.  **병합 충돌** 대화 상자에서 다음 중 하나를 수행할 수 있습니다.  
  
    -   **최신 버전** 을 선택하고 **적용** 을 클릭하여 보류 중인 변경을 실행 취소하고 서버에서 최신 버전을 다시 로드합니다.  
  
    -   **원본** 을 선택하고 **적용** 을 클릭하여 워크시트의 원래 버전을 적용합니다.  
  
    -   **내 변경 내용** 을 선택하고 **적용** 을 클릭하여 기존 로컬 변경 내용을 유지합니다.  
  
4.  **적용**을 클릭한 후에 추가 변경을 수행하고 데이터를 다시 게시할 수 있습니다. 또는 **취소** 를 클릭하여 업데이트를 취소하고 서버에서 최신 버전을 다시 로드할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [개요: Excel에서 데이터 가져오기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
