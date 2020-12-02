---
title: IClientVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::Close 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: ccac23e8049884ba7bd403c91f6bde8a1f29cf84
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128981"
---
# <a name="iclientvirtualdeviceset2close-vdi"></a>IClientVirtualDeviceSet2::Close (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Close** 함수는 IClientVirtualDeviceSet2::Create에서 만든 가상 디바이스 세트를 닫습니다. 그러면 가상 디바이스 세트에 연결된 모든 리소스가 해제됩니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 가상 디바이스 세트가 성공적으로 닫힌 경우 반환됩니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 열리지 않았으므로 아무 작업도 수행되지 않았습니다. |
| VD_E_OPEN | 디바이스가 열려 있었습니다. |

## <a name="remarks"></a>설명

Close 호출은 가상 디바이스 세트에서 사용되는 모든 리소스를 해제해야 하는 클라이언트에 의한 선언입니다. 클라이언트는 Close를 호출하기 전에 데이터 버퍼 및 가상 디바이스와 관련된 모든 작업이 종료되었는지 확인해야 합니다. OpenDevice에서 반환된 모든 가상 디바이스 인터페이스는 Close로 무효화됩니다.

클라이언트는 Close 호출이 결과를 반환한 후에 가상 디바이스 세트 인터페이스에서 Create 호출을 실행할 수 있습니다. 해당 호출은 후속 BACKUP 또는 RESTORE 작업에 대한 새 가상 디바이스 세트를 만듭니다.

하나 이상의 가상 디바이스가 열려 있을 때 Close를 호출하면 VD_E_OPEN이 반환됩니다. 이 경우 가능한 경우 적절한 종료를 보장하기 위해 SignalAbort는 내부적으로 트리거됩니다. VDI 리소스가 해제됩니다. 클라이언트는 IClientVirtualDeviceSet2::Close를 호출하기 전에 각 디바이스에서 VD_E_CLOSE 표시를 기다려야 합니다. 클라이언트는 가상 디바이스 세트가 이미 비정상적으로 종료된 상태임을 인식하면 GetCommand에서 VD_E_CLOSE 표시를 예상하지 않으며, 공유 버퍼의 활동이 종료되는 즉시 IClientVirtualDeviceSet2::Close를 호출할 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.