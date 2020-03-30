---
title: IClientVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::OpenDevice 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: aff46d7240cf504b02e75d91b75d0ba746a24752
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847574"
---
# <a name="iclientvirtualdeviceset2opendevice-vdi"></a>IClientVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**OpenDevice** 함수는 가상 디바이스 세트의 디바이스 중 하나를 엽니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::OpenDevice (
   LPCWSTR                  lpName,
   IClientVirtualDevice**   ppVirtualDevice

);
```

## <a name="parameters"></a>매개 변수

*lpName* 가상 디바이스를 식별합니다.

*ppVirtualDevice* 함수가 성공하면 가상 디바이스에 대한 인터페이스 포인터가 반환됩니다. 이 인터페이스는 GetCommand 및 CompleteCommand에 사용됩니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_ABORT | 중단이 요청되었습니다. |
| VD_E_OPEN |모든 디바이스가 열립니다. |
| VD_E_PROTOCOL | 세트가 초기화 상태가 아니거나 이 특정 디바이스가 이미 열려 있습니다. |
| VD_E_INVALID | 디바이스 이름이 잘못되었습니다. 세트를 구성하는 것으로 알려진 이름 중 하나가 아닙니다. |

## <a name="remarks"></a>설명

VD_E_OPEN가 문제없이 반환될 수 있습니다. 클라이언트는 이 코드가 반환될 때까지 루프를 통해 OpenDevice를 호출할 수 있습니다.
두 개 이상의 디바이스(예: n개 디바이스)가 구성된 경우 가상 디바이스 세트는 n개의 고유한 디바이스 인터페이스를 반환합니다. 첫 번째 디바이스는 가상 디바이스 세트와 이름이 같습니다. 다른 디바이스는 BACKUP/RESTORE 문의 VIRTUAL_DEVICE 절에 지정된 대로 이름이 지정됩니다.

GetConfiguration 함수는 디바이스를 열 수 있을 때까지 대기하는 데 사용할 수 있습니다.

이 함수가 실패하면 ppVirtualDevice를 통해 null 값이 반환됩니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.