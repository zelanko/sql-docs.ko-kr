---
title: IClientVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::GetConfiguration 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d7d42d081b0494feeb5c2b221575e0d5df1143a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847454"
---
# <a name="iclientvirtualdeviceset2getconfiguration-vdi"></a>IClientVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**GetConfiguration** 함수는 서버가 가상 디바이스 세트를 집합을 구성할 때까지 기다리는 데 사용됩니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::GetConfiguration (
   DWORD         dwTimeOut,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>매개 변수

*DwTimeOut* 시간 제한(밀리초)입니다. 제한 시간을 방지하려면 INFINITE를 사용합니다.

*pCfg* 성공적으로 실행되면 서버에서 선택한 구성이 포함됩니다. 자세한 내용은 구성을 참조하세요.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 구성이 반환되었습니다. |
| VD_E_ABORT | SignalAbort가 호출되었습니다. |
| VD_E_TIMEOUT | 함수 시간이 초과되었습니다. |

## <a name="remarks"></a>설명

이 함수는 경고 가능 상태에서 차단됩니다. 성공적으로 호출된 후에는 가상 디바이스 세트의 디바이스가 열릴 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.