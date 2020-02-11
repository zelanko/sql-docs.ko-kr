---
title: SET DELETED 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997740"
---
# <a name="set-deleted-command"></a>SET DELETED 명령
삭제 표시 된 레코드를 처리 하 고 다른 명령에서 사용할 수 있는지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버의 기본값입니다. Visual FoxPro의 기본값은 OFF입니다.) 범위를 사용 하 여 레코드 (관련 테이블의 레코드 포함)에서 작동 하는 명령이 삭제 표시 된 레코드를 무시 하도록 지정 합니다.  
  
 OFF  
 범위를 사용 하 여 레코드 (관련 테이블의 레코드 포함)에서 작동 하는 명령이 삭제 하도록 표시 된 레코드에 액세스할 수 있도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 Deleted ()를 사용 하 여 레코드 상태를 테스트 하는 쿼리는 삭제 된 ()에서 테이블이 인덱싱되는 경우 Visual FoxPro Rushmore 기술을 사용 하 여 최적화할 수 있습니다.  
  
> [!IMPORTANT]  
>  명령의 기본 범위가 현재 레코드 이거나 단일 레코드의 범위를 포함 하는 경우에는 SET DELETED가 무시 됩니다. 인덱스는 항상 삭제 된 집합을 무시 하 고 테이블의 모든 레코드를 인덱싱합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DELETE - SQL 명령](../../odbc/microsoft/delete-sql-command.md)
