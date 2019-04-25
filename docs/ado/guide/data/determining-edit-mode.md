---
title: 편집 모드 확인 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e638cda03d7dc0f0bd580c3ca29c126568d1595a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472344"
---
# <a name="determining-edit-mode"></a>편집 모드 확인
ADO는 현재 레코드와 연결 된 편집 버퍼를 유지 합니다. 합니다 **EditMode** 속성은이 버퍼에 변경 사항이 있는지 여부 또는 새 레코드를 만들어졌는지를 나타냅니다. 사용 하 여 **EditMode** 현재 레코드의 편집 상태를 확인 합니다. 편집 프로세스가 중단 된 보류 중인 변경 내용에 대 한 테스트를 사용 해야 하는지 여부를 확인 합니다 **업데이트** 또는 **CancelUpdate** 메서드.  
  
 **EditMode** 중 하나를 반환 합니다 **EditModeEnum** 다음 표에 나열 된 상수입니다.  
  
|상수|Description|  
|--------------|-----------------|  
|**adEditNone**|편집 작업이 진행에서 중임을 나타냅니다.|  
|**adEditInProgress**|현재 레코드의 데이터가 수정 되었지만 저장 되지 있는지를 나타냅니다.|  
|**adEditAdd**|나타내는 합니다 **AddNew** 메서드를 호출 이며 복사 버퍼에서 현재 레코드가 새 레코드를 데이터베이스에 저장 되지 않았습니다.|  
|**adEditDelete**|현재 레코드를 삭제 했을 나타냅니다.|  
  
 **EditMode** 현재 레코드를 필요한 경우에 유효한 값을 반환할 수 있습니다. **EditMode** 하는 경우 오류가 반환 됩니다 **BOF** 또는 **EOF** 됩니다 **True** 현재 레코드를 삭제 하는 경우.
