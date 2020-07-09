---
title: IClientVirtualDeviceSet2::GetBufferHandle
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::GetBufferHandle 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cf187379aaa664e536710859e08bf084b14657d1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896904"
---
# <a name="iclientvirtualdeviceset2getbufferhandle-vdi"></a>IClientVirtualDeviceSet2::GetBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

일부 애플리케이션은 **IClientVirtualDevice2::GetCommand**에서 반환된 버퍼에서 작동할 두 개 이상의 프로세스가 필요할 수 있습니다. 이 경우 명령을 수신하는 프로세스는 **GetBufferHandle**을 사용하여 버퍼를 식별하는 프로세스 독립 핸들을 가져올 수 있습니다. 그런 다음, 이 핸들은 동일한 가상 디바이스 세트가 열려 있는 다른 프로세스에 전달될 수 있습니다. 해당 프로세스는 IClientVirtualDeviceSet2::MapBufferHandle을 사용하여 버퍼의 주소를 가져옵니다. 각 프로세스는 서로 다른 주소에서 버퍼를 매핑할 수 있으므로 이 주소는 파트너에 있는 주소와 다를 수 있습니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::GetBufferHandle (
   BYTE*         pBuffer,
   DWORD*      pBufferHandle
);
```

## <a name="parameters"></a>매개 변수

*pBuffer* Read 또는 Write 명령에서 가져온 버퍼의 주소입니다.

*pBufferHandle* 버퍼의 고유 식별자가 반환됩니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 현재 열려 있지 않습니다. |
| VD_E_INVALID | pBuffer가 유효한 주소가 아닙니다. |

## <a name="remarks"></a>설명

GetBufferHandle 함수를 호출하는 프로세스는 데이터 전송이 완료될 때 IClientVirtualDevice2::CompleteCommand를 호출해야 합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.