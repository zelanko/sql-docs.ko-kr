---
description: 편집 모드 확인
title: 편집 모드를 확인 하는 중 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: rothja
ms.author: jroth
ms.openlocfilehash: ec235cfd012b79449fdebfab9c99399d967ca32f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991364"
---
# <a name="determining-edit-mode"></a>편집 모드 확인
ADO는 현재 레코드와 연결 된 편집 버퍼를 유지 관리 합니다. **EditMode** 속성은이 버퍼가 변경 되었는지 또는 새 레코드가 생성 되었는지 여부를 나타냅니다. **EditMode** 를 사용 하 여 현재 레코드의 편집 상태를 확인 합니다. 편집 프로세스가 중단 된 경우 보류 중인 변경 내용을 테스트 하 고 **Update** 또는 **CancelUpdate** 메서드를 사용 해야 하는지 여부를 결정할 수 있습니다.  
  
 **EditMode** 는 다음 표에 나열 된 **editmodeenum** 상수 중 하나를 반환 합니다.  
  
|상수|설명|  
|--------------|-----------------|  
|**adEditNone**|진행 중인 편집 작업이 없음을 나타냅니다.|  
|**adEditInProgress**|현재 레코드의 데이터가 수정 되었지만 저장 되지 않았음을 나타냅니다.|  
|**adEditAdd**|는 **AddNew** 메서드를 호출 했 고 복사 버퍼의 현재 레코드는 데이터베이스에 저장 되지 않은 새 레코드 임을 나타냅니다.|  
|**adEditDelete**|현재 레코드가 삭제 되었음을 나타냅니다.|  
  
 **EditMode** 는 현재 레코드가 있는 경우에만 유효한 값을 반환할 수 있습니다. **BOF** 또는 **EOF** 가 **True** 이거나 현재 레코드가 삭제 된 경우 **EditMode** 는 오류를 반환 합니다.
