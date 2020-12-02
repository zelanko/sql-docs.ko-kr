---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::SignalAbort 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d36a08586a6903a6e85bb4bad4d6344a54938cd2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125391"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**SignalAbort** 함수는 비정상적인 종료가 발생해야 함을 신호로 알리는 데 사용됩니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Return Value

메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. NOERROR 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.

## <a name="remarks"></a>설명

언제든지 클라이언트는 BACKUP 또는 RESTORE 작업을 중단하도록 선택할 수 있습니다. 이 루틴은 모든 작업이 중단되어야 함을 신호로 알립니다. 전체 가상 디바이스 세트의 상태가 중단 상태로 전환됩니다. 모든 디바이스에서 추가 명령이 반환되지 않습니다. 완료되지 않은 모든 명령이 자동으로 완료되고 ERROR_OPERATION_ABORTED가 완료 코드로 반환됩니다. 클라이언트는 클라이언트에 제공된 버퍼의 처리되지 않은 사용을 안전하게 종료한 후 IClientVirtualDeviceSet2::Close를 호출해야 합니다. 자세한 내용은 비정상적인 종료를 참조하세요.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.