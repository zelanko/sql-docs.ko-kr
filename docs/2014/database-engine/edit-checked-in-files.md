---
title: 체크 인 된 파일을 편집 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97d6ab997a1ece36919a49243e0f1dc3cc6f3593
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779607"
---
# <a name="edit-checked-in-files"></a>체크 인 파일 편집
  일반적으로 원본 제어 파일을 편집하려면 먼저 해당 파일을 체크 아웃해야 합니다. 그러나 체크 아웃하지 않는 파일을 수정할 수 있도록 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 구성할 수 있습니다. 이렇게 할 경우에는 파일을 저장할 때까지 변경 내용이 메모리에 유지됩니다. 그런 다음 소스 제어에서 파일을 체크 아웃하라는 메시지가 나타납니다.  
  
 팀에서 작업하는 중이면 소스 제어 공급자가 로컬 버전 및 서버 버전 체크 아웃을 모두 지원하지 않을 경우에는 체크 인한 파일을 편집할 수 있도록 허용하는 것이 권장되지 않습니다. 대부분의 공급자는 로컬 버전 체크 아웃을 지원하지 않습니다. 공급자가 로컬 버전 체크 아웃을 지원하지 않는 상태에서 체크 인한 파일을 편집하려는 경우 파일을 체크 인하려면 메모리 내 버전과 서버 버전을 수동으로 병합해야 합니다. 이 상황에서 자동 및 공급자 지원 병합은 지원되지 않습니다.  
  
### <a name="to-edit-checked-in-files"></a>체크 인한 파일을 편집하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **소스 제어**폴더를 확장한 다음 **환경**을 클릭합니다.  
  
3.  **체크 인한 항목 편집 허용**을 클릭한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [체크 인 관리](../../2014/database-engine/manage-checkins.md)   
 [체크 아웃 관리](../../2014/database-engine/manage-checkouts.md)  
  
  
