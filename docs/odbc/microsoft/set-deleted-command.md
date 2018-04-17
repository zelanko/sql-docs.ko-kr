---
title: SET DELETED 명령을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d81c422b5984fbc95b0c71787940f24b75356db2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="set-deleted-command"></a>삭제 된 명령 집합
삭제 표시 된 레코드가 처리 여부 및 다른 명령에서 사용 하기 위해 사용할 수 있는 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본, Visual FoxPro에 대 한 기본값은 OFF) 레코드 (관련된 테이블의 레코드를 포함)에서 작동 하는 명령을 지정 삭제 표시 된 레코드를 무시할 범위를 사용 합니다.  
  
 OFF  
 레코드 삭제 레코드 (관련된 테이블의 레코드를 포함)에서 작동 하는 명령을 사용 하 여 액세스할 수에 대 한 표시 되도록 지정 범위를 사용 합니다.  
  
## <a name="remarks"></a>주의  
 레코드의 상태를 테스트 하려면 삭제 된 ()를 사용 하 여 테이블은 삭제 됨 ()에 지정 된 경우 Visual FoxPro Rushmore 기술을 사용 하 여 최적화할 수 있는지를 쿼리 합니다.  
  
> [!IMPORTANT]  
>  설정 삭제 명령에 대 한 기본 범위는 현재 레코드 또는 단일 레코드의 범위를 포함 하는 경우 무시 됩니다. 인덱스는 항상 삭제 설정 무시 하 고 테이블의 모든 레코드를 인덱싱합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DELETE - SQL 명령](../../odbc/microsoft/delete-sql-command.md)
