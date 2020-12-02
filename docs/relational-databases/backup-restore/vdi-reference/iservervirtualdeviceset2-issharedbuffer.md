---
title: IServerVirtualDeviceSet2::IsSharedBuffer
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::IsSharedBuffer 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 5e969b4cb9bef48d11a884dd3bfec7d2fcabde88
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125322"
---
# <a name="iservervirtualdeviceset2issharedbuffer-vdi"></a>IServerVirtualDeviceSet2::IsSharedBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**IsSharedBuffer** 함수는 지정된 버퍼 주소가 AllocateBuffer 메서드를 통해 사용할 수 있게 지정된 공유 버퍼 중 하나를 참조하는지를 확인합니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::IsSharedBuffer (
   LPVOID   lpBuffer
);
```

## <a name="parameters"></a>매개 변수

*lpBuffer* 버퍼의 주소입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| TRUE | 버퍼가 공유 버퍼입니다. |
| FALSE | 버퍼가 가상 디바이스 세트의 일부가 아닙니다. |

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.