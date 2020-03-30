---
title: IServerVirtualDeviceSet2::AllocateBuffer
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::AllocateBuffer 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8c28009fae8b52264b541ca3eb4281ab9abccf63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847494"
---
# <a name="iservervirtualdeviceset2allocatebuffer-vdi"></a>IServerVirtualDeviceSet2::AllocateBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**AllocateBuffer** 함수는 가상 디바이스 세트에서 공유 메모리 버퍼를 가져옵니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::AllocateBuffer (
   LPVOID*      ppBuffer,
   UINT32      dwSize,
   UINT32      dwAlignment
);
```

## <a name="parameters"></a>매개 변수

*ppBuffer* 버퍼의 시작에 대한 포인터를 반환합니다.

*dwsize* 버퍼의 크기(바이트)입니다. 클라이언트에서 요청한 접두사 영역은 여기에 포함되지 않습니다. 이러한 영역은 서버에서 숨겨지고 버퍼 주소가 반환되기 전에 사용할 수 있는 공간이 제공됩니다.

*dwAlignment* 버퍼의 맞춤 경계를 지정합니다. 예를 들어, 4096 값을 설정하면 버퍼가 4096바이트 경계에 맞춰집니다. 즉, 반환되는 주소에서는 낮은 순서 12비트가 0으로 설정됩니다. 이 매개 변수는 2의 거듭제곱이어야 합니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 버퍼가 반환됩니다. |
| VD_E_MEMORY | 메모리 부족 상태가 발생했습니다. |
| VD_E_INVALID | 매개 변수가 잘못되었습니다. |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.