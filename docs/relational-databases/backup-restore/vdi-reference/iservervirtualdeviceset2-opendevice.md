---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::OpenDevice 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4dcec84bd4e46eead1ee558a1b2e0c4013ae9fed
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125363"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**OpenDevice** 함수는 가상 디바이스 세트에서 가상 디바이스 인터페이스를 가져옵니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>매개 변수

*lpName* BACKUP 또는 RESTORE 명령의 첫 번째 VIRTUAL_DEVICE= 절에서 제공됩니다. 이 이름은 클라이언트에서 만든 가상 디바이스 세트에 대한 액세스 권한을 얻기 위한 키로 사용됩니다.

*ppVirtualDevice* 가상 디바이스 인터페이스를 반환하는 데 사용됩니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_OPEN |모든 디바이스가 열렸습니다. |

## <a name="remarks"></a>설명

각 호출은 열려 있지 않은 다음 디바이스를 반환합니다. 이 함수는 가상 디바이스 세트 구성에 지정된 디바이스 수와 동일한 횟수만 호출할 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.