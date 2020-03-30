---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDevice::SendCommand 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c75cd206557547f55d47eec0a7aec52cc0069b71
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847514"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SendCommand** 함수는 IServerVirtualDeviceSet2::OpenDevice에서 반환된 가상 디바이스 개체를 사용하여 클라이언트에 명령을 보냅니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>매개 변수

*pCmd* 명령 요청 블록에 대한 포인터입니다. 자세한 내용은 명령을 참조하세요. 다음 서명을 사용하여 함수의 주소를 가리키도록 completionFunction 필드를 설정해야 합니다.

```c
void callbackFunction ( VDS_Command *pCmd);
```

이 콜백은 클라이언트가 명령이 완료되었음을 나타내는 경우 완료 에이전트에 의해 수행됩니다. SQL Server는 pCmd의 completionContext 필드를 설정합니다. 이는 콜백 함수에 컨텍스트를 제공하기 위한 것입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 명령이 클라이언트 큐에 성공적으로 대기되었습니다. |
| VD_E_QUEUE_FULL | 디바이스 큐가 꽉 찼습니다. |
| VD_E_IO_ERROR | 디바이스가 IO-ERROR 상태에 있습니다. |
| VD_E_PROTOCOL | 디바이스가 활성화되지 않았습니다. |

## <a name="remarks"></a>설명

명령을 보내려고 시도하는 동안 오류가 발생하면 콜백 함수가 호출되고 명령 버퍼의 completionCode가 다음과 같이 설정됩니다.

| completionCode | Error |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.