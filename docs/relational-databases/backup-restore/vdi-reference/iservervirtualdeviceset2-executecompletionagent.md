---
title: IServerVirtualDeviceSet2::ExecuteCompletionAgent
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::ExecuteCompletionAgent 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2ad094794b5115aa4593f918de442798445e2b79
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847294"
---
# <a name="iservervirtualdeviceset2executecompletionagent-vdi"></a>IServerVirtualDeviceSet2::ExecuteCompletionAgent (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**ExecuteCompletionAgent** 함수는 완료 에이전트의 주 루프를 구현하는 데 사용됩니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::ExecuteCompletionAgent ();
```

## <a name="return-value"></a>반환 값

메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. NOERROR 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.

## <a name="remarks"></a>Remarks

완료 에이전트는 SQL Server가 가상 디바이스 명령 완료를 사용하여 자기 자신과 동기화할 수 있는 메커니즘을 제공합니다. 명령을 실행하기 전에는 활성 상태여야 하며 모든 디바이스를 닫을 때까지 활성 상태를 유지해야 합니다.

SQL Server는 특별한 스레드 초기화를 수행해야 할 수 있으므로 이 인터페이스는 컨트롤의 새 스레드를 시작하지 않습니다. 대신, SQL Server는 스레드를 설정한 후 이 루틴에 컨트롤을 전달합니다. 스레드는 Windows NT IPC(프로세스 간 통신) 메커니즘에서 차단 가능해야 하며, IServerVirtualDevice:: SendCommand를 통해 전송된 명령과 함께 제공되는 콜백 함수를 호출할 수 있어야 합니다.

이 함수는 IServerVirtualDeviceSet2::Close 또는 SignalAbort가 호출될 때까지 반환되지 않습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.