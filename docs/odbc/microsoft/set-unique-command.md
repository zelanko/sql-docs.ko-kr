---
description: SET UNIQUE 명령
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
ms.openlocfilehash: b8fa4ca11ed5beae08bfcbeb8b5a55d6c2969785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412459"
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
