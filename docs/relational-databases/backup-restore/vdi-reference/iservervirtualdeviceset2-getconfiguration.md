---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::GetConfiguration 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d62a2042221bebf04e19a46a21ba81caa7c877b
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847254"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**GetConfiguration** 함수는 클라이언트에서 요청하는 구성을 가져옵니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>매개 변수

*pCfg* IClientVirtualDeviceSet2::Create를 사용하여 클라이언트에서 지정하는 구성입니다.

## <a name="return-value"></a>반환 값

메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. NOERROR 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.

## <a name="remarks"></a>Remarks

서버는 클라이언트에서 제공하는 설정을 검사하고 이에 응답해야 합니다. 자세한 내용은 구성을 참조하세요. 제공된 구성에서 제대로 작동할 수 없는 것으로 확인되면 서버는 SignalAbort를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.