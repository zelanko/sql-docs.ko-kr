---
title: 정책 가져오기 대화 상자 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a0830e5db32fcc651b59114e1a2dad870e48d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705238"
---
# <a name="import-policies-dialog-box"></a>정책 가져오기 대화 상자
  이 대화 상자를 사용하여 XML 파일로 저장된 하나 이상의 정책과 해당 참조 조건을 현재 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스로 가져올 수 있습니다.  
  
## <a name="options"></a>변수  
 **가져올 파일**  
 XML 파일에서 정책을 가져오려면 파일의 경로와 이름을 입력하거나 찾아보기 단추( **...** )를 사용합니다.  
  
 **가져온 항목으로 중복 항목 바꾸기**  
 이 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 이름이 같은 정책 또는 조건이 이미 있는 경우 기존 정책 또는 조건을 덮어쓰려면 선택합니다. 종속 정책이 있는 조건은 종속 정책도 덮어쓰지 않는 한 덮어쓸 수 없습니다. 이 옵션을 선택하지 않으면 같은 조건 식을 사용하는 기존 조건으로 인해 오류가 발생하지 않습니다.  
  
 **정책 상태**  
 가져온 정책에서 원하는 상태를 선택합니다.  
  
-   **가져올 때 정책 상태 유지**  
  
-   **가져올 때 모든 정책을 사용할 수 있도록 설정**  
  
-   **가져올 때 모든 정책을 사용할 수 없도록 설정**  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 정책 가져오기](import-a-policy-based-management-policy.md)   
 [정책 기반 관리 정책 내보내기](export-a-policy-based-management-policy.md)  
  
  
