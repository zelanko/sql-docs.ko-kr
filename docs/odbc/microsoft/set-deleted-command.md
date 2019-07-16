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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997740"
---
# <a name="set-deleted-command"></a>SET DELETED 명령
삭제 표시 된 레코드를 처리 하는 여부 및 다른 명령에서 사용할 수 있는지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본; Visual FoxPro에 대 한 기본값은 OFF입니다.) 레코드 (관련된 테이블의 레코드를 포함)에서 작동 하는 명령을 지정 범위를 사용 하 여 삭제 표시 된 레코드를 무시 합니다.  
  
 OFF  
 레코드 삭제는 레코드 (관련된 테이블의 레코드를 포함)에서 작동 하는 명령에 액세스할 수 있습니다에 대 한 표시 되도록 지정 된 범위를 사용 하 여 합니다.  
  
## <a name="remarks"></a>설명  
 레코드의 상태를 테스트 하려면 삭제 ()를 사용 하 여 최적화할 수 있습니다. 테이블 삭제 ()에서 인덱싱된 경우 Visual FoxPro Rushmore 기술을 사용 하 여 쿼리 합니다.  
  
> [!IMPORTANT]  
>  설정 삭제 명령에 대 한 기본 범위는 현재 레코드 또는 단일 레코드의 범위를 포함 하는 경우 무시 됩니다. 인덱스는 항상 삭제 설정 무시 하 고 테이블의 모든 레코드를 인덱싱합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DELETE - SQL 명령](../../odbc/microsoft/delete-sql-command.md)
