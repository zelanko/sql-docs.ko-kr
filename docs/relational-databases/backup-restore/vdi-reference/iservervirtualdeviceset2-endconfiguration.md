---
title: IServerVirtualDeviceSet2::EndConfiguration
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::EndConfiguration 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d2ed7365e9a0e895a7deb0ba20d57868a947b350
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896329"
---
# <a name="iservervirtualdeviceset2endconfiguration-vdi"></a>IServerVirtualDeviceSet2::EndConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Endconfiguration** 함수는 서버의 구성이 완료되었음을 VDI에 알립니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::EndConfiguration ();
```

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_ABORT | 중단이 요청되었습니다. |
| VD_E_PROTOCOL | 설정이 구성 가능한 상태가 아닙니다. |
| VD_E_MEMORY | 'RequestBuffers' 호출을 통해 필요한 메모리를 가져올 수 없습니다. 해당 세트는 사용할 수 있는 버퍼 공간이 없는 구성 가능 상태로 유지됩니다. 서버는 버퍼 요구 사항을 줄이거나 작업을 중단할 수 있습니다. |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.