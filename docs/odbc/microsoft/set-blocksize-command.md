---
title: SET BLOCKSIZE 명령을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee5b55501d055d3bea09903a5486e88de3cdc993
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 명령
메모 필드의 저장에 대 한 디스크 공간이 할당 되는 방식을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>인수  
 *nBytes*  
 메모 필드에 대 한 디스크 공간 할당 된 블록 크기를 지정 합니다. 경우 *nBytes* 은 0으로, 단일 바이트 (1 바이트 블록)에서 디스크 공간을 할당 합니다. 경우 *nBytes* 1-32, 디스크 공간 사이의 정수 블록에 할당 되는 *nBytes* 바이트 512를 곱합니다. 경우 *nBytes* 32 보다 큰 블록에 디스크 공간이 할당 *nBytes* 바이트입니다. 32 보다 큰 블록 크기 값을 지정 하는 경우에 디스크 공간을 크게를 저장할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 블록 크기 설정의 기본값은 64입니다. 파일이 생성 된 블록 크기를 다른 값으로 다시 설정, 새 값으로 설정 하 고 복사를 사용 하 여 새 테이블을 만들 합니다. 새 테이블에는 지정 된 블록 크기입니다.
