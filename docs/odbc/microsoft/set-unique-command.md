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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063610"
---
# <a name="set-unique-command"></a>SET UNIQUE 명령
중복 인덱스 키 값을 사용 하 여 레코드 인덱스 파일에 유지 됩니다 있는지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 인덱스 파일에 중복 인덱스 키 값을 가진 모든 레코드를 포함 되지 않음을 지정 합니다. 원래 인덱스 키 값을 가진 첫 번째 레코드에만 인덱스 파일에 포함 됩니다.  
  
 OFF  
 (기본값) 중복 인덱스 키 값을 사용 하 여 레코드 인덱스 파일에 포함 되어야 함을 지정 합니다.  
  
## <a name="remarks"></a>설명  
 인덱스 파일 REINDEX 실행할 때 해당 고유 설정 설정을 유지 합니다. 자세한 내용은 [인덱스](../../odbc/microsoft/index-command.md)합니다.
