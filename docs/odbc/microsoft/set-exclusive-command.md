---
title: SET EXCLUSIVE 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccbc9b258cbff1e14ccc76e10af9d26efc4b70b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159267"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 명령
네트워크에서 배타적으로 또는 공유 사용에 대 한 테이블 파일을 열지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 연 사용자에 게 해당 하는 네트워크에서 열을 테이블의 액세스 가능성을 제한 합니다. 테이블을 다른 사용자는 네트워크에 액세스할 수 없습니다. 또한 SET 단독 ON는 읽기 전용으로 액세스 하는 것과 다른 모든 사용자를 방지 합니다.  
  
 OFF  
 (드라이버에 대 한 기본; Visual FoxPro에 대 한 기본값은 ON 글로벌 데이터 세션 및 OFF 용 개인 데이터 세션) 테이블을을 공유 하 고 네트워크에서 모든 사용자가 수정한 네트워크에서 열 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 배타적 집합의 설정 변경 이전에 열린된 테이블의 상태를 변경 되지 않습니다. 예를 들어, 전용 설정 ON으로 설정 된 테이블을 열 경우 배타적 설정 나중에 변경 OFF로 테이블에 배타적 사용 상태가 유지 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
