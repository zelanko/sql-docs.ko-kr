---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::Open 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9dd14245e10963d7a685c17b24ffd1666c3223a7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896292"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**Open** 함수는 서버에 설정된 가상 디바이스를 열며, COM에서 제공하는 인터페이스 핸들을 사용하는 첫 번째 호출이어야 합니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>매개 변수

*lpInstanceName* 이 문자열은 SQL 명령이 전송될 SQL Server 인스턴스를 식별합니다. 현재 머신의 기본 인스턴스를 식별하기 위해 NULL이 제공될 수 있습니다.

*lpName* BACKUP 또는 RESTORE 명령의 첫 번째 VIRTUAL_DEVICE= 절에서 제공됩니다. 이 이름은 클라이언트에서 만든 가상 디바이스 세트에 대한 액세스 권한을 얻기 위한 키로 사용됩니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_INVALID | 제공된 이름으로 서버에서 액세스할 수 있는 가상 디바이스 세트를 식별하지 못했습니다. |

## <a name="remarks"></a>설명

이 함수가 성공적으로 호출된 후에 서버는 GetConfiguration 및 SetConfiguration을 사용하여 가상 디바이스 세트를 계속 구성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.