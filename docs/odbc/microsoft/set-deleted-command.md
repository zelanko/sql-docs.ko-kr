---
title: 삭제된 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b3302dc7eecca7135dab9dff5afa376169be0f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300883"
---
# <a name="set-deleted-command"></a>SET DELETED 명령
삭제로 표시된 레코드가 처리되는지 여부와 다른 명령에서 사용할 수 있는지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버에 대 한 기본값; Visual FoxPro에 대 한 기본값은 꺼져 있습니다.) 범위를 사용하여 레코드에서 작동하는 명령(관련 테이블의 레코드 포함)은 삭제로 표시된 레코드무시를 지정합니다.  
  
 OFF  
 범위를 사용하여 레코드(관련 테이블의 레코드 포함)에서 작동하는 명령에서 삭제로 표시된 레코드에 액세스할 수 있도록 지정합니다.  
  
## <a name="remarks"></a>설명  
 DELETED()를 사용하여 레코드 상태를 테스트하는 쿼리는 DELETED()에서 테이블을 인덱싱하는 경우 Visual FoxPro Rushmore 기술을 사용하여 최적화할 수 있습니다.  
  
> [!IMPORTANT]  
>  SET DELETED 는 명령의 기본 범위가 현재 레코드이거나 단일 레코드의 범위를 포함하는 경우 무시됩니다. INDEX는 항상 SET DELETED를 무시하고 테이블의 모든 레코드를 인덱싱합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DELETE - SQL 명령](../../odbc/microsoft/delete-sql-command.md)
