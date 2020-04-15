---
title: 고유 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d3d37509450d1305891100b37bfd1ad026166e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300843"
---
# <a name="set-unique-command"></a>SET UNIQUE 명령
중복 인덱스 키 값이 있는 레코드가 인덱스 파일에서 유지 관리되는지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 중복 인덱스 키 값이 있는 레코드가 인덱스 파일에 포함되지 않도록 지정합니다. 원래 인덱스 키 값이 있는 첫 번째 레코드만 인덱스 파일에 포함됩니다.  
  
 OFF  
 (기본값)을 사용합니다. 중복 인덱스 키 값이 있는 레코드가 인덱스 파일에 포함되도록 지정합니다.  
  
## <a name="remarks"></a>설명  
 인덱스 파일은 REINDEX를 발행할 때 고유 설정 설정을 유지합니다. 자세한 내용은 [INDEX](../../odbc/microsoft/index-command.md)을 참조하십시오.
