---
title: 블록 크기 설정 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4fe84a470f5e877c73701168394cd85d75253fb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997753"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 명령
메모 필드의 저장소에 대해 디스크 공간을 할당 하는 방법을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>인수  
 *nBytes*  
 메모 필드에 대 한 디스크 공간이 할당 되는 블록 크기를 지정 합니다. *Nbytes* 가 0 인 경우 디스크 공간은 단일 바이트 (1 바이트 블록)로 할당 됩니다. *Nbytes* 가 1에서 32 사이의 정수 이면 디스크 공간은 *nbytes* 바이트의 블록에 512를 곱하여 할당 됩니다. *Nbytes* 가 32 보다 큰 경우 디스크 공간은 *nbytes* 바이트 블록으로 할당 됩니다. 32 보다 큰 블록 크기 값을 지정 하면 실제 디스크 공간을 절약할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 집합 블록 블록의 기본값은 64입니다. 파일이 만들어진 후 블록 크기를 다른 값으로 다시 설정 하려면 새 값으로 설정한 다음 복사를 사용 하 여 새 테이블을 만듭니다. 새 테이블에는 지정 된 블록 크기가 지정 됩니다.
