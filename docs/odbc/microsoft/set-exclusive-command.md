---
title: "SET 단독 명령을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 830cec1dbb87ae2bc4336d28d6112fd76b4db0ed
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="set-exclusive-command"></a>SET 단독 명령
네트워크에서 배타적으로 또는 공유 사용 하기 위해 테이블 파일을 열지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 사용자에 게 열었을 네트워크에서 열 테이블의 액세스 가능성을 제한 합니다. 테이블을 다른 사용자는 네트워크에 액세스할 수 없습니다. 또한 SET 단독 ON 읽기 전용 액세스 하는 것과 다른 모든 사용자가 방지 합니다.  
  
 OFF  
 (드라이버에 대 한 기본, Visual FoxPro에 대 한 기본값은 ON 글로벌 데이터 세션과 OFF 용 개인 데이터 세션) 테이블을을 공유 하 고 네트워크에서 사용자가 수정할 네트워크에서 열 수 있습니다.  
  
## <a name="remarks"></a>주의  
 단독 설정의 설정 변경 이전에 열린된 테이블의 상태를 변경 되지 않습니다. 예를 들어 단독 설정 ON으로 설정 된 테이블을 열 경우 배타적 설정가 OFF로 변경 나중에 테이블 배타적 사용 가능한 상태로 유지 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)

