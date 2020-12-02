---
title: IClientVirtualDevice::GetCommand
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDevice::GetCommand 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 226c11ebde66450431719c8d6c2e027479eb3ca4
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125421"
---
# <a name="iclientvirtualdevicegetcommand-vdi"></a>IClientVirtualDevice::GetCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**GetCommand** 함수는 디바이스 큐에 추가된 다음 명령을 가져오는 데 사용됩니다. 요청될 때 이 함수는 다음 명령을 기다립니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDevice::GetCommand (
   DWORD               dwTimeOut,
   VDC_Command**      const ppCmd
);
```

## <a name="parameters"></a>매개 변수

*ppCmd* 명령이 성공적으로 반환되면 매개 변수는 실행할 명령의 주소를 반환합니다. 반환된 메모리는 읽기 전용입니다. 명령이 완료되면 이 포인터가 CompleteCommand 루틴으로 전달됩니다. 각 명령에 대한 자세한 내용은 명령을 참조하세요.

*dwTimeOut* 대기할 시간(밀리초)입니다. 무기한 대기하려면 INFINTE를 사용합니다. 명령을 폴링하려면 0을 사용합니다. 현재 사용할 수 있는 명령이 없으면 VD_E_TIMEOUT이 반환됩니다. 시간 초과가 발생하면 클라이언트는 다음 작업을 결정합니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 명령을 가져왔습니다. |
| VD_E_CLOSE | 서버에서 디바이스를 닫았습니다. |
| VD_E_TIMEOUT | 사용할 수 있는 명령이 없으며 시간 제한이 만료되었습니다. |
| VD_E_ABORT | 클라이언트 또는 서버가 SignalAbort를 사용하여 강제로 종료했습니다. |

## <a name="remarks"></a>설명

VD_E_CLOSE가 반환될 때 SQL Server가 디바이스를 닫았습니다. 정상적인 종료의 일부입니다. 모든 디바이스가 닫힌 후 클라이언트는 IClientVirtualDeviceSet2::Close를 호출하여 가상 디바이스 세트를 닫습니다.

명령을 기다리기 위해 이 루틴이 차단되어야 하는 경우 스레드는 경고 가능 조건으로 남아 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.