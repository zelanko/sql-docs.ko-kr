---
title: IServerVirtualDeviceSet2::RequestBuffers
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::RequestBuffers 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1b941f251c9093f10abbced8c3522f1719a1580e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847184"
---
# <a name="iservervirtualdeviceset2requestbuffers-vdi"></a>IServerVirtualDeviceSet2::RequestBuffers (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RequestBuffers** 함수는 서버에 지정된 크기 및 맞춤 요구 사항을 갖는 특정 개수의 버퍼가 필요함을 VDI에 알립니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::RequestBuffers (
   DWORD   dwSize,
   DWORD   dwAlignment,
   DWORD   dwCount
);
```

## <a name="parameters"></a>매개 변수

*dwsize* 각 버퍼의 크기를 식별합니다. 이 크기는 데이터에 필요한 영역을 포함해야 합니다. VDI는 맞춤 및 접두사 요구 사항을 처리합니다.

*dwalignment* 이러한 버퍼에 필요한 맞춤입니다. 'BeginConfiguration'으로 지정된 기본 맞춤 값보다 좀 더 제한적인 값을 사용할 수 있습니다. 값이 0이면 기본적으로 기본 맞춤 값이 사용됩니다.

*dwcount* 지정된 크기와 맞춤을 갖는 'AllocateBuffer'에서 요청하는 버퍼 수입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_ABORT | 중단이 요청되었습니다. |
| VD_E_PROTOCOL | 이 세트는 버퍼 할당이 선언될 수 있는 상태가 아닙니다(상태 전환 행렬 참조). |
| VD_E_MEMORY | 요청된 메모리를 가져올 수 없습니다. |

## <a name="remarks"></a>설명

이 메서드는 AllocateBuffer를 사용하여 버퍼를 할당하기 전에 사용해야 합니다. 지정된 크기와 맞춤이 지정된 버퍼 세트가 RequestBuffers를 사용하여 요청된 다음, AllocateBuffer를 사용하여 개별 버퍼가 할당됩니다.

구성 단계에서 RequestBuffers 호출은 모두 "합산"되므로 EndConfiguration 호출에서 단일 버퍼 영역을 사용할 수 있습니다(해당 시간에 할당됨). 구성이 완료된 후에 RequestBuffers 호출이 수행되면 더 많은 버퍼 공간이 즉시 할당됩니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.