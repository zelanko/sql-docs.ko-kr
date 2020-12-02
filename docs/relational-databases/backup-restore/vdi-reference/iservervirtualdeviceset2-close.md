---
title: IServerVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::Close 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 10e699462f2e0b01cb5973e3aeb033ffe10e7680
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128933"
---
# <a name="iservervirtualdeviceset2close-vdi"></a>IServerVirtualDeviceSet2::Close (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Close** 함수는 IServerVirtualDeviceSet2::Open에 의해 열린 가상 디바이스 세트를 닫습니다. 그러면 가상 디바이스와 연결된 모든 리소스가 해제됩니다. IServerVirtualDeviceSet2 핸들은 이 함수가 결과를 반환한 후에는 유용하지 않으며 COM으로 반환되어야 합니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| VD_E_PROTOCOL | 디바이스가 여전히 열려 있습니다. |

## <a name="remarks"></a>설명

디바이스를 닫기 전에 가상 디바이스 세트를 닫지 마세요. 이러한 상황이 발생하면 VD_E_PROTOCOL이 반환됩니다. 이 작업을 수행하면 Close에서 공유 메모리의 매핑을 즉시 해제합니다. 가상 디바이스 인터페이스에서 반환된 리소스의 소유권이 계속 필요한 경우 서버에 액세스 위반이 발생합니다. 이 인터페이스는 SignalAbort 처리를 수행합니다.

완료 에이전트(실행 중인 경우)는 호출자에게 반환되기 전에 처리 중인 모든 명령을 완료합니다. 처리 중인 모든 명령은 ERROR_OPERATION_ABORTED와 함께 완료됩니다. 즉, 콜백 함수가 이러한 각 명령에 대해 호출됩니다.

오류가 반환되는 경우를 비롯한 모든 경우에서 Close는 가상 디바이스 인터페이스에 대한 모든 리소스를 해제합니다. VDI에서 반환된 모든 버퍼 및 기타 인터페이스 포인터가 유효하지 않게 됩니다.

COM 라이브러리가 언로드되기 전에 완료 에이전트가 종료되었는지 확인하는 것이 중요합니다. 완료 에이전트가 호출자에게 반환되기 전에 라이브러리가 언로드되면 해당 프로세스로 인해 명령이 위반될 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.