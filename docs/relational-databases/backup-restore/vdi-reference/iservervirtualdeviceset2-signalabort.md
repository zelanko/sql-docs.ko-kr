---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::SignalAbort 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b61a972d7b379ff40440124c875d8d49a7af1835
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847174"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SignalAbort** 함수는 비정상적인 종료가 발생하도록 신호를 보냅니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Return Value

메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. NOERROR 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.

## <a name="remarks"></a>설명

언제든지 서버는 BACKUP 또는 RESTORE 작업을 중단하도록 선택할 수 있습니다.

이 루틴은 모든 작업이 중단되어야 함을 신호로 알립니다. 전체 인터페이스는 중단 상태로 전환됩니다. 모든 디바이스에서 추가 명령이 수락되지 않습니다. 완료 에이전트는 처리 중인 각 요청에 대해 ERROR_OPERATION_ABORTED를 반환하고 해당 호출자에게 반환합니다. 클라이언트에서 기록된 모든 완료는 무시됩니다.

서버에서는 가상 디바이스 인터페이스에서 반환된 버퍼 또는 디바이스를 더 이상 사용하지 않아도 됩니다. 그런 다음, 서버는 IServerVirtualDeviceSet2::Close 함수 호출을 포함해야 하는 비정상적인 종료 정리를 수행합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.