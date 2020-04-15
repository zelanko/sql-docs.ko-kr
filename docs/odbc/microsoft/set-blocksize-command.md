---
title: 블록 크기 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300903"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 명령
메모 필드 저장에 디스크 공간이 할당되는 방법을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>인수  
 *n바이트*  
 메모 필드에 대한 디스크 공간이 할당되는 블록 크기를 지정합니다. *n바이트가* 0이면 디스크 공간은 단일 바이트(1바이트 블록)로 할당됩니다. *nBytes가* 1에서 32 사이의 정수인 경우 디스크 공간은 *nBytes* 바이트 블록에 512를 곱한 값으로 할당됩니다. *nBytes가* 32보다 큰 경우 디스크 공간은 *nBytes* 바이트 블록에 할당됩니다. 블록 크기 값이 32보다 큰 경우 상당한 디스크 공간을 절약할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 SET BLOCKSIZE의 기본값은 64입니다. 파일을 만든 후 블록 크기를 다른 값으로 재설정하려면 파일을 새 값으로 설정한 다음 COPY를 사용하여 새 테이블을 만듭니다. 새 테이블에 지정된 블록 크기가 있습니다.
