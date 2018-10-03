---
title: SET BLOCKSIZE 명령 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e904d341513047b3940cf5b3fc2ba9538cdb5c8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764231"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 명령
메모 필드의 저장소에 대 한 디스크 공간이 할당 되는 방식을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>인수  
 *nBytes*  
 메모 필드에 대 한 디스크 공간이 할당 되는 블록 크기를 지정 합니다. 하는 경우 *nBytes* 0 인 단일 바이트 (1 바이트 블록)에서 디스크 공간을 할당 합니다. 하는 경우 *nBytes* 1 자에서 32, 디스크 공간 사이의 정수 블록에 할당 되는 *nBytes* 512 바이트를 곱하고 합니다. 하는 경우 *nBytes* 32 보다 큰 블록에서 디스크 공간을 할당 *nBytes* 바이트입니다. 32 보다 큰 블록 크기 값을 지정 하는 경우에 상당한 디스크 공간을 저장할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 BLOCKSIZE 설정의 기본값은 64입니다. 를 다시 설정 하려면 블록 크기를 다른 값으로 파일을 만든 후 새 값으로 설정 하 고 새 테이블을 만들려면 복사를 사용 합니다. 새 테이블에 지정 된 블록 크기입니다.
