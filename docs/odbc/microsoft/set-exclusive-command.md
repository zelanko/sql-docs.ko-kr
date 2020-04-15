---
title: 전용 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300863"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 명령
테이블에서 단독 또는 공유 용으로 테이블 파일을 열수 있는지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 네트워크에서 열린 테이블의 접근성을 연 사용자에게 제한합니다. 네트워크의 다른 사용자가 테이블에 액세스할 수 없습니다. 또한 단독 ON 설정은 다른 모든 사용자가 읽기 전용 액세스 권한을 갖지 못하도록 합니다.  
  
 OFF  
 (드라이버의 기본값; Visual FoxPro의 기본값은 전역 데이터 세션의 경우 ON이고 개인 데이터 세션의 경우 꺼져 있습니다.) 네트워크에서 열린 테이블을 네트워크의 모든 사용자가 공유하고 수정할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 SET EXCLUSIVE 설정을 변경해도 이전에 열린 테이블의 상태는 변경되지 않습니다. 예를 들어, SET 배타적 세트를 ON으로 설정하고 단독 설정으로 테이블을 열면 나중에 OFF로 변경된 테이블은 단독 사용 상태를 유지합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
