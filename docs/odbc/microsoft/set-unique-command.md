---
title: SET UNIQUE 명령 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300843"
---
# <a name="set-unique-command"></a>SET UNIQUE 명령
인덱스 키 값이 중복 된 레코드가 인덱스 파일에 유지 되는지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 인덱스 키 값이 중복 되는 레코드가 인덱스 파일에 포함 되지 않도록 지정 합니다. 원래 인덱스 키 값을 가진 첫 번째 레코드만 인덱스 파일에 포함 됩니다.  
  
 OFF  
 (기본값) 인덱스 키 값이 중복 된 레코드가 인덱스 파일에 포함 되도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 인덱스 파일은 인덱스를 사용할 때 설정 된 고유 설정을 유지 합니다. 자세한 내용은 [인덱스](../../odbc/microsoft/index-command.md)를 참조 하세요.
