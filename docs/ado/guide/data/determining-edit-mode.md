---
title: "편집 모드 결정 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3ffee8b910c5e13754c461671a00380d348f3f9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="determining-edit-mode"></a>편집 모드 확인
ADO 현재 레코드와 연결 된 편집 버퍼를 유지 관리 합니다. **EditMode** 속성은이 버퍼에 변경 사항이 있는지 여부 또는 새 레코드를 만들어졌는지를 나타냅니다. 사용 하 여 **EditMode** 현재 레코드의 편집 상태를 확인할 수 있습니다. 편집 프로세스가 중단 된 보류 중인 변경 내용에 대 한 테스트 하 고 사용 해야 하는지 여부를 확인할 수는 **업데이트** 또는 **CancelUpdate** 메서드.  
  
 **EditMode** 중 하나를 반환 된 **EditModeEnum** 다음 표에 나열 된 상수입니다.  
  
|상수|Description|  
|--------------|-----------------|  
|**adEditNone**|편집 작업이 진행에서 중인지를 나타냅니다.|  
|**adEditInProgress**|현재 레코드의 데이터가 수정 되었지만 저장 안 됨을 나타냅니다.|  
|**adEditAdd**|나타냅니다는 **AddNew** 메서드를 호출 하 고 복사 버퍼의 현재 레코드는 데이터베이스에 저장 되지 않은 새 레코드입니다.|  
|**adEditDelete**|현재 레코드 삭제 했을 나타냅니다.|  
  
 **EditMode** 현재 레코드가 있는 경우에 유효한 값을 반환할 수 있습니다. **EditMode** 경우 오류가 반환 됩니다 **BOF** 또는 **EOF** 은 **True** 아니면 현재 레코드를 삭제 합니다.
