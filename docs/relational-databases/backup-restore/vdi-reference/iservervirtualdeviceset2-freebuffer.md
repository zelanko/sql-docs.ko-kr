---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::FreeBuffer 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d75d859b4340e95d705037b603f186871acb3b42
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125343"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**FreeBuffer** 함수는 가상 디바이스 세트에서 공유 메모리 버퍼를 가져옵니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>매개 변수

*pBuffer* IServerVirtualDeviceSet2::AllocateBuffer에서 반환된 버퍼를 반환합니다.

*dwsize* 버퍼의 크기(바이트)입니다. 클라이언트에서 요청한 접두사 영역은 여기에 포함되지 않습니다. 이러한 영역은 서버에서 숨겨지고 버퍼 주소가 반환되기 전에 사용할 수 있는 공간이 제공됩니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 버퍼가 반환됩니다. |
| VD_E_INVALID | 매개 변수가 잘못되었습니다. |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.