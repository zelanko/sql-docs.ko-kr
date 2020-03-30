---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::FreeBuffer 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2829f849ce8cd220fdabc75a0d2059c5da0c80fd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847264"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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