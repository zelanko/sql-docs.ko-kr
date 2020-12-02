---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDevice::CompleteCommand 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 367d398160daa8b9a9da5bfc3a3285cf61b6d085
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128988"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CompleteCommand** 이 함수는 명령이 완료되었음을 SQL Server에 알리는 데 사용됩니다. 명령에 적합한 완료 정보가 반환되어야 합니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>매개 변수

*pCmd* 이전에 IClientVirtualDevice::GetCommand에서 반환된 명령의 주소입니다.

*dwCompletionCode* 완료 상태를 나타내는 WIN32 상태 코드입니다. 이 매개 변수는 모든 명령에 대해 반환되어야 합니다. 반환된 코드는 실행 중인 명령에 적합해야 합니다. ERROR_SUCCESS는 모든 사례에서 성공적으로 실행된 명령을 나타내는 데 사용됩니다. 가능한 코드의 전체 목록은 Winerror.h 파일을 참조하세요. 각 명령의 일반적인 상태 코드 목록은 명령에 표시됩니다.

*dwBytesTransferred* 성공적으로 전송된 바이트 수입니다. 데이터 전송 명령 Read 및 Write에 대해서만 반환됩니다.

*dwlPosition* GetPosition 명령에만 해당하는 응답입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 완료가 올바르게 표시되었습니다. |
| VD_E_INVALID | pCmd가 활성 명령이 아닙니다. |
| VD_E_ABORT | 중단 신호를 받았습니다. |
| VD_E_PROTOCOL | 디바이스가 열리지 않습니다. |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.
